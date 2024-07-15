---
title: Adobe Commerceへのデータの保存
description: データの生成方法、新しい行が挿入される原因およびAdobe Commerce データベースにアクションが記録される方法について説明します。
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# [!DNL Adobe Commerce] へのデータの保存

[!DNL Adobe Commerce] プラットフォームは、数百のテーブルにわたる様々な貴重なコマースデータを記録および整理します。 このトピックでは、以下について説明します。

* そのデータの生成方法
* [ コア Commerce テーブル ](../data-warehouse-mgr/common-mage-tables.md) の 1 つに新しい行が挿入される理由
* 購入やアカウントの作成などのアクションを [!DNL Adobe Commerce] データベースに記録する方法

これらの概念については、次の例を参照してください。

`Clothes4U` は、オンラインと実店舗の両方のプレゼンテーションを行う衣料品小売業者です。 Web サイトの背後にある [!DNL Magento Open Source] を使用して、データを収集および整理します。

## `catalog\_product\_entity`

9 月 22 日（PT）に、秋のライ `Clothes4U` に `Throwback Bellbottoms`、`Straight Leg Jeans`、`V-Neck T-Shirts` の 3 つの新しいアイテムをロールアウトします。 ある社 `Clothes4U` の社員がCommerce管理者を開き、**[!UICONTROL Add Product]** をクリックして、`Throwback Bellbottoms` のすべての情報を入力します。

`Throwback Bellbottoms` のすべての設定に満足したら、従業員は **[!UICONTROL Save]** をクリックし、下の最初の行を `catalog_product_entity` テーブルに挿入します。 従業員はプロセスを繰り返し、`Straight Leg Jeans` に別のCommerce製品を作成し、次に `V-Neck T-Shirt` に 3 つ目の製品を作成して、`catalog_product_entity` の表に次の 2 行目と 3 行目を挿入します。

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | ズボン 10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | ズボン 11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | シャツ 6 | 2016/09/22 09:24:02 |

* `entity_id` – これは `catalog_product_entity` テーブルのプライマリ・キーです。つまり、テーブルのローごとに異なる `entity_id` が必要です。 このテーブルの各 `entity_id` は 1 つの製品にのみ関連付けることができ、各製品は 1 つの製 `entity_id` にのみ関連付けることができます
   * 前述の表の一番上の行 `entity_id`= 205 は、「Throwback Bellbottoms」用に作成された新しい行です。 Commerce プラットフォームで `entity_id` = 205 が表示される場合は、製品「Throwback Bellbottoms」を参照しています
* `entity_type_id` - Commerceには複数のカテゴリのオブジェクト（顧客、住所、商品など）があり、この列は、この特定の行が分類されるカテゴリを示すために使用されます。
   * これは `catalog_product_entity` テーブルであり、各行のエンティティタイプは product と同じです。 Adobe Commerceでは商品の `entity_type_id` は 4 なので、作成された新製品 3 つはこの列に 4 を返します。
* `attribute_set_id` – 属性セットは、同じ記述子を持つ製品を識別するために使用されます。
   * テーブルの上の 2 列は `Throwback Bellbottoms` と `Straight Leg Jeans` の商品で、どちらもパンツです。 これらの製品には同じ記述子（名前、継ぎ目、ウエストラインなど）が使用されるので、`attribute_set_id` が同じになります。 3 番目のアイテムは、ズボン `V-Neck T-Shirt` 同じ記述子を持たないので異なる `attribute_set_id` を持っています。シャツにはウエストラインや縫い目がありません。
* `sku` - Adobe Commerceで商品を作成する際にユーザーが各商品に割り当てる一意の値です。
* `created_at` – この列は、各製品が作成された際のタイムスタンプを返します

## `customer\_entity`

