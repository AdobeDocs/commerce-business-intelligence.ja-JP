---
title: クーポンコード分析（基本）
description: ビジネスのクーポンパフォーマンスについて学ぶと、注文をセグメント化し、顧客の習慣をより深く理解する興味深い方法です。
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# 基本的なクーポンコード分析

ビジネスのクーポンパフォーマンスを理解することは、注文をセグメント化し、顧客の習慣をより深く理解するための興味深い方法です。

この分析を作成するために必要な手順を文書化し、クーポンを取得した顧客がどのように実行し、トレンドを確認し、個々のクーポンコードの使用を追跡するかを理解しました。

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## はじめに

まず、クーポンコードの追跡方法に関するメモを追加します。 顧客が 1 つの注文にクーポンを適用すると、次の 3 つのことがおこなわれます。

* 割引が `base_grand_total` ( `Revenue` 指標（MBI 内）
* クーポンコードは、 `coupon_code` フィールドに入力します。 このフィールドが NULL（空）の場合、注文にはクーポンが関連付けられません。
* 割引額は、 `base_discount_amount`. 設定に応じて、この値は負の値または正の値になる場合があります。

## 指標の作成

最初の手順は、次の手順で新しい指標を作成することです。

* に移動します。 **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* を選択します。 `sales_order`.
* この指標では **合計** の **base_discount_amount** 列、並べ替え順 **created_at**.
   * [!UICONTROL Filters]:
      * を `Orders we count` （保存済みフィルタセット）
      * 以下を追加します。
         * `coupon_code`**IS NOT**`[NULL]`
      * 指標に名前を付けます（例： ）。 `Coupon discount amount`.

## ダッシュボードの作成

* 指標が作成されたら、次の手順に従います。
   * に移動します。 [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
   * ダッシュボードに次のような名前を付けます。 `_Coupon Analysis_`.

* ここで、すべてのレポートを作成して追加します。

## レポートの作成

* **新しいレポート：**

>[!NOTE]
>
>この [!UICONTROL Time Period]**レポートごとに、 `All-time`. 分析のニーズに合わせて自由に変更できます。 このダッシュボードのすべてのレポートは、次のように同じ期間に対応することをお勧めします。 `All time`, `Year-to-date`または `Last 365 days`.

* **クーポンを含む注文**
   * 
      [!UICONTROL 指標]: `Orders`
      * フィルターを追加：
         * [`A`] `coupon_code` **IS NOT** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **クーポンのない注文**
   * 
      [!UICONTROL 指標]: `Orders`
      * フィルターを追加：
         * [`A`] `coupon_code` **次に該当** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **クーポンを含む注文からの純売上高**
   * 
      [!UICONTROL 指標]: `Revenue`
      * フィルターを追加：
         * [`A`] `coupon_code` **IS NOT** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **クーポンからの割引**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **全期間平均売上高：獲得したクーポン顧客**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * フィルターを追加：
         * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **全期間平均売上高：獲得した非クーポン顧客**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * フィルターを追加：
         * [A] `Customer's first order's coupon_code` **次に該当**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **クーポン使用状況の詳細（初回注文）**
   * 指標 `1`: `Orders`
      * フィルターを追加：
         * [`A`] `coupon_code` **IS NOT**`[NULL]`
         * [`B`] `Customer's order number` **次と等しい** `1`
   * 指標 `2`: `Revenue`
      * フィルターを追加：
         * [`A`] `coupon_code` **IS NOT**`[NULL]`
         * [`B`] `Customer's order number` **次と等しい** `1`
      * 名前を変更：  `Net revenue`
   * 指標 `3`: `Coupon discount amount`
      * フィルターを追加：
         * [`A`] `coupon_code` **IS NOT**`[NULL]`
         * [`B`] `Customer's order number` **次と等しい** `1`
   * 新しい数式を作成： `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
         [!UICONTROL Format]: `Currency`
   * 新しい数式を作成：**割引率**
      * 数式： `(C / (B - C))`
      * 
         [!UICONTROL Format]: `Percentage`
   * 新しい数式を作成： `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
         [!UICONTROL Format]: `Percentage`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 間隔]: `None`
   * 

      [!UICONTROL グラフの種類]: `Table`








* **初回注文クーポン別の平均ライフタイム売上高**
   * [!UICONTROL Metric]:**平均全期間売上高**
      * フィルターを追加：
         * [`A`] `coupon_code` **次に該当**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **クーポン使用状況の詳細（初回注文）**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * フィルターを追加：
         * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 間隔]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 

      [!UICONTROL グラフの種類]: **Column**


* **クーポン別/クーポン以外の獲得別の新規顧客**
   * 指標 `1`: `New customers`
      * フィルターを追加：
         * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`
      * [!UICONTROL Rename]: `Coupon acquisition customer`
   * 指標 `2`: `New customers`
      * フィルターを追加：
         * [`A`] `coupon_code` **次に該当**`[NULL]`
      * [!UICONTROL Rename]: `Non-coupon acquisition customer`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`





レポートを作成したら、このトピックの上部にある画像を参照して、ダッシュボードでのレポートの構成方法を確認してください。
