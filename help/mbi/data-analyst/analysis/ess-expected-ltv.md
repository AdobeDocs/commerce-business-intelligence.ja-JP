---
title: 全期間値 (LTV) 分析（基本）
description: 分析を作成して、現在の顧客のライフタイム値を把握し、注文件数が増えるにつれてライフタイム値が増加する方法を予測する方法を説明します。
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# ライフタイム値の予測分析

顧客がより多くの注文をする際に、顧客のライフタイム値を予測することは、あらゆる規模のあらゆるビジネスの最も重要な側面の 1 つです。

次に、現在の顧客のライフタイム値を把握し、より多くの注文でライフタイム値が増加する方法を予測するための分析を作成する手順を示します。

![期待されるライフタイム値](../../assets/expected_ltv_720.png)

## 指標の作成

最初の手順は、次の手順で新しい指標を作成することです。
* に移動します。 **[!UICONTROL Manage Data > Metrics]**
   * 既存の **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >この指標が構築されるテーブル ( おそらく `customer_entity` または `sales_order` ストアがゲストのチェックアウトを受け入れる機能に応じて異なります )。

   * クリック **[!UICONTROL Create New Metric]** 上からテーブルを選択します。
   * この指標では **中央値** の `Customer's lifetime revenue` 列、並べ替え順 `created_at`.
      * [!UICONTROL Filters]:
         * を `Customers we count (Saved Filter Set)` ( または `Registered accounts we count`)
   * 指標に名前を付けます（例： ）。 `Median lifetime revenue`.



## ダッシュボードの作成

指標が作成されたら、次の操作を実行できます。 **ダッシュボードの作成** 次の手順を実行します。
* に移動します。 **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* ダッシュボードに次のような名前を付けます。 `Expected LTV`.

* ここで、すべてのレポートを作成して追加します。

## レポートの作成

>[!NOTE]
>
>オン **[!UICONTROL Time Period:]**&#x200B;を指定する場合、各レポートの期間は `All-time`. 分析のニーズに合わせて自由に変更できます。 このダッシュボードのすべてのレポートは、次のように同じ期間に対応することをお勧めします。 `All time`, `Year-to-date`または `Last 365 days`.

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
      [!UICONTROL グラフの種類]: `Line`
   * オフ `Multiple Y-Axes`

* **全期間注文数別の LTV**
   * 指標 `1`: `Avg lifetime revenue`
   * 指標 `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL 間隔]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 

      [!UICONTROL グラフの種類]: `Line`
   >[!NOTE]
   >
   >すべての値を `Customer's lifetime number of orders`ではなく、新規顧客の数が少ない時点を見て、各顧客の全期間注文額をその時点に手動で追加します。 例えば、1 回の注文で 200 人の顧客、2 回に 75 人、3 回に 15 人、4 回に 3 人の顧客がある場合、 *1、2、3*.

* 既存の [!UICONTROL Avg customer lifetime revenue by cohort] レポート。

レポートを作成したら、このトピックの上部にある画像を参照して、ダッシュボードでのレポートの構成方法を確認してください。
