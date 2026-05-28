---
title: 顧客濃度の定義
description: 総売上が顧客基盤にどのように分配されるかを測定するためのダッシュボードの設定方法を説明します。
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Developer, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/kayq-ci-AiHHgNoaX09h6dqKQX14MudLvEqFmos3hQE
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 483
ht-degree: 0%

---

# 顧客中心主義

このトピックでは、総売上が顧客基盤にどのように分配されるかを測定するためのダッシュボードの設定方法を示します。 顧客の何パーセントが売上の何パーセントに貢献しているかを把握し、高い貢献度を持つ顧客を惹きつけ、維持するために最適なマーケティング方法をセグメント化されたリストを作成できます。

この分析には、[高度な計算列](../data-warehouse-mgr/adv-calc-columns.md)が含まれています。

## はじめに

最初に、値が1のプライマリキーのみを含むファイルをアップロードする必要があります。 これにより、分析に必要な計算列を作成できます。

[&#x200B; ファイルアップローダー](../importing-data/connecting-data/using-file-uploader.md)と以下の画像を使用して、ファイルをフォーマットできます。

## 予定列

元のアーキテクチャを使用している場合（例えば、`Manage Data` メニューの下に`Data Warehouse Views` オプションがない場合）は、サポートチームに連絡して以下の列を作成する必要があります。 新しいアーキテクチャでは、これらの列は`Manage Data > Data Warehouse` ページから作成できます。 詳細な手順は以下のとおりです。

あなたのビジネスがゲストの注文を許可するならば、さらに区別されます。 その場合、`customer_entity` テーブルのすべての手順を無視できます。 ゲスト注文が許可されていない場合は、`sales_flat_order` テーブルのすべての手順を無視します。

作成する列

* `Sales_flat_order/customer_entity` テーブル
* （入力） `reference`
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `entity_id`
* [!UICONTROL Calculation]: - **Aがnullの場合、その後nullの場合、1 end**
* [!UICONTROL Datatype]: - `Integer`

* `Customer concentration` テーブル （これは、番号`1`を付けてアップロードしたファイルです）
* 顧客数
* [!UICONTROL Column type]: - `Many to One > Count Distinct`
* パス - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`または`customer_entity.(input)reference > Customer Concentration.Primary Key`
* 選択された列 – `sales_flat_order.customer_email`または`customer_entity.entity_id`

* `customer_entity` テーブル
* 顧客数
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* パス - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* 選択した列 – `Number of customers`

* （入力） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: - `Same table > Event Number`
* イベント所有者 – `Number of customers`
* イベントランク - `Customer's lifetime revenue`

* 顧客の収益率
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`、`Number of customers`
* [!UICONTROL Calculation]: - **&#x200B; Aがnullの場合、その後nullの場合（A/B） *100 end &#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

* `Sales_flat_order` テーブル
* 顧客数
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* パス - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* 選択した列 – `Number of customers`

* （input）顧客生涯売上別ランキング
* [!UICONTROL Column type]: - `Same table > Event Number`
* イベント所有者 – `Number of customers`
* イベントランク - `Customer's lifetime revenue`
* フィルター – `Customer's order number = 1`

* 顧客の収益率
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`、`Number of customers`
* [!UICONTROL Calculation]: - **&#x200B; Aがnullの場合、その後nullの場合（A/B） *100 end &#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>使用されるパーセンタイルは顧客の分割であり、顧客基盤のXth パーセンタイルを表します。 各顧客は、1から100までの整数に関連付けられており、これは顧客生涯売上&#x200B;*ランク*&#x200B;と見なすことができます。 例えば、特定の顧客に対する顧客の収益パーセンタイルが&#x200B;**5**&#x200B;の場合、この顧客は全顧客の&#x200B;***5 パーセンタイル***&#x200B;に含まれます（生涯収益）。

## 指標

* **合計顧客生涯価値**
* `customer_entity` テーブル内
* この指標は&#x200B;**合計**&#x200B;を実行します
* `Customer's lifetime revenue`列
* `Customer's first order date` タイムスタンプで注文

## レポート

* **顧客集中度**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* &#x200B;
  [!UICONTROL グループ化：]: `Independent`
* 指標`A`: `Total customer lifetime revenue by percentile`
* 指標`B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* 上/下を表示：`100% of Customer's revenue percentile Name`
* &#x200B;
  [!UICONTROL Chart type]: `Line`

* **上位10%濃度**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* 指標`A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* グラフを隠す
* &#x200B;
  [!UICONTROL グループ化：]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **購入が1回だけの場合の最下位50%の集中**

* 指標`A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* グラフを隠す
* &#x200B;
  [!UICONTROL グループ化：]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **下10%濃度**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* 指標`A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* グラフを隠す
* &#x200B;
  [!UICONTROL グループ化：]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

すべてのレポートをまとめた後、必要に応じてダッシュボード上でレポートを整理できます。 結果は、上記のサンプルダッシュボードのようになります。

この分析の構築中に質問が発生した場合、または単にプロフェッショナルサービスチームに連絡したい場合は、[&#x200B; サポートにお問い合わせください](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
