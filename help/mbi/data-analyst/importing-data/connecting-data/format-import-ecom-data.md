---
title: コマースデータのフォーマットとインポート
description: e コマースデータのアップロードに使用する理想的なデータ形式について説明します。
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/3Aa9DgQL0H9cNeJOJ7-qHkROOkphjzpQkDvJ0KwOIwY
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 459
ht-degree: 0%

---

# データの書式設定と読み込み

現在[!DNL Adobe Commerce Intelligence]でサポートされていない統合を使用している場合でも、[ ファイルアップロード機能](using-file-uploader.md)を使用してデータをData Warehouseに取り込むことができます。 このトピックでは、e コマースデータのアップロードに使用する理想的なデータ形式について説明します。

## `Orders` テーブル

`orders` テーブルには、ビジネスが実行したトランザクションごとに1行を含める必要があります。 潜在的な列は次のとおりです。

| 列名 | 説明 |
|----|----|
| `Order ID` | 注文IDは、テーブル内の各行に対して一意である必要があります。 また、これは通常、テーブルのプライマリキーです。 |
| `Customer` | 注文した顧客。 |
| `Order total` | 注文の合計。 これは計算ベースの列で、小計や出荷など、他の列の値がこの列の合計を構成します。 |
| `Currency` | 注文が支払われた通貨。 関連する場合は含める。 |
| ` Order status` | 注文のステータス（`In Progress`、`Refunded`、`Complete`など）。 この列の値が変更されます（完全でない場合）。 新しいデータと更新されたデータは、[ ページの](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) データ追加機能`File Uploads`を使用してインポートできます。 |
| `Acquisition/marketing channel` | 注文した顧客が参照された獲得チャネルまたはマーケティングチャネル。 |
| `Order datetime` | 注文が作成された日時。 |
| `Order updated at` | 注文レコードの最後の変更が行われた日時。 |

{style="table-layout:auto"}

## `Order detail/items` テーブル {#itemstable}

`order_detail / items` テーブルには、各順序の個別のアイテムごとに1行を含める必要があります。 潜在的な列は次のとおりです。

| 列名 | 説明 |
|----|----|
| `Order item ID` | 注文項目IDは、テーブル内の各行に対して一意である必要があります。 また、これは通常、テーブルの`primary key`です。 |
| `Order ID` | 注文のID。 |
| `Product ID` | 製品のID。 |
| `Product name` | 製品の名前。 |
| `Product's unit price` | 製品の1単位の価格。 |
| `Quantity` | 注文の製品の数量。 |

## `Customers` テーブル {#customerstable}

`customers` テーブルには、顧客アカウントごとに1行を含める必要があります。 潜在的な列は次のとおりです。

| 列名 | 説明 |
|----|----|
| `Customer ID` | 顧客IDは、テーブル内の各行に対して一意である必要があります。 また、これは通常、テーブルのプライマリキーです。 |
| `Customer created at` | 顧客のアカウントが作成された日時。 |
| `Customer modified at` | 顧客のアカウントが最後に変更された日時。 |
| `Acquisition/marketing channel source` | 顧客が紹介された獲得チャネルまたはマーケティングチャネル。 |
| `Demographic info` | 年齢範囲や性別などのデモグラフィック情報を使用して、レポートをセグメンテーションできます。 |
| `Acquisition/marketing channel` | 注文した顧客が参照された獲得チャネルまたはマーケティングチャネル。 |

## `Subscription payments` テーブル

`subscriptions` テーブルには、サブスクリプションの支払いごとに1行を含める必要があります。 潜在的な列は次のとおりです。

| 列名 | 説明 |
|----|----|
| `Subscription ID` | サブスクリプション IDは、テーブル内の各行に対して一意である必要があります。 また、これは通常、テーブルのプライマリキーです。 |
| `Customer ID` | 支払いを行った顧客のID。 |
| `Payment amount` | サブスクリプションの支払い金額。 |
| `Start date` | 支払いがカバーする期間の開始日時。 |
| `End date` | 支払がカバーする期間の終了日時。 |
