---
title: 最新性、頻度、通貨 (RFM) 分析
description: 最新性、頻度、および金額のランク付けによって顧客をセグメント化できるダッシュボードを設定する方法を説明します。
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# RFM 分析

この記事では、最新性、頻度、金額のランク付けによって顧客をセグメント化できるダッシュボードを設定する方法を示します。 RFM 分析は、顧客行動を考慮に入れてアウトリーチのセグメント化を決定するマーケティング手法です。 次の 3 つの側面を考慮します。顧客が最近店舗から購入した最新性、顧客が自分から購入した頻度、顧客がどの程度購入したかに関する通貨。

![](../../assets/blobid0.png)

RFM 分析は、 [!DNL MBI] 新しいアーキテクチャの計画を立てます ( 例えば、「Data Warehouseを管理」メニューの「データビュー」オプションがある場合 )。 これらの列は、「データを管理/Data Warehouse」ページから作成できます。 詳細な手順は以下のとおりです。

## はじめに

最初に、値が 1 のプライマリキーのみを含むファイルをアップロードする必要があります。 これにより、分析に必要な計算列を作成できます。

この [ヘルプセンター記事](../importing-data/connecting-data/using-file-uploader.md) および以下の画像でファイルの形式を設定してください。

## 計算列

お客様のビジネスがゲストの注文を許可する場合は、さらに区別がおこなわれます。 その場合、 `customer_entity` 表。 ゲストによる注文が許可されない場合、 `sales_flat_order` 表。

作成する列

* **`Sales_flat_order/customer_entity`** 表
* `Customer's last order date`
* [!UICONTROL Column type]: `Many to one > Max`
* [!UICONTROL Pat]: `sales_flat_order.customer_id > customer_entity.entity_id`
* 選択済み [!UICONTROL column]: `created_at`
* [!UICONTROL Filter]: `Orders we count`

* 

       顧客の最終注文日からの経過秒数
   * [!UICONTROL Column type]:- &quot;同じ表 > 年齢
* 選択済み [!UICONTROL column]: `Customer's last order date`

* （入力）カウントの参照
* [!UICONTROL Column type]: `Same table > Calculation`
* 
   [!UICONTROL 入力]: `entity_id`
* [!UICONTROL Calculation]: `**case when A is null then null else 1 end**`
* 

   [!UICONTROL データ型]: `Integer`

* **カウントの参照** テーブル（数字が「1」のファイル）
* 顧客数
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `ales_flat_order.(input) reference > Count reference.Primary Key` または `customer_entity.(input)reference > Count Reference`. `Primary Key`
* 選択済み [!UICONTROL column]: `sales_flat_order.customer_email` または `customer_entity.entity_id`

* **Customer_entity** 表
* 顧客数
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity`.（入力）参照 > お客様の集中。 `Primary Key`
* 選択済み [!UICONTROL column]: `Number of customers`

* （入力） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime revenue`

* 顧客のライフタイム売上高別のランキング
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [!UICONTROL データ型]: `Integer`

* 顧客の金額スコア（パーセンタイル単位）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL データ型]: `Integer`

* （入力）顧客のライフタイム番号による注文件数のランキング
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime number of orders`

* 顧客のライフタイム数別のランキング（注文件数）
* 
   [!UICONTROL 列タイプ]: – "同じテーブル/計算"
* [!UICONTROL Inputs]:- **（入力）顧客のライフタイム番号による注文件数のランキング**, **顧客数**
* [!UICONTROL Calculation]:- **A が null の場合は Null、それ以外の場合 (B-(A-1)) は終了**
* [!UICONTROL Datatype]: — 整数

* 顧客の頻度スコア（パーセンタイル単位）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL データ型]: `Integer`

* 顧客の最終注文日からの秒数別のランキング
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Seconds since customer's last order date`

* 顧客の最新性スコア（パーセンタイル単位）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL データ型]: `Integer`

* 顧客の最新性スコア（パーセンタイル単位）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* 

   [!UICONTROL データ型]: String

* **カウントの参照** 表
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `sales_flat_order.(input) reference > Customer Concentration. Primary Key` または `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 選択済み [!UICONTROL column]: `sales_flat_order.customer_email` または `customer_entity.entity_id`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` 000 と等しくない

* **Customer_entity** 表
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity.(input) reference > Customer Concentration.Primary Key`
* 選択済み [!UICONTROL column]:- `Number of customers`

* 顧客の最新性スコア `(R+F+M)`
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: – `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* 

   [!UICONTROL データ型]: `Integer`

* （入力）顧客の RFM スコア全体によるランキング
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's recency score (R+F+M)`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` 000 と等しくない

* 顧客の RFM 全体スコア別のランキング
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer's overall RFM score`, `Number of customers (RFM > 0)`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [!UICONTROL データ型]: `Integer`

* 顧客の RFM グループ
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* 

   [!UICONTROL データ型]: `Integer`

>[!NOTE]
>
>使用されるパーセンタイルは、顧客の均等分割です（例えば、1 ～ 5 を返す 20%グループ）。 これらを重み付けするカスタム方法がある場合は、チケットを送信する際にアナリストに知らせてください。

## 指標

新しい指標がありません。

**注意**:必ず [すべての新しい列を指標のディメンションとして追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に

## レポート

* **RFM グループ別の顧客**
* 指標 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's RFM score (by percentiles) Not Equal to 000`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* グラフを非表示
* [!UICONTROL Group by]: `Customer's RFM group`
* 
   [!UICONTROL グループ化基準]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **最新性スコアが 5 回の顧客**
* 指標 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 5`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 
   [!UICONTROL Chart Type]: `Scalar`
* グラフを非表示
* 
   [!UICONTROL グループ化基準]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

* **最新性スコアが 1 の顧客**
* 指標 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 1`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 
   [!UICONTROL Chart Type]: `Scalar`
* グラフを非表示
* 
   [!UICONTROL グループ化基準]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

すべてのレポートをコンパイルした後、必要に応じてダッシュボードで整理できます。 最終結果は上記のサンプルダッシュボードのようになりますが、3 つの生成されたテーブルは、実行できる顧客セグメントのタイプの例に過ぎません。
