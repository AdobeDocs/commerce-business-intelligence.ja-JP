---
title: sales_order_item テーブル
description: sales_order_item テーブルの操作方法を説明します。
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/oIuu3bNkmZMRrwa6V76fQPgKUWr4IsG3Madq46ar0Tk
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 889
ht-degree: 0%

---

# `sales_order_item` テーブル

`sales_order_item` テーブル （`sales_flat_order_item` on M1）には、注文で購入されたすべての製品のレコードが含まれています。 各行は、注文に含まれる一意の`sku`を表します。 特定の`sku`に対して購入されたユニットの数量は、最も多くの場合、`qty_ordered` フィールドで表されます。

## 製品タイプ

`sales_order_item`は、購入したすべての[製品タイプ &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types)の詳細をキャプチャします。 [!DNL Adobe Commerce]の一般的な方法は、設定可能な製品、つまり、サイズ、色、その他の製品属性に応じてカスタマイズできる製品を提供することです。 設定可能な製品には独自の`sku`がありますが、複数の単純な製品に関連付けることができます。各単純な製品は一意の製品設定を表します。 詳しくは、[製品の設定](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/)を参照してください。

例えば、T シャツのような設定可能な商品を考えてみましょう。 顧客がチェックアウトすると、色やサイズを変更するオプションが選択されます。 お客様が`blue`の色と`small`のサイズを選択した場合、親製品`t-shirt`に関連する`t-shirt-blue-small`のような単純な製品が購入されます。

