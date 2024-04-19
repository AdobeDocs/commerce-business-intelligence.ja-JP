---
title: クーポンコード分析（基本）
description: あなたのビジネスのクーポンパフォーマンスについて学ぶことは、注文をセグメント化し、顧客の習慣をより深く理解するための興味深い方法です。
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: d8fc96a58b72c601a5700f35ea1f3dc982d76571
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 0%

---

# 基本クーポンコード分析

あなたのビジネスのクーポンパフォーマンスを理解することは、注文をセグメント化し、顧客の習慣をより深く理解するための興味深い方法です。

このトピックでは、クーポンを取得した顧客のパフォーマンスを理解し、トレンドを確認し、個々のクーポンコードの使用状況を追跡するために、この分析を作成するために必要な手順について説明します。

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## はじめに

まず、クーポンコードの追跡方法に関するメモ。 顧客が注文にクーポンを適用した場合、次の 3 つの問題が発生します。

* 割引は次に反映されます `base_grand_total` 金額（自分 `Revenue` （Commerce Intelligence の指標）
* クーポンコードは、に保存されます。 `coupon_code` フィールド。 このフィールドが NULL （空）の場合、注文にはクーポンが関連付けられていません。
* 割引された金額は、次の場所に保存されます。 `base_discount_amount`. 設定によっては、この値が負または正に表示される場合があります。

Commerce 2.4.7 の時点では、お客様は 1 つの注文に複数のクーポンコードを適用できます。 この場合の解決策は、次のとおりです。

* 適用されたすべてのクーポンコードは、 `coupon_code` フィールドの `sales_order_coupons`. 適用された最初のクーポンコードも、に保存されます。 `coupon_code` フィールドの `sales_order`. このフィールドが NULL （空）の場合、注文にはクーポンが関連付けられていません。

## 指標の作成

最初の手順では、次の手順で新しい指標を作成します。

* に移動します。 **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* 「」を選択します `sales_order`.
* このメトリックは、 **合計** 日 **base_discount_amount** 列、並べ替え順 **created_at**.
   * [!UICONTROL Filters]:
      * を追加 `Orders we count` （保存済みフィルターセット）
      * 以下を追加します。
         * `coupon_code`**等しくない**`[NULL]`
      * 指標に名前を付けます（例：）。 `Coupon discount amount`.

## ダッシュボードの作成

* 指標を作成したら、次の手順を実行します。
   * に移動します。 [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**。
   * ダッシュボードに次のような名前を付けます `_Coupon Analysis_`.

* ここで、すべてのレポートを作成および追加します。

## レポートの作成

* **新しいレポート：**

>[!NOTE]
>
>この [!UICONTROL Time Period]各レポートの**は次のとおりです。 `All-time`. 分析のニーズに合わせて自由に変更できます。 Adobeでは、次のような、このダッシュボードのすべてのレポートが同じ期間をカバーすることをお勧めします `All time`, `Year-to-date`、または `Last 365 days`.

* **クーポン付きの注文**
   * 
     [!UICONTROL 指標]: `Orders`
      * フィルターを追加：
         * [`A`] `coupon_code` **等しくない** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **クーポンのない注文**
   * 
     [!UICONTROL 指標]: `Orders`
      * フィルターを追加：
         * [`A`] `coupon_code` **等しい** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **クーポン付き注文からの純売上高**
   * 
     [!UICONTROL 指標]: `Revenue`
      * フィルターを追加：
         * [`A`] `coupon_code` **等しくない** `[NULL]`

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

* **平均生涯売上高：クーポンで獲得した顧客**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * フィルターを追加：
         * [`A`] `Customer's first order's coupon_code` **等しくない** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **平均生涯売上高：クーポン以外で取得した顧客**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * フィルターを追加：
         * [A] `Customer's first order's coupon_code` **等しい**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **クーポンの使用状況の詳細（初回の注文）**
   * 指標 `1`: `Orders`
      * フィルターを追加：
         * [`A`] `coupon_code` **等しくない**`[NULL]`
         * [`B`] `Customer's order number` **次と等しい** `1`

   * 指標 `2`: `Revenue`
      * フィルターを追加：
         * [`A`] `coupon_code` **等しくない**`[NULL]`
         * [`B`] `Customer's order number` **次と等しい** `1`

      * 名前を変更：  `Net revenue`

   * 指標 `3`: `Coupon discount amount`
      * フィルターを追加：
         * [`A`] `coupon_code` **等しくない**`[NULL]`
         * [`B`] `Customer's order number` **次と等しい** `1`

   * 数式を作成： `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
        [!UICONTROL Format]: `Currency`

   * 数式を作成：**割引率**
      * 数式： `(C / (B - C))`
      * 
        [!UICONTROL Format]: `Percentage`

   * 数式を作成： `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
        [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 間隔]: `None`
   * 
     [!UICONTROL グラフ タイプ]: `Table`

* **初回注文クーポン別の平均生涯売上高**
   * [!UICONTROL Metric]:**平均生涯売上高**
      * フィルターを追加：
         * [`A`] `coupon_code` **等しい**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **クーポンの使用状況の詳細（初回の注文）**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * フィルターを追加：
         * [`A`] `Customer's first order's coupon_code` **等しくない** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 間隔]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 
     [!UICONTROL グラフ タイプ]: **Column**

* **クーポン/非クーポン獲得による新規顧客**
   * 指標 `1`: `New customers`
      * フィルターを追加：
         * [`A`] `Customer's first order's coupon_code` **等しくない** `[NULL]`

      * [!UICONTROL Rename]: `Coupon acquisition customer`

   * 指標 `2`: `New customers`
      * フィルターを追加：
         * [`A`] `coupon_code` **等しい**`[NULL]`

      * [!UICONTROL Rename]: `Non-coupon acquisition customer`

   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`

レポートを作成したら、このトピックの上部にある画像を参照して、ダッシュボード上でレポートを整理する方法を確認します。

>[!NOTE]
>
>Adobe Commerce 2.4.7 以降、のお客様は以下を使用できます **quote_coupons** および **sales_order_coupons** 顧客が複数のクーポンをどのように使用しているかに関するインサイトを取得するテーブル。

![](../../assets/multicoupon_relationship_tables.png)
