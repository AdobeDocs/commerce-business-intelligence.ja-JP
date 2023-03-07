---
title: e コマースデータのフォーマットとインポート
description: e コマースデータのアップロードに使用する最適なデータ形式について説明します。
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# データのフォーマットとインポート

現在、でサポートされていない統合を使用している場合 [!DNL MBI]を使用する場合、 [ファイルのアップロード機能](using-file-uploader.md) データをData Warehouseに取り込む この記事では、e コマースデータのアップロードに使用する最適なデータ形式について説明します。

## `Orders` 表

この `orders` テーブルには、ビジネスが実行したトランザクションごとに 1 つの行を含める必要があります。 使用可能な列は次のとおりです。

| 列名 | 説明 |
|----|----|
| `Order ID` | 注文 ID は、テーブルの各行で一意である必要があります。 また、これは通常、テーブルのプライマリキーです。 |
| `Customer` | 注文を行った顧客。 |
| `Order total` | 注文の合計。 これは、計算に基づく列で、小計や送料など、他の列の値がこの列の合計を構成する場合があります。 |
| `Currency` | 注文が支払われた通貨。 必要に応じてを含めます。 |
| ` Order status` | 注文のステータス（例： ） `In Progress`, `Refunded`または `Complete`. この列の値は変更されます（完了していない場合）。 新しいデータと更新されたデータは、 [データ追加機能](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) の `File Uploads` ページ。 |
| `Acquisition/marketing channel` | 注文をした顧客が参照元となった獲得またはマーケティングチャネル。 |
| `Order datetime` | 注文が作成された日時。 |
| `Order updated at` | 注文レコードに最後に変更が加えられた日時。 |

{style="table-layout:auto"}

## `Order detail/items` 表 {#itemstable}

この `order_detail / items` テーブルでは、個々のアイテムごとに、それぞれの順序で 1 行が含まれている必要があります。 使用可能な列は次のとおりです。

| 列名 | 説明 |
|----|----|
| `Order item ID` | 注文項目 ID は、テーブルの各行で一意である必要があります。 また、通常、 `primary key` テーブルの |
| `Order ID` | 注文の ID。 |
| `Product ID` | 製品の ID。 |
| `Product name` | 製品の名前。 |
| `Product's unit price` | 製品の 1 単位の価格。 |
| `Quantity` | 注文の商品の数量。 |

## `Customers` 表 {#customerstable}

この `customers` テーブルには、顧客アカウントごとに 1 つの行を含める必要があります。 使用可能な列は次のとおりです。

| 列名 | 説明 |
|----|----|
| `Customer ID` | 顧客 ID は、テーブルの各行で一意である必要があります。 また、これは通常、テーブルのプライマリキーです。 |
| `Customer created at` | 顧客アカウントが作成された日時。 |
| `Customer modified at` | 顧客アカウントが最後に変更された日時。 |
| `Acquisition/marketing channel source` | 顧客が参照された獲得またはマーケティングチャネル。 |
| `Demographic info` | レポートのセグメント化には、年齢の範囲や性別などの人口統計情報を使用できます。 |
| `Acquisition/marketing channel` | 注文をした顧客が参照元となった獲得またはマーケティングチャネル。 |

## `Subscription payments` 表

この `subscriptions` テーブルには、購読の支払いごとに 1 行が含まれている必要があります。 使用可能な列は次のとおりです。

| 列名 | 説明 |
|----|----|
| `Subscription ID` | 購読 ID は、テーブルの行ごとに一意である必要があります。 また、これは通常、テーブルのプライマリキーです。 |
| `Customer ID` | 支払いをおこなった顧客の ID。 |
| `Payment amount` | 購読の支払い金額。 |
| `Start date` | 支払いの対象となる期間の開始日時。 |
| `End date` | 支払いの対象となる期間の終了日時。 |
