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

# へのデータの保存 [!DNL Adobe Commerce]

この [!DNL Adobe Commerce] platform は、何百ものテーブルにわたって多種多様な貴重なコマースデータを記録し、整理します。 このトピックでは、以下について説明します。

* そのデータの生成方法
* 新しいローがいずれかのローに挿入される原因 [コア Commerce テーブル](../data-warehouse-mgr/common-mage-tables.md)
* 購入やアカウントの作成などのアクションがに記録される方法 [!DNL Adobe Commerce] データベース

これらの概念については、次の例を参照してください。

`Clothes4U` は、オンラインと実店舗の両方のエクスペリエンスを備えた衣料品小売業者です。 が使用されます [!DNL Magento Open Source] web サイトの背後でデータを収集および整理します。

## `catalog\_product\_entity`

九月二十二日です。 `Clothes4U` は、秋のラインに 3 つの新しいアイテムをロールアウトしています。 `Throwback Bellbottoms`, `Straight Leg Jeans`、および `V-Neck T-Shirts`. A `Clothes4U` 従業員がCommerce管理者を開き、クリックする **[!UICONTROL Add Product]**&#x200B;を選択し、に関するすべての情報を入力します。 `Throwback Bellbottoms`.

の設定すべてに満足 `Throwback Bellbottoms`、従業員がクリック **[!UICONTROL Save]**：の下の 1 行目を `catalog_product_entity` テーブル。 従業員はこのプロセスを繰り返し、次のCommerce製品を作成します `Straight Leg Jeans`を選択し、さらに 3 番目の `V-Neck T-Shirt`（下の 2 行目と 3 行目を `catalog_product_entity` テーブル：

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | ズボン 10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | ズボン 11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | シャツ 6 | 2016/09/22 09:24:02 |

* `entity_id`  – これは、 `catalog_product_entity` テーブル。つまり、テーブルの各行に異なる値を指定する必要があります `entity_id`. Each `entity_id` このテーブルでは、1 つの製品にのみ関連付けることができ、各製品は 1 つの製品にのみ関連付けることができます `entity_id`
   * 上のテーブルの一番上の行、 `entity_id` = 205、「バックベルボトムの調整」用に作成された新規行です。 場所を問わず `entity_id` = 205 がCommerce プラットフォームに表示される。これは、商品「Throwback Bellbottoms」を参照しています。
* `entity_type_id` - Commerceには複数のカテゴリのオブジェクト（例：顧客、住所、商品）があり、この列は、この特定の行が分類されるカテゴリを示すために使用されます。
   * これが `catalog_product_entity` テーブル、各行のエンティティタイプは product です。 Adobe Commerceでは、 `entity_type_id` 製品が 4 の場合、3 つの新製品が作成されると、この列には 4 が返されます。
* `attribute_set_id`  – 属性セットは、同じ記述子を持つ製品を識別するために使用されます。
   * テーブルの上位 2 行は `Throwback Bellbottoms` および `Straight Leg Jeans` 両方ともパンツである製品。 これらの製品には同じ記述子（名前、継ぎ目、ウエストラインなど）が使用されるので、同じ記述子が使用されます `attribute_set_id`. 3 番目の項目 `V-Neck T-Shirt` には異なるがあります `attribute_set_id` ズボンと同じ記述子を持たないので、シャツにはウエストラインや縫い目がありません。
* `sku` - Adobe Commerceで商品を作成する際にユーザーが各商品に割り当てる一意の値です。
* `created_at`  – この列は、各製品が作成された際のタイムスタンプを返します

## `customer\_entity`

3 つの新製品を追加した直後、新規顧客、 `Sammy Customer`、訪問回数 `Clothes4U`さんの初めての web サイト。 以降 `Clothes4U` ゲストによる注文は許可されません。 `Sammy Customer` まず、web サイトでアカウントを作成する必要があります。 顧客が必要な資格情報を入力して「送信」をクリックすると、に次の新しいエントリが表示されます。 [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id`  – 前のテーブルと同様に、 `entity_id` は、のプライマリキーです。 `customer_entity` テーブル。
   * 条件 `Sammy Customer` がアカウントを作成し、上記の行がに書き込まれました `customer_entity` テーブル、顧客が割り当てられました `entity_id` = 214。 すべてのテーブルで、顧客は次のように識別されます `entity_id` = 214 は常にユーザー Sammy Customer を参照します。
* `entity_type_id`  – この列は、このテーブルにリストされているエンティティのタイプを識別し、 `catalog_product_entity` テーブル
   * のすべての行 `customer_entity` テーブルは顧客で、Commerceは顧客を次のように定義します `entity_type_id` デフォルトは 1 です
* `email`  – このフィールドには、新規顧客がアカウントの作成時に入力するメールが入力されます
* `created_at`  – この列は、各ユーザーが参加した際のタイムスタンプを返します

## `sales\_flat\_order (or Sales\_order` 以下がある場合： [!DNL Adobe Commerce 2.x]

アカウントの作成が完了したら、 `Sammy Customer` 購入を開始する準備が整いました。 Web サイトでは、顧客は次の 2 つのペアを `Throwback Bellbottoms` と 1 `V-Neck T-Shirt` 買い物かごに。 選択に満足すると、顧客はチェックアウトに移動し、注文を送信します。これにより、 [販売フラット注文テーブル](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id`  – これは、 `sales_flat_order` テーブル。
   * Sammy Customer がこの注文を行い、上記の行がに書き込まれたとき `sales_flat_order` テーブル、注文が割り当てられました `entity_id` = 227。
* `customer_id`  – この列は、この特定の注文を行った顧客の一意の識別子です
   * この `customer_id` この注文に関連するのは 214 で、これは Sammy Customer の `entity_id` 日 `customer_entity` テーブル。
* `subtotal`  – この列は、注文に対して顧客に請求された合計金額です
   * 「Throwback Bellbottons」と「V-Neck T シャツ」の 2 組は合計 94.85 ドルでした
* `created_at`  – この列は、各注文が作成された際のタイムスタンプを返します

## `sales\_flat\_order\_item ( or Sales\_order\_item`

（Commerce 2.0 以降の場合）

の単一の行に加えて `Sales\_flat\_order` テーブル、条件 `Sammy Customer` 注文を送信し、一意の各項目のその注文の行がに挿入されます [`sales\_flat\_order\_item` テーブル](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id`  – この列は、 `sales_flat_order_item` テーブル
   * `Sammy Customer`の注文により、このテーブルに 2 つの異なる製品が含まれていたため、この注文では 2 つの行が作成されました
* `name`  – この列は製品名です
* `product_id`  – この列は、この行が参照している製品の一意の ID です
   * 上記の最初の行は、 `product_id` = 205。これは、 `Throwback Bellbottoms` 持っている `entity_id` の 205 `catalog_product_entity` テーブル
* `order_id`  – この列は `entity_id` これらの特定の注文項目を含む注文の
   * 上記の行は両方とも、以下を含む `order_id` = 227 （両方とも注文の一部であるため） `Sammy Customer`、次を持つ `entity_id` = 227 `sales_flat_order` テーブル
* `qty_ordered`  – この列は、この特定の順序に含まれる製品の単位数です
   * `Sammy Customer`の注文には、次の 2 組が含まれています `Throwback Bellbottoms`
* `price`  – この列は、注文品目の 1 単位の価格です
   * この `subtotal` から `Sammy Customer`内のの順序 `sales_flat_order` 表は 94.85 で、これは 2 つのペアの合計です `Throwback Bellbottoms` 39.95 ドル各 1 ドル `V-Neck T-Shirt` 14.95 ドル。
