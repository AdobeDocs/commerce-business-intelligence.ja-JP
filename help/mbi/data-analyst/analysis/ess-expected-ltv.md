---
title: LTV （期待生涯価値）分析（基本）
description: 分析を作成して、現在の顧客の生涯価値を理解し、より多くの注文で生涯価値がどのように増加するかを予測する方法を説明します。
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
role: Admin, User
feature: Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/bGbpknj6UfM8k995EnptIRfwZsvYTNo8-kzF9HrALQk
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 338
ht-degree: 0%

---

# 期待される生涯価値分析

より多くの注文をおこなう顧客の生涯価値を予測することは、規模を問わず、あらゆる企業にとって最も重要な側面のひとつです。

次の手順に従って、分析を実施して、既存顧客の生涯価値を把握し、より多くの注文が発生するにつれて生涯価値がどのように増加するかを予測します。

![期待されるライフタイム値](../../assets/expected_ltv_720.png)

## 指標の構築

最初の手順は、次の手順で新しい指標を作成することです。
* **[!UICONTROL Manage Data > Metrics]**&#x200B;に移動
   * 既存の&#x200B;**[!UICONTROL Avg lifetime revenue]**&#x200B;を表示します。

  >[!NOTE]
  >
  >この指標が作成されるテーブル （おそらく`customer_entity`または`sales_order`は、お客様のストアのゲストチェックアウトの受け入れ機能によって異なります）。

   * **[!UICONTROL Create New Metric]**&#x200B;をクリックし、上からテーブルを選択します。
   * この指標は、**様が注文した**&#x200B;列に`Customer's lifetime revenue`中央値`created_at`を実行します。
      * [!UICONTROL Filters]:
         * `Customers we count (Saved Filter Set)` （または`Registered accounts we count`）を追加

   * 指標に`Median lifetime revenue`などの名前を付けます。

## ダッシュボードの作成

指標を作成したら、次の操作を実行して&#x200B;**ダッシュボードを作成できます**。
* **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**&#x200B;に移動します。
* ダッシュボードに`Expected LTV`などの名前を付けます。

* ビューでは、すべてのレポートを作成および追加できます。

## レポートの作成

>[!NOTE]
>
>**[!UICONTROL Time Period:]**&#x200B;には、各レポートの期間が`All-time`として表示されます。 分析ニーズに合わせて変更してください。 Adobeでは、`All time`、`Year-to-date`、`Last 365 days`など、このダッシュボードのすべてのレポートが同じ期間をカバーすることをお勧めします。

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * [!UICONTROL filters]を追加：
         * [`A`] `Customer's group code` **次と等しくない** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **より大**`0`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL間隔]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average and Median LTV]**
   * 指標`1`: `Avg lifetime revenue`
   * 指標`2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
     [!UICONTROL チャートタイプ]: `Line`
   * `Multiple Y-Axes`のチェックを外す

* 注文数のライフタイム数による&#x200B;**LTV**
   * 指標`1`: `Avg lifetime revenue`
   * 指標`2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL間隔]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 
     [!UICONTROL チャートタイプ]: `Line`

  >[!NOTE]
  >
  >`Customer's lifetime number of orders`の値をすべて追加しないでください。 代わりに、新規顧客数が少数に達した時点を見て、各顧客の顧客生涯注文額をその時点に手動で追加します。 例えば、1つの注文に200人の顧客があり、75人が2人、15人が3人、3人が4人の場合、*1、2、および3*&#x200B;を追加します。

* 既存の[!UICONTROL Avg customer lifetime revenue by cohort] レポートを追加します。

レポートを作成した後、ダッシュボードでレポートを整理する方法については、このトピックの上部にある画像を参照してください。
