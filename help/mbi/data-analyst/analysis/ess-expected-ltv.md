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

![ 期待されるライフタイム値 ](../../assets/expected_ltv_720.png)

## 指標の作成

最初の手順では、次の手順で新しい指標を作成します。
* **[!UICONTROL Manage Data > Metrics]** に移動します。
   * 既存の **[!UICONTROL Avg lifetime revenue]** を表示します。

  >[!NOTE]
  >
  >この指標が構築されるテーブル（おそらく `customer_entity` または `sales_order` は、ストアがゲストのチェックアウトを受け入れることができるかどうかに応じて異なります）。

   * 「**[!UICONTROL Create New Metric]**」をクリックし、上からテーブルを選択します。
   * この指標は、**列を** 順に並べ替えた `Customer's lifetime revenue` 中央値 `created_at` を実行します。
      * [!UICONTROL Filters]:
         * `Customers we count (Saved Filter Set)` （または `Registered accounts we count`）を追加

   * 指標に名前（例：`Median lifetime revenue`）を付けます。

## ダッシュボードの作成

指標を作成したら、次の操作を実行して **ダッシュボードを作成** できます。
* **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]** に移動します。
* ダッシュボードに `Expected LTV` などの名前を付けます。

* ここで、すべてのレポートを作成および追加します。

## レポートの作成

>[!NOTE]
>
>**[!UICONTROL Time Period:]** に、各レポートの期間が `All-time` として表示されます。 分析のニーズに合わせて自由に変更できます。 Adobeでは、このダッシュボードのすべてのレポートが、`All time`、`Year-to-date`、`Last 365 days` など、同じ期間をカバーすることをお勧めします。

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL 間隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * [!UICONTROL filters] を追加：
         * [`A`] `Customer's group code` **次と等しくない** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **より大きい**`0`

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
   * `Multiple Y-Axes` をオフ

* **LTV （ライフタイム注文数）**
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
  >`Customer's lifetime number of orders` のすべての値を追加しないでください。 代わりに、新規顧客の数が少ない時点で、各顧客の注文のライフタイム数をその時点に手動で追加します。 例えば、1 回の注文で 200 人の顧客が存在し、2 が 75 人、3 が 15 人、4 が 3 人の場合、*1、2 および 3* を加算します。

* 既存の [!UICONTROL Avg customer lifetime revenue by cohort] レポートを追加します。

レポートを作成したら、このトピックの上部にある画像を参照して、ダッシュボード上でレポートを整理する方法を確認します。
