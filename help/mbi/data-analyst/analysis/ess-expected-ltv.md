---
title: 期待生涯価値（LTV）分析（ベーシック）
description: 現在の顧客のライフタイム値を理解し、より多くの注文に伴うライフタイム値の増大方法を予測するための分析を作成する方法を説明します。
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# ライフタイム値の期待分析

より多くの注文を行う際に顧客の生涯価値を予測することは、あらゆる規模のビジネスにおいて最も重要な側面の 1 つです。

以下は、現在の顧客のライフタイム値を理解し、注文が増えるにつれてライフタイム値がどのように増加するかを予測するための分析を作成する手順です。

![期待されるライフタイム値](../../assets/expected_ltv_720.png)

## 指標の作成

最初の手順では、次の手順で新しい指標を作成します。
* に移動します。 **[!UICONTROL Manage Data > Metrics]**
   * 既存のを表示 **[!UICONTROL Avg lifetime revenue]**.

  >[!NOTE]
  >
  >この指標が構成されるテーブル（おそらく） `customer_entity` または `sales_order` ストアがゲストのチェックアウトを受け入れる機能に応じて異なります。）。

   * クリック **[!UICONTROL Create New Metric]** 上からテーブルを選択します。
   * このメトリックは、 **中央値** 日 `Customer's lifetime revenue` 列、並べ替え順 `created_at`.
      * [!UICONTROL Filters]:
         * を追加 `Customers we count (Saved Filter Set)` （または `Registered accounts we count`）

   * 指標に名前を付けます（例：）。 `Median lifetime revenue`.

## ダッシュボードの作成

指標を作成すると、次の操作を実行できます **ダッシュボードの作成** 次の手順を実行します。
* に移動します。 **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* ダッシュボードに次のような名前を付けます `Expected LTV`.

* ここで、すべてのレポートを作成および追加します。

## レポートの作成

>[!NOTE]
>
>日付： **[!UICONTROL Time Period:]**&#x200B;の場合、各レポートの期間は次のように表示されます `All-time`. 分析のニーズに合わせて自由に変更できます。 Adobeでは、次のような、このダッシュボードのすべてのレポートが同じ期間をカバーすることをお勧めします `All time`, `Year-to-date`、または `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * 追加 [!UICONTROL filters]:
         * [`A`] `Customer's group code` **次と等しくない** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **次より大きい**`0`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average and Median LTV]**
   * 指標 `1`: `Avg lifetime revenue`
   * 指標 `2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
     [!UICONTROL グラフ タイプ]: `Line`
   * Uncheck `Multiple Y-Axes`

* **LTV （全期間の注文数）**
   * 指標 `1`: `Avg lifetime revenue`
   * 指標 `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 間隔]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 
     [!UICONTROL グラフ タイプ]: `Line`

  >[!NOTE]
  >
  >のすべての値を追加しないでください `Customer's lifetime number of orders`. 代わりに、新規顧客の数が少ない時点で、各顧客の注文のライフタイム数をその時点に手動で追加します。 例えば、1 回の注文で 200 人の顧客が存在し、2 回が 75 人、3 回が 15 人、4 回が 3 人の場合、 *1、2、3*.

* 既存のを追加 [!UICONTROL Avg customer lifetime revenue by cohort] レポート。

レポートを作成したら、このトピックの上部にある画像を参照して、ダッシュボード上でレポートを整理する方法を確認します。