設定可能な製品が注文に含まれる場合、2つの行が`sales_order_item` テーブルに生成されます。[simple](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku`の1行と[設定可能](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html)の親の1行。 `sales_order_item` テーブル内のこれら2つのレコードは、次の結合を通じて相互に関連付けることができます。

* （シンプル） `sales_order_item.parent_item_id` => （設定可能） `sales_order_item.item_id`

したがって、製品の販売を簡単なレベルまたは設定可能なレベルで報告することができます。 デフォルトでは、[!DNL Commerce Intelligence]内のすべての標準`order-item-level`指標は、シンプルな製品を除外するように設定され、設定可能なバージョンについて&#x200B;*のみ*&#x200B;のレポートが表示されます。 これは、`parent_item_id`が`NULL`の条件でフィルターを実行する`Ordered products we count` フィルターセットを通じて実行されます。

## 共通の列

| **列名** | **説明** |
|----|----|
| `base_price` | 販売時の製品の個々のユニットの価格[&#x200B; カタログ価格ルール、階層割引、特別価格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)が適用され、税金、送料、カートの割引が適用される前に適用されます。 これは、ストアの基本通貨で表されます。 |
| `created_at` | 注文項目の作成タイムスタンプ。ローカルにUTCで保存されます。 [!DNL Commerce Intelligence]の設定に応じて、このタイムスタンプは、データベースのタイムゾーンとは異なる[!DNL Commerce Intelligence]のレポートタイムゾーンに変換される場合があります。 |
| `item_id` （PK） | テーブルの一意のID。 |
| `name` | 注文項目のテキスト名。 |
| `order_id` | `Foreign key`が`sales_order` テーブルに関連付けられています。 `sales_order.entity_id`に結合して、注文項目に関連付けられている注文属性を決定します。 |
| `parent_item_id` | 単純な製品を親バンドルまたは設定可能な製品に関連付ける`Foreign key`。 `sales_order_item.item_id`に参加して、単純な製品に関連付けられている親製品属性を決定します。 親の注文項目（バンドルまたは設定可能な製品タイプ）の場合、`parent_item_id`は`NULL`です。 |
| `product_id` | `Foreign key`が`catalog_product_entity` テーブルに関連付けられています。 `catalog_product_entity.entity_id`に結合して、注文項目に関連付けられている製品属性を決定します。 |
| `product_type` | 販売された商品のタイプ。 潜在的な[製品タイプ &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types)には、シンプル、設定可能、グループ化、仮想、バンドル、ダウンロード可能などがあります。 |
| `qty_ordered` | 販売時に特定の注文品目のカートに含まれる単位の数量。 |
| `sku` | 購入された注文項目の一意のID。 |
| `store_id` | `Foreign key`が`store` テーブルに関連付けられています。 `store.store_id`に結合して、注文項目に関連付けられているCommerce ストアビューを決定します。 |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Customer's email` | 注文する顧客の電子メールアドレス。 `sales_order_item.order_id`を`sales_order.entity_id`に結合し、`customer_email` フィールドを返すことで計算されます。 |
| `Customer's lifetime number of orders` | この顧客による注文の合計数です。 `sales_order_item.order_id`を`sales_order.entity_id`に結合し、`Customer's lifetime number of orders` フィールドを返すことで計算されます。 |
| `Customer's lifetime revenue` | この顧客が行ったすべての注文の収益の合計。 `sales_order_item.order_id`を`sales_order.entity_id`に結合し、`Customer's lifetime revenue` フィールドを返すことで計算されます。 |
| `Customer's order number` | この顧客の注文に対する順序付き注文ランク。 `sales_order_item.order_id`を`sales_order.entity_id`に結合し、`Customer's order number` フィールドを返すことで計算されます。 |
| `Order item total value (quantity * price)` | 販売時の注文商品の合計金額（[&#x200B; カタログ価格ルール、階層割引、特別価格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)以降）が適用され、税金、送料、カートの割引が適用される前に適用されます。 `qty_ordered`に`base_price`を掛けて計算します。 |
| `Order's coupon_code` | 注文に適用されたクーポン。 `sales_order_item.order_id`を`sales_order.entity_id`に結合し、`coupon_code` フィールドを返すことで計算されます。 |
| `Order's increment_id` | 注文の一意のID。 `sales_order_item.order_id`を`sales_order.entity_id`に結合し、`increment_id` フィールドを返すことで計算されます。 |
| `Order's status` | 注文のステータス。 `sales_order_item.order_id`を`sales_order.entity_id`に結合し、`status` フィールドを返すことで計算されます。 |
| `Store name` | 注文項目に関連付けられているCommerce ストアの名前。 `sales_order_item.store_id`を`store.store_id`に結合し、`name` フィールドを返すことで計算されます。 |

{style="table-layout:auto"}

## 共通指標

| **指標の名前** | **説明** | **建設** |
|---|---|---|
| `Products ordered` | 販売時にカートに含まれる製品の合計数量 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | カタログ価格ルール、階層割引、特別価格が適用され、税金、送料、カート割引が適用される前に、販売時にカートに含まれる商品の合計金額 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key`個の参加パス

`catalog_product_entity`

* `catalog_product_entity` テーブルに結合して、注文項目に関連付けられた製品属性を返す列を作成します。
   * パス：`sales_order_item.product_id` （多数） => `catalog_product_entity.entity_id` （1つ）

`sales_order`

* `sales_order` テーブルに結合して、注文項目に関連付けられた新しい注文レベルの列を作成します。
   * パス：`sales_order_item.order_id` （多数） => `sales_order.entity_id` （1つ）

`sales_order_item`

* `sales_order_item`に結合して、親の設定可能なSKUまたはバンドル SKUの詳細をシンプルな製品に関連付ける列を作成します。 Data Warehouse Managerでビルドする場合は、[&#x200B; サポート &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)に連絡して、これらの計算の設定についてサポートを受けてください。
   * パス：`sales_order_item.parent_item_id` （多数） => `sales_order_item.item_id` （1つ）

`store`

* `store` テーブルに結合して、注文項目に関連付けられているCommerce ストアに関連する詳細を返す列を作成します。
   * パス：`sales_order_item.store_id` （多数） => `store.store_id` （1つ）
