---
title: 最新性、頻度、通貨（RFM）分析
description: 顧客のリーセンシー、頻度、通貨ランキング別に顧客をセグメント化できるダッシュボードの設定方法を説明します。
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# RFM 分析

このトピックでは、顧客のリーセンシー、頻度、通貨ランキング別に顧客をセグメント化できるダッシュボードの設定方法を説明します。 RFM 分析は、顧客の行動を考慮して、アウトリーチのためのセグメント化を決定するのに役立つマーケティング テクニックです。 次の 3 つの側面が考慮されます。

1. ストアから顧客が購入した最近の最新性
1. 顧客が自社から購入する頻度
1. お客様が費やす金額

![&#x200B; リーセンシー、頻度、金銭的価値セグメントを示す RFM 分析ダッシュボード &#x200B;](../../assets/blobid0.png)

RFM 分析は、新しいアーキテクチャに [!DNL Adobe Commerce Intelligence] Pro プランがある場合（たとえば、`Data Warehouse Views` メニューの `Manage Data` オプションがある場合）にのみ設定できます。 これらの列は、**[!DNL Manage Data > Data Warehouse]** のページから作成できます。 詳細な手順は次のとおりです。

## はじめに

まず、値が 1 のプライマリキーのみを含むファイルをアップロードする必要があります。 これにより、分析に必要な計算列を作成できます。

この [&#x200B; 記事 &#x200B;](../importing-data/connecting-data/using-file-uploader.md) と以下の画像を使用して、ファイルをフォーマットできます。

## 計算される列

ビジネスでゲストによる注文が許可されている場合は、さらに区別されます。 その場合は、`customer_entity` テーブルのすべてのステップを無視できます。 ゲストの注文が許可されていない場合は、`sales_flat_order` テーブルのすべてのステップを無視します。

作成する列

* **`Sales_flat_order/customer_entity`** テーブル
* `Customer's last order date`
* [!UICONTROL Column type]: `Many to one > Max`
* [!UICONTROL Pat]: `sales_flat_order.customer_id > customer_entity.entity_id`
* 選択された [!UICONTROL column]: `created_at`
* [!UICONTROL Filter]: `Orders we count`

* &#x200B;
       顧客の最終注文日からの経過時間（秒） 
  * [!UICONTROL Column type]: -     &quot;同じテーブル > 年齢
* 選択された [!UICONTROL column]: `Customer's last order date`

* （入力）カウント参照
* [!UICONTROL Column type]: `Same table > Calculation`
* &#x200B;
  [!UICONTROL 入力]: `entity_id`
* [!UICONTROL Calculation]: `**case when A is null then null else 1 end**`
* &#x200B;
  [!UICONTROL データ型]: `Integer`

* **カウント参照** テーブル（これは「1」という番号でアップロードしたファイルです）
* 顧客の数
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `ales_flat_order.(input) reference > Count reference.Primary Key` または `customer_entity.(input)reference > Count Reference`。`Primary Key`
* 選択された [!UICONTROL column]: `sales_flat_order.customer_email` または `customer_entity.entity_id`

* **Customer_entity** テーブル
* 顧客の数
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity`。（入力） リファレンス > 顧客集中度。`Primary Key`
* 選択された [!UICONTROL column]: `Number of customers`

* （入力） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime revenue`

* 顧客の生涯売上高によるランキング
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* &#x200B;
  [!UICONTROL データ型]: `Integer`

* 顧客の通貨スコア （パーセンタイル単位）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* &#x200B;
  [!UICONTROL データ型]: `Integer`

* （入力）顧客のライフタイムナンバーごとの注文ランキング
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime number of orders`

* 顧客の生涯注文数によるランキング
* &#x200B;
  [!UICONTROL 列タイプ]: – "同じテーブル/計算"
* [!UICONTROL Inputs]: - **（入力）顧客のライフタイム数によるランキング注文数**、**顧客数**
* [!UICONTROL Calculation]: - **A が null の場合は null、それ以外の場合は（B – （A-1））終了**
* [!UICONTROL Datatype]: – 整数

* 顧客の頻度スコア （パーセンタイル単位）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* &#x200B;
  [!UICONTROL データ型]: `Integer`

* 顧客の前回の注文日以降のランキング （秒）
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Seconds since customer's last order date`

* 顧客の最新性スコア （パーセンタイル単位）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* &#x200B;
  [!UICONTROL データ型]: `Integer`

* 顧客の最新性スコア （パーセンタイル単位）
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `Customer's recency score (by percentiles)`、`Customer's frequency score (by percentiles)`、`Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* &#x200B;
  [!UICONTROL データ型]: String

* **カウント参照** テーブル
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `sales_flat_order.(input) reference > Customer Concentration. Primary Key` または `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 選択された [!UICONTROL column]: `sales_flat_order.customer_email` または `customer_entity.entity_id`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` が 000 と等しくない

* **Customer_entity** テーブル
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity.(input) reference > Customer Concentration.Primary Key`
* 選択された [!UICONTROL column]: - `Number of customers`

* 顧客の最新性スコア `(R+F+M)`
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: - `Customer's recency score (by percentiles)`、`Customer's frequency score (by percentiles)`、`Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* &#x200B;
  [!UICONTROL データ型]: `Integer`

* （入力）顧客の RFM 全体スコア別のランキング
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's recency score (R+F+M)`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` が 000 と等しくない

* 顧客の RFM スコア全体によるランキング
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer's overall RFM score`, `Number of customers (RFM > 0)`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* &#x200B;
  [!UICONTROL データ型]: `Integer`

* 顧客の RFM グループ
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* &#x200B;
  [!UICONTROL データ型]: `Integer`

>[!NOTE]
>
>使用されるパーセンタイルは、顧客の偶数分割です（例えば、20% バケットで 1～5 のリターン）。 カスタムウェイで重みを付けたい場合は、チケットの送信時にアナリストにお知らせください。

## 指標

新しい指標はありません。

>[!NOTE]
>
>新しいレポートを作成する前に、必ず [&#x200B; すべての新しい列をディメンションとして指標に追加する &#x200B;](../data-warehouse-mgr/manage-data-dimensions-metrics.md) ようにしてください。

## レポート

* **RFM グループ別の顧客**
* 指標 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's RFM score (by percentiles) Not Equal to 000`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* グラフを非表示
* [!UICONTROL Group by]: `Customer's RFM group`
* &#x200B;
  [!UICONTROL Group by]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **5 つの最新性スコアを持つ顧客**
* 指標 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 5`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`
* グラフを非表示
* &#x200B;
  [!UICONTROL Group by]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **1 つの最新性スコアを持つ顧客**
* 指標 `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 1`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`
* グラフを非表示
* &#x200B;
  [!UICONTROL Group by]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

すべてのレポートをコンパイルした後、必要に応じてダッシュボード上で整理できます。 結果は上記のサンプルダッシュボードのようになりますが、生成された 3 つのテーブルは、実行できる顧客セグメント化のタイプの例に過ぎません。
