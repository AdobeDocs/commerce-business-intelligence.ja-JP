---
title: Adobe Commerceへのデータの保存
description: データの生成方法、新しい行の挿入の原因、Adobe Commerce データベースにアクションを記録する方法について説明します。
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/IUTQdZYcHkue-29jNZOxONAK4u5plphslzqtUXJ5JAs
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 962
ht-degree: 3%

---

# [!DNL Adobe Commerce]にデータを保存しています

[!DNL Adobe Commerce] プラットフォームは、数百のテーブルにまたがる様々な価値あるコマースデータを記録して整理します。 このトピックでは、以下について説明します。

* データの生成方法
* 新しい行を[ コア Commerce テーブル ](../data-warehouse-mgr/common-mage-tables.md)のいずれかに挿入する原因
* 購入やアカウントの作成などのアクションを[!DNL Adobe Commerce] データベースに記録する方法

これらの概念について説明するには、次の例を参照してください。

`Clothes4U`は、オンラインと実店舗の両方を利用した衣料品のretailerです。 Web サイトの背後にある[!DNL Magento Open Source]を使用してデータを収集および整理します。

## `catalog\_product\_entity`

9月22日です。`Clothes4U`は、秋のラインに3つの新しいアイテムをロールアウトしています：`Throwback Bellbottoms`、`Straight Leg Jeans`、`V-Neck T-Shirts`。 `Clothes4U`人の従業員がCommerce管理者を開き、**[!UICONTROL Add Product]**&#x200B;をクリックし、`Throwback Bellbottoms`のすべての情報を入力します。

