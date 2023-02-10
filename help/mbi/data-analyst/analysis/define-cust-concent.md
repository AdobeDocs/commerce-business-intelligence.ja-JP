---
title: 顧客の集中度を定義
description: 顧客ベース間での合計売上高の分布を測定するのに役立つダッシュボードを設定する方法を説明します。
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# 顧客の集中

この記事では、顧客ベース間での合計売上高の分布を測定するのに役立つダッシュボードの設定方法を示します。 どの割合の顧客が売上高に貢献しているかを把握し、最適なマーケットに最適なセグメント化リストを作成して、貢献度の高い顧客を維持します。

この分析に含まれる内容 [高度な計算列](../data-warehouse-mgr/adv-calc-columns.md).

## はじめに

最初に、値が 1 のプライマリキーのみを含むファイルをアップロードする必要があります。 これにより、分析に必要な計算列を作成できます。

以下を利用して、 [ファイルアップローダ](../importing-data/connecting-data/using-file-uploader.md) および以下の画像でファイルの形式を設定してください。

## 計算列

元のアーキテクチャを使用している場合 ( 例えば、 `Data Warehouse Views` オプションを `Manage Data` メニュー ) を使用する場合は、以下の列を構築するために、アドビのサポートチームに連絡する必要があります。 新しいアーキテクチャでは、これらの列は `Manage Data > Data Warehouse` ページ。 詳細な手順は以下のとおりです。

お客様のビジネスがゲストの注文を許可する場合は、さらに区別がおこなわれます。 その場合、 `customer_entity` 表。 ゲストによる注文が許可されない場合、 `sales_flat_order` 表。

作成する列

* `Sales_flat_order/customer_entity` 表
* （入力） `reference`
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `entity_id`
* [!UICONTROL Calculation]:- **A が null の場合は Null の場合、それ以外の場合は 1 の終わり**
* [!UICONTROL Datatype]: – `Integer`

* `Customer concentration` テーブル ( これは、アップロードしたファイルの番号 `1`)
* 顧客数
* [!UICONTROL Column type]: – `Many to One > Count Distinct`
* パス — `sales_flat_order.(input) reference > Customer Concentration.Primary Key` または `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 選択された列 — `sales_flat_order.customer_email` または `customer_entity.entity_id`

* `customer_entity` 表
* 顧客数
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* パス — `customer_entity.(input) reference > Customer Concentration. Primary Key`
* 選択された列 — `Number of customers`

* （入力） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: – `Same table > Event Number`
* イベント所有者 — `Number of customers`
* イベントのランク — `Customer's lifetime revenue`

* 顧客の売上高の百分位
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]:- **A が null の場合は Null を、それ以外の場合 (A/B)* 100 終了&#x200B;**
* [!UICONTROL Datatype]: – `Decimal`

* `Sales_flat_order` 表
* 顧客数
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* パス — `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* 選択された列 — `Number of customers`

* （入力）顧客のライフタイム売上高別のランキング
* [!UICONTROL Column type]: – `Same table > Event Number`
* イベント所有者 — `Number of customers`
* イベントランク — `Customer's lifetime revenue`
* フィルター — `Customer's order number = 1`

* 顧客の売上高の百分位
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]:- **A が null の場合は Null を、それ以外の場合 (A/B)* 100 終了&#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>使用されるパーセンタイルは、顧客の第 1 百分位を表す複数の顧客を偶数分割したものです。 各顧客には 1 ～ 100 の整数が関連付けられます。これは、顧客の全期間売上高と考えることができます *rank*. 例えば、特定の顧客の売上高の百分位値が **5**&#x200B;の場合、この顧客は ***第 5 百分位*** の全期間の売上高に関するすべての顧客の

## 指標

* **合計顧客ライフタイム値**
* 内 `customer_entity` 表
* この指標では **合計**
* の `Customer's lifetime revenue` 列
* 発注元： `Customer's first order date` timestamp

## レポート

* **顧客の集中**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
   [!UICONTROL グループ化基準]: `Independent`
* 指標 `A`: `Total customer lifetime revenue by percentile`
* 指標 `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* 上/下を表示： `100% of Customer's revenue percentile Name`
* 

   [!UICONTROL Chart type]: `Line`

* **上位 10%の濃度**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* 指標 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* グラフを非表示
* 
   [!UICONTROL グループ化基準]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **1 回の購入で 50%以下の集中**

* 指標 `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* グラフを非表示
* 
   [!UICONTROL グループ化基準]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **下 10%濃度**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* 指標 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* グラフを非表示
* 
   [!UICONTROL グループ化基準]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

すべてのレポートをコンパイルした後、必要に応じてダッシュボードで整理できます。 最終結果は、上記のサンプルダッシュボードのようになります。

この分析の構築中に質問が発生した場合、または単にプロフェッショナルサービスチームを引き込みたい場合、 [連絡先サポート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