3 つの新製品が追加された直後、新規顧客の `Sammy Customer` が初めて `Clothes4U` の Web サイトを訪問します。 `Clothes4U` はゲストによる注文を許可しないので、`Sammy Customer` ず web サイト上でアカウントを作成する必要があります。 顧客が必要な資格情報を入力して「送信」をクリックすると、[`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md) に次の新しいエントリが表示されます。

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` – 前のテーブルと同様に、`entity_id` は `customer_entity` のテーブルのプライマリキーです。
   * `Sammy Customer` がアカウントを作成し、上記の行が `customer_entity` テーブルに書き込まれると、顧客は `entity_id` = 214 に割り当てられました。 すべてのテーブルで、`entity_id` = 214 と識別される顧客は、常にユーザー Sammy Customer を指します
* `entity_type_id` – この列は、このテーブルにリストされるエンティティのタイプを識別し、`catalog_product_entity` テーブルと同じように機能します
   * `customer_entity` テーブルの行はすべて顧客であり、Commerceでは、顧客をデフォルトで `entity_type_id`1 として定義しています
* `email` – このフィールドには、新規顧客がアカウントの作成時に入力するメールが入力されます
* `created_at` – この列は、各ユーザーが参加した際のタイムスタンプを返します

## [!DNL Adobe Commerce 2.x] がある場合は `sales\_flat\_order (or Sales\_order`

アカウントの作成が完了 `Sammy Customer` たら、購入を開始する準備が整います。 Web サイトでは、顧客は 2 組の `Throwback Bellbottoms` と 1 組の `V-Neck T-Shirt` を買い物かごに追加します。 選択が完了すると、顧客はチェックアウトに移動し、受注を発行します。[ 受注フラット表 ](../data-warehouse-mgr/sales-flat-order-table.md) に次のエントリが作成されます。

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id` - `sales_flat_order` テーブルのプライマリキーです。
   * Sammy Customer がこの注文を行い、上記の行が `sales_flat_order` テーブルに書き込まれると、注文は `entity_id` = 227 に割り当てられました。
* `customer_id` – この列は、この特定の注文を行った顧客の一意の識別子です
   * この注文に関連付けられている `customer_id` は 214 です。これは、Sammy Customer の `customer_entity` テーブルの `entity_id` です。
* `subtotal` – この列は、受注に対して顧客に請求される合計金額です
   * 「Throwback Bellbottons」と「V-Neck T シャツ」の 2 組は合計 94.85 ドルでした
* `created_at` – この列は、各注文が作成された際のタイムスタンプを返します

## `sales\_flat\_order\_item ( or Sales\_order\_item`

（Commerce 2.0 以降の場合）

`Sales\_flat\_order` テーブルの 1 つの行に加えて、注文を送信 `Sammy Customer` ると、注文の一意の各項目の行が [`sales\_flat\_order\_item` テーブルに挿入され ](../data-warehouse-mgr/sales-flat-order-item-table.md) す。

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id` – この列は `sales_flat_order_item` テーブルの主キーです
   * 注文に 2 つの異なる製品が含まれていたため、`Sammy Customer` の注文によってこのテーブルに 2 行が作成されました
* `name` – この列は製品名です
* `product_id` – この列は、この行が参照している製品の一意の ID です
   * 上記の最初の行には `product_id` = 205 があります `Throwback Bellbottoms` これは、`catalog_product_entity` テーブルの `entity_id` が 205 であるためです
* `order_id` – この列は、これらの特定の注文項目を含む注文の `entity_id` です
   * 上記の行は、両方とも `Sammy Customer` から注文された注文の一部なので、`order_id` = 227 です。`sales_flat_order` テーブルの場合、`entity_id` = 227 です
* `qty_ordered` – この列は、この特定の順序に含まれる製品の単位数です
   * `Sammy Customer` の注文には 2 組の `Throwback Bellbottoms` が含まれていた
* `price` – この列は、受注品目の 1 単位の価格です
   * `sales_flat_order` 表の `Sammy Customer` の注文からの `subtotal` は 94.85 で、これは `Throwback Bellbottoms` の 2 組の合計をそれぞれ 39.95 ドル、1`V-Neck T-Shirt` を 14.95 ドルとした。
