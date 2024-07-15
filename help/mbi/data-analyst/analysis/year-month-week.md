---
title: 年次、月次および週次レポート
description: 時間の経過に伴うトレンドを簡単に確認する方法と、比較したい期間の視点を変更する方法を説明します。
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 一定期間のレポート

>[!NOTE]
>
>このトピックには、元のアーキテクチャと新しいアーキテクチャを使用しているクライアント向けの手順が含まれています。 メインのツールバーから「[!DNL _Data Warehouseビュー [」セクションを選択できる場合は_] 新しいアーキテクチャ ](../../administrator/account-management/new-architecture.md) を開 [!DNL Manage Data] ています。

Report Builder を使用すると、経時的なトレンドを簡単に確認し、比較したい期間の視点を変更できます。 このトピックでは、より深いレベルに到達するためのダッシュボードを設定する方法を説明します。これにより、週別、月別、年別分析のレポートを作成できます。

![](../../assets/Wow__mom__yoy.png)

始める前に、より詳細な視点を探索する [ こちら ](../../tutorials/using-visual-report-builder.md) および独立した時間オプション [ こちら ](../../tutorials/time-options-visual-rpt-bldr.md) を確認する必要があります。

この分析には [ 高度な計算列 ](../data-warehouse-mgr/adv-calc-columns.md) が含まれています。

## 計算される列

* **`Sales_flat_order`** テーブル
* **元のアーキテクチャ：** 以下の列は、`[YoY WoW MoM ANALYSIS]` チケットの一部としてアナリストによって作成されています
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **新しいアーキテクチャ：** この計算の作成方法の例を示す写真付きの以下の SQL
   * `created_at (month-day)` [!UICONTROL Calculation]: **to_char （A, &#39;mm-dd&#39;）**
   * `created_at (month)` [!UICONTROL Calculation]: **to_char （A, &#39;mm-month&#39;）**
   * `created_at (day of the month)`&lt; [!UICONTROL Calculation]: **to_char （A, &#39;dd&#39;）**
   * `created_at (day of the week)` [!UICONTROL Calculation]: **to_char （A, &#39;d-Day&#39;）**
   * **`created_at (hour of the day)` [!UICONTROL Calculation]: **to_char （A, &#39;hh24&#39;）**
     ![](../../assets/new-arch-create-calc.png)

## 指標

なし。

>[!NOTE]
>
>新しいレポートを作成する前に、必ず [ すべての新しい列をディメンションとして指標に追加する ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) ようにしてください。

## レポート

* **YoY グラフ**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom]：上位 100% を **`created_at (month-day)`***で並べ替えた場合

* 指標 `A`: `This year`
* 指標 `B`: `Last year`
* [!UICONTROL Time period]: `1 year ago to 0 years ago`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (month-day)`
* 
  [!UICONTROL Chart Type]: `Line`

* **MoM グラフ**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 時間オプション：`Time range (Custom)`: `2 months ago to 1 month ago`

   * 上/下を表示：上位 100% を **`created_at (day of month)`***で並べ替え

* 指標 `A`：今月*
* 指標 `B`：先月*
* [!UICONTROL Time period]:1 か月前から 0 か月前
* 
  [!UICONTROL Interval]: None
* [!UICONTROL Group by]: `created_at (day of month)`
* 
  [!UICONTROL Chart Type]: Line

* **WoW グラフ**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom]：上位 100% を `created_at (day of week)` 順に並べ替えた場合

* 指標 `A`: `This week`
* 指標 `B`: `Last week`
* [!UICONTROL Time period]: `1 week ago to 0 weeks ago`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (day of week)`
* 
  [!UICONTROL Chart Type]: `Line`

* **DoD グラフ**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 days ago to 1 day ago`

   * [!UICONTROL Show top/bottom]：上位 100% を `created_at (hour of day)` 順に並べ替えた場合

* 指標 `A`: `Today`
* 指標 B: `Yesterday`
* [!UICONTROL Time period]: `1 day ago to 0 days ago`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (hour of day)`
* 
  [!UICONTROL Chart Type]: `Line`

すべてのレポートをコンパイルした後、必要に応じてダッシュボード上で整理できます。 結果は、このページの上部の画像のようになります。