`Throwback Bellbottoms`のすべての設定に満足した従業員は、**[!UICONTROL Save]**&#x200B;をクリックし、下の最初の行を`catalog_product_entity` テーブルに挿入します。 このプロセスを繰り返し、別のCommerce製品を`Straight Leg Jeans`用に作成し、次に`V-Neck T-Shirt`用に3行目を作成し、下の2行目と3行目を`catalog_product_entity` テーブルに挿入します。

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | パンツ 11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id` – これは`catalog_product_entity` テーブルのプライマリキーです。つまり、テーブルのすべての行に異なる`entity_id`が必要です。 このテーブルの各`entity_id`は1つの製品にのみ関連付けることができ、各製品は1つの`entity_id`にのみ関連付けることができます
   * 上のテーブルの一番上の行、`entity_id` = 205は、「Throwback Bellbottoms」用に作成された新しい行です。 Commerce プラットフォームに`entity_id` = 205が表示される場合は、「Throwback Bellbottoms」という商品を指しています
* `entity_type_id` - Commerceには複数のカテゴリのオブジェクト （顧客、住所、商品など）があり、この列はこの特定の行が属するカテゴリを示すために使用されます。
   * これは`catalog_product_entity` テーブルです。各行のエンティティの種類はproductと同じです。 Adobe Commerceでは、商品の`entity_type_id`は4です。そのため、作成された3つの新商品すべてがこの列に4を返します。
* `attribute_set_id` – 属性セットは、同じ記述子を持つ製品を識別するために使用されます。
   * テーブルの上位2行は`Throwback Bellbottoms`および`Straight Leg Jeans`製品で、どちらもパンツです。 これらの製品には同じ記述子（名前、inseam、waistlineなど）が含まれているため、同じ`attribute_set_id`が使用されます。 3つ目のアイテム `V-Neck T-Shirt`は、パンツと同じ記述子を持たないため、異なる`attribute_set_id`を持っています。シャツにはウエスト線や縫い目がありません。
* `sku` – これらは、Adobe Commerceで商品を作成する際にユーザーが各商品に割り当てた一意の値です。
* `created_at` – この列は、各製品が作成されたときのタイムスタンプを返します

## `customer\_entity`

3つの新製品が追加された直後、新規顧客`Sammy Customer`が`Clothes4U`のweb サイトに初めてアクセスしました。 `Clothes4U`はゲスト注文を許可していないため、`Sammy Customer`は最初にweb サイトでアカウントを作成する必要があります。 お客様が必要な資格情報を入力し、「送信」をクリックすると、[`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md)に次の新しいエントリが表示されます。

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` – 前のテーブルと同様に、`entity_id`は`customer_entity` テーブルの主キーです。
   * `Sammy Customer`がアカウントを作成し、上記の行が`customer_entity` テーブルに書き込まれると、顧客に`entity_id` = 214が割り当てられました。 すべてのテーブルで、`entity_id` = 214として識別された顧客は、常にユーザーSammy Customerを参照します
* `entity_type_id` – この列は、このテーブルにリストされているエンティティのタイプを特定し、`catalog_product_entity` テーブルと同じように機能します
   * `customer_entity` テーブルのすべての行は顧客であり、Commerceはデフォルトで`entity_type_id` 1として顧客を定義します
* `email` – このフィールドには、新規顧客がアカウントを作成するときに入力する電子メールが入力されます
* `created_at` – この列は、各ユーザーが参加した時点のタイムスタンプを返します

## [!DNL Adobe Commerce 2.x]をお持ちの場合は`sales\_flat\_order (or Sales\_order`

アカウントの作成が完了したら、`Sammy Customer`様が購入を開始する準備ができました。 Web サイトで、お客様は`Throwback Bellbottoms`の2組と`V-Neck T-Shirt`の1組をカートに追加します。 選択に満足した後、お客様はチェックアウトに移動し、注文を送信します。[販売注文テーブル ](../data-warehouse-mgr/sales-flat-order-table.md)に次のエントリを作成します。

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id` – これは`sales_flat_order` テーブルのプライマリキーです。
   * Sammy Customerがこの注文を行い、上の行が`sales_flat_order` テーブルに書き込まれると、注文は`entity_id` = 227に割り当てられました。
* `customer_id` – この列は、この特定の注文を行った顧客の一意のIDです
   * この注文に関連付けられている`customer_id`は214です。これは、`customer_entity` テーブルのSammy Customerの`entity_id`です。
* `subtotal` – この列は、注文の顧客に請求された合計金額です
   * 「Throwback Bellbottoms」と「V-Neck T-Shirt」の2組の価格は合計で94.85 ドルでした
* `created_at` – この列は、各注文が作成されたときのタイムスタンプを返します

## `sales\_flat\_order\_item ( or Sales\_order\_item`

（Commerce 2.0以降をお持ちの場合）

`Sales\_flat\_order` テーブルの1行に加えて、`Sammy Customer`が注文を送信すると、その注文の各一意の項目の行が[`sales\_flat\_order\_item` テーブル ](../data-warehouse-mgr/sales-flat-order-item-table.md)に挿入されます。

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id` – この列は`sales_flat_order_item` テーブルのプライマリキーです
   * `Sammy Customer`の注文では、このテーブルに2行の行が作成されました。注文には2つの異なる商品が含まれています
* `name` – この列は製品の名前です
* `product_id` – この列は、この行が参照している製品の一意の識別子です
   * 上の最初の行には`product_id` = 205があります。`Throwback Bellbottoms`には`catalog_product_entity` テーブルに205の`entity_id`があるためです
* `order_id` – この列は、これらの特定の注文項目を含む注文の`entity_id`です
   * 上の行は両方とも`order_id` = 227です。これは、両方とも`Sammy Customer`によって配置された注文の一部であり、`sales_flat_order` テーブルに`entity_id` = 227が含まれているためです
* `qty_ordered` – この列は、この特定の順序に含まれる製品の単位数です
   * `Sammy Customer`の注文には、2組の`Throwback Bellbottoms`が含まれています
* `price` – この列は、注文項目の1単位の価格です
   * `sales_flat_order` テーブルの`Sammy Customer`の注文からの`subtotal`は94.85で、これは、各$39.95の`Throwback Bellbottoms`と$14.95の`V-Neck T-Shirt`の2つのペアの合計です。
