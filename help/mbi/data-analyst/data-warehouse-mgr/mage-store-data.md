---
title: Adobe Commerceへのデータの格納
description: データの生成方法、新しい行の挿入原因、アクションのAdobe Commerceデータベースへの記録方法について説明します。
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# データの格納先 [!DNL Adobe Commerce]

The [!DNL Adobe Commerce] プラットフォームは、数百のテーブルにわたって様々な貴重なコマースデータを記録し、整理します。 ここでは、以下について説明します。

* データの生成方法
* 新しい行を [コアコマーステーブル](../data-warehouse-mgr/common-mage-tables.md)
* 購入やアカウントの作成などのアクションを [!DNL Adobe Commerce] データベース

これらの概念について説明するには、次の例を参照してください。

`Clothes4U` は、オンラインとレンガとモルタルの両方のプレゼンスを持つ衣料品店です。 次を使用します。 [!DNL Magento Open Source] データを収集および整理するために、Web サイトの背後に配置されている。

## `catalog\_product\_entity`

9 月 22 日、 `Clothes4U` は、秋の行に 3 つの新しい項目を展開しています。 `Throwback Bellbottoms`, `Straight Leg Jeans`、および `V-Neck T-Shirts`. A `Clothes4U` 従業員がコマース管理者を開き、「 **[!UICONTROL Add Product]**&#x200B;を入力し、 `Throwback Bellbottoms`.

のすべての設定に満足 `Throwback Bellbottoms`をクリックした場合、従業員は **[!UICONTROL Save]**：の下に最初の行を挿入します。 `catalog_product_entity` 表。 従業員はこのプロセスを繰り返し、次のための別のコマース製品を作成します。 `Straight Leg Jeans`そして 3 つ目は `V-Neck T-Shirt`の下に 2 行目と 3 行目を挿入し、 `catalog_product_entity` テーブル：

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id`  — これは、 `catalog_product_entity` テーブル ( テーブルの各行に異なる `entity_id`. 各 `entity_id` このテーブルで関連付けることができる製品は 1 つだけで、各製品を関連付けることができる製品は 1 つだけです `entity_id`
   * 上の表の上の行 `entity_id` = 205 は、「Throwback Bellbottoms」用に作成された新しい行です。 どこでも `entity_id` = 205 は、コマースプラットフォームに表示され、製品「Throwback Bellbottoms」を参照しています。
* `entity_type_id`  — コマースには、複数のカテゴリのオブジェクト（顧客、住所、製品など）があり、この列は、この特定の行が該当するカテゴリを示すために使用されます。
   * これは `catalog_product_entity` テーブルでは、各行のエンティティタイプが product と同じになっています。 Adobe Commerceでは、 `entity_type_id` 製品が 4 の場合、新しく作成された 3 つの製品はすべて、この列に 4 を返すのです。
* `attribute_set_id`  — 属性セットは、記述子と同じ製品を識別するために使用されます。
   * テーブルの上の 2 行は、 `Throwback Bellbottoms` および `Straight Leg Jeans` 両方ともズボンの製品です。 これらの製品は同じ記述子（名前、縫い目、胴回りなど）を持つので、同じ記述子を持ちます `attribute_set_id`. 3 つ目の項目は、 `V-Neck T-Shirt` が異なる `attribute_set_id` ズボンと同じ記述子を持たないので、シャツには胴の胴に胴脚や縫い目がないのです。
* `sku`  — ユーザーがAdobe Commerceで製品を作成する際に各製品に割り当てる一意の値です。
* `created_at`  — この列は、各製品が作成された日時のタイムスタンプを返します

## `customer\_entity`

3 つの新しい製品が追加された直後に、新しいお客様が `Sammy Customer`，訪問 `Clothes4U`初めてのウェブサイト。 次以降 `Clothes4U` ゲストによる注文を許可しません。 `Sammy Customer` まず、web サイト上にアカウントを作成する必要があります。 顧客が必要な資格情報を入力し、「送信」をクリックすると、 [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id`  — 前のテーブルと同じように。 `entity_id` は、 `customer_entity` 表。
   * 条件 `Sammy Customer` アカウントが作成され、上の行が `customer_entity` テーブル、顧客が割り当てられました `entity_id` = 214 すべてのテーブルで、顧客が `entity_id` = 214 は常に、Sammy 顧客を指します
* `entity_type_id`  — この列は、このテーブルにリストされているエンティティのタイプを識別し、 `catalog_product_entity` 表
   * 各行の `customer_entity` テーブルが顧客で、 Commerce が顧客を `entity_type_id` デフォルトでは 1
* `email`  — このフィールドは、新規顧客がアカウントを作成する際に入力する E メールによって設定されます
* `created_at`  — この列は、各ユーザーが参加した際のタイムスタンプを返します

## `sales\_flat\_order (or Sales\_order` もし [!DNL Adobe Commerce 2.x]

アカウントの作成が完了したら、 `Sammy Customer` は、購入を開始する準備が整っています。 この Web サイトで、顧客が `Throwback Bellbottoms` 一つ `V-Neck T-Shirt` を買い物かごに追加します。 選択に満足した顧客はチェックアウトに移動し、注文を送信し、次のエントリを [販売フラット注文テーブル](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id`  — これは、 `sales_flat_order` 表。
   * Sammy 顧客がこの注文を行い、上の行が `sales_flat_order` テーブルに、注文が割り当てられました `entity_id` = 227
* `customer_id`  — この列は、この特定の注文をした顧客の一意の識別子です
   * The `customer_id` この注文に関連付けられているのは 214 で、これは Sammy 顧客の `entity_id` の `customer_entity` 表。
* `subtotal`  — この列は、注文に対して顧客に請求された合計金額です
   * 「Throwback Bellbottoms」と「V-Neck T-Shirt」の 2 組のペアは、合計 94.85 ドルでした
* `created_at`  — この列は、各注文が作成された際のタイムスタンプを返します

## `sales\_flat\_order\_item ( or Sales\_order\_item`

（Commerce 2.0 以降を使用している場合）

また、 `Sales\_flat\_order` 表、場合 `Sammy Customer` オーダーを送信し、そのオーダーの一意のアイテムごとに行が [`sales\_flat\_order\_item` 表](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id`  — この列は、 `sales_flat_order_item` 表
   * `Sammy Customer`注文に 2 つの異なる製品が含まれているので、このテーブルに 2 行が作成されました
* `name`  — この列は製品の名前です
* `product_id`  — この列は、この行が参照している製品の一意の識別子です
   * 上の最初の行には、 `product_id` = 205( 理由： `Throwback Bellbottoms` 持っている `entity_id` 205 日に `catalog_product_entity` 表
* `order_id`  — この列は `entity_id` この特定の注文項目を含む注文の
   * 上の両方の行には `order_id` = 227。どちらも次の順序の一部であるためです。 `Sammy Customer`( ) `entity_id` = 227 （上） `sales_flat_order` 表
* `qty_ordered`  — この列は、この特定の注文に含まれる製品の数量です
   * `Sammy Customer`の順序には 2 組のが含まれていました `Throwback Bellbottoms`
* `price`  — この列は、注文項目の 1 単位の価格です
   * The `subtotal` から `Sammy Customer`の順序は、 `sales_flat_order` 表は 94.85 で、これは `Throwback Bellbottoms` 39.95 ドルで、それぞれ 1 ドルで `V-Neck T-Shirt` 14.95 ドル。
