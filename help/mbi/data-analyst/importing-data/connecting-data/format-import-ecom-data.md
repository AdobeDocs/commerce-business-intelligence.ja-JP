---
title: e コマースデータのフォーマットと読み込み
description: e コマースデータのアップロードに使用する理想的なデータ形式について説明します。
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# データのフォーマットとインポート

[!DNL Adobe Commerce Intelligence] で現在サポートされていない統合を使用している場合でも、[ ファイルアップロード機能 ](using-file-uploader.md) を使用してデータをData Warehouseに取り込むことができます。 このトピックでは、e コマースデータのアップロードに使用する理想的なデータ形式について説明します。

## `Orders` テーブル

`orders` テーブルには、ビジネスが実行したすべてのトランザクションに対して 1 行を含める必要があります。 可能な列は次のとおりです。

| 列名 | 説明 |
|----|----|
| `Order ID` | 注文 ID は、テーブルの行ごとに一意である必要があります。 また、これは通常、テーブルのプライマリキーです。 |
| `Customer` | 注文を行った顧客。 |
| `Order total` | 注文の合計。 これは計算ベースの列である可能性があり、小計や出荷などの他の列の値がこの列の合計を構成します。 |
| `Currency` | 注文の支払いに使用された通貨。 該当する場合は含めます。 |
| ` Order status` | 注文のステータス（`In Progress`、`Refunded`、`Complete` など）。 この列の値は変更されます（完了していない場合）。 新しいデータや更新されたデータは、`File Uploads` のページの [ データを追加機能 ](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) を使用して読み込むことができます。 |
| `Acquisition/marketing channel` | 注文を行った顧客が紹介された獲得またはマーケティングチャネル。 |
| `Order datetime` | 注文が作成された日時。 |
| `Order updated at` | 注文レコードに対して最後に変更が加えられた日時。 |

{style="table-layout:auto"}

## `Order detail/items` テーブル {#itemstable}

`order_detail / items` テーブルには、各順序で個別の項目ごとに 1 行を含める必要があります。 可能な列は次のとおりです。

| 列名 | 説明 |
|----|----|
| `Order item ID` | 注文項目 ID は、テーブルの行ごとに一意である必要があります。 また、これは通常、テーブルの `primary key` です。 |
| `Order ID` | 注文の ID。 |
| `Product ID` | 商品の ID。 |
| `Product name` | 商品の名前。 |
| `Product's unit price` | 商品の 1 単位の価格。 |
| `Quantity` | オーダー内の商品の数量。 |

## `Customers` テーブル {#customerstable}

`customers` テーブルには、顧客アカウントごとに 1 行を含める必要があります。 可能な列は次のとおりです。

| 列名 | 説明 |
|----|----|
| `Customer ID` | 顧客 ID は、テーブルの行ごとに一意である必要があります。 また、これは通常、テーブルのプライマリキーです。 |
| `Customer created at` | 顧客のアカウントが作成された日時。 |
| `Customer modified at` | 顧客のアカウントが最後に変更された日時。 |
| `Acquisition/marketing channel source` | 顧客が参照された獲得またはマーケティングチャネル。 |
| `Demographic info` | 年齢層や性別などの人口統計情報を使用して、レポートをセグメント化できます。 |
| `Acquisition/marketing channel` | 注文を行った顧客が紹介された獲得またはマーケティングチャネル。 |

## `Subscription payments` テーブル

`subscriptions` テーブルには、サブスクリプション支払ごとに 1 行を含める必要があります。 可能な列は次のとおりです。

| 列名 | 説明 |
|----|----|
| `Subscription ID` | 購読 ID は、テーブルの行ごとに一意である必要があります。 また、これは通常、テーブルのプライマリキーです。 |
| `Customer ID` | 支払いを行った顧客の ID。 |
| `Payment amount` | サブスクリプションの支払い金額。 |
| `Start date` | 支払いの対象となる期間の開始日時。 |
| `End date` | 支払が対象とする期間の終了日時。 |
