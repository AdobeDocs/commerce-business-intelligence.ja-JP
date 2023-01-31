---
title: 年別、月別、週別のレポート
description: 経時的なトレンドの確認方法と、比較する期間のパースペクティブの変更方法を説明します。
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# 長期にわたるレポート

>[!NOTE]
>
>この記事では、元のアーキテクチャと新しいアーキテクチャを使用しているお客様向けの手順について説明します。 あなたは [新しいアーキテクチャ](../../administrator/account-management/new-architecture.md) もし _Data Warehouseビュー_ 選択後に使用可能なセクション `Manage Data` を選択します。

Report Builder を使用すると、経時的なトレンドを簡単に確認でき、比較する期間のパースペクティブを変更できます。 この記事では、ダッシュボードを設定して、前週比、前月比、前年比の分析用のレポートを作成できるようにする方法を説明します。

![](../../assets/Wow__mom__yoy.png)

開始する前に、より詳細に分析を行うためのパースペクティブについて理解しておく必要があります [ここ](../../tutorials/using-visual-report-builder.md) 独立した時間オプション [ここ](../../tutorials/time-options-visual-rpt-bldr.md).

この分析に含まれる内容 [高度な計算列](../data-warehouse-mgr/adv-calc-columns.md).

## 計算列

* **`Sales_flat_order`** 表
* **元のアーキテクチャ：** 以下の列は、アナリストによって、 `[YoY WoW MoM ANALYSIS]` チケット
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **新しいアーキテクチャ：** 次に、この計算の作成方法の例を示す SQL を示します
   * `created_at (month-day)` [!UICONTROL Calculation]:: **to_char(A, &#39;mm-dd&#39;)**
   * `created_at (month)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-month&#39;)**
   * `created_at (day of the month)`&lt; [!UICONTROL Calculation]: **to_char(A, &#39;dd&#39;)**
   * `created_at (day of the week)` [!UICONTROL Calculation]: **to_char(A, &#39;d-Day&#39;)**
   * **`created_at (hour of the day)` [!UICONTROL Calculation]:: **to_char(A, &#39;hh24&#39;)**

      ![](../../assets/new-arch-create-calc.png)

## 指標

なし。

>[!NOTE]
>
>必ず [すべての新しい列を指標のディメンションとして追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に

## レポート

* **Y グラフ**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom]:上位 100%の並べ替え基準 **`created_at (month-day)`***

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
   * 時間オプション： `Time range (Custom)`: `2 months ago to 1 month ago`

   * 上/下を表示：上位 100%の並べ替え基準 **`created_at (day of month)`***

* 指標 `A`:今月*
* 指標 `B`:先月*
* [!UICONTROL Time period]:1 か月前～ 0 か月前
* 
   [!UICONTROL Interval]: None
* [!UICONTROL Group by]: `created_at (day of month)`
* 
   [!UICONTROL Chart Type]: Line

* **WoW グラフ**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom]:上位 100%の並べ替え基準 `created_at (day of week)`

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

   * [!UICONTROL Show top/bottom]:上位 100%の並べ替え基準 `created_at (hour of day)`

* 指標 `A`: `Today`
* 指標 B: `Yesterday`
* [!UICONTROL Time period]: `1 day ago to 0 days ago`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (hour of day)`
* 
   [!UICONTROL Chart Type]: `Line`

すべてのレポートをコンパイルした後、必要に応じてダッシュボードで整理できます。 最終的な結果は、このページの上部にある画像のように見える場合があります。
