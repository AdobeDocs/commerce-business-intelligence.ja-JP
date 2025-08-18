---
title: sales_order_item テーブル
description: sales_order_item テーブルの操作方法を説明します。
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# `sales_order_item` テーブル

`sales_order_item` テーブル（M1 の `sales_flat_order_item`）には、注文で購入されたすべての製品のレコードが含まれています。 各行は、注文に含まれる一意の `sku` を表します。 特定の `sku` に対して購入された数量は、ほとんどの場合、`qty_ordered` フィールドで表されます。

## 製品タイプ

`sales_order_item` は、購入したすべての [ 製品タイプ ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) に関する詳細をキャプチャします。 [!DNL Adobe Commerce] の一般的な方法は、設定可能な製品、つまり、サイズ、色、その他の製品属性に応じてカスタマイズできる製品を提供することです。 設定可能な製品には独自の `sku` がありますが、複数の単純な製品に関連付けることができます。単純な製品はそれぞれ、一意の製品設定を表します。 詳しくは、[ 製品の設定 ](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) を参照してください。

例えば、設定可能な製品（T シャツなど）について考えてみます。 ユーザーはチェックアウト時に、カラーとサイズを変更するオプションを選択します。 顧客が `blue` の色と `small` のサイズを選択すると、`t-shirt-blue-small` の親製品に関連する `t-shirt` のような単純な製品が購入されます。

設定可能な商品が注文に含まれている場合、`sales_order_item` テーブルには、[simple](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) 行と `sku`configurable[ 親 ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) の 2 つの行が生成されます。 `sales_order_item` テーブルのこれらの 2 つのレコードは、次の結合によって相互に関連付けることができます。

* （シンプル） `sales_order_item.parent_item_id` => （設定可能） `sales_order_item.item_id`

したがって、製品の売上に関するレポートを単純なレベルまたは構成可能なレベルで作成することが可能になります。 デフォルトでは、`order-item-level` のすべての標準 [!DNL Commerce Intelligence] 指標は、単純な製品を除外するように設定され、設定可能なバージョンに関するレポート *のみ* を行います。 これは、`Ordered products we count` が `parent_item_id` 定されている条件でフィルタリングする `NULL` フィルターセットを通じて実現されます。

## 共通列

| **列名** | **説明** |
|----|----|
| `base_price` | カタログ価格ルール、階層割引、特別価格 [ が適用された後、税金、送料、買い物かごの割引が適用される前の ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 販売時の製品の個々の単位の価格。 これは、ストアのベース通貨で表されます。 |
| `created_at` | 注文項目の作成タイムスタンプ（UTC でローカルに保存）。 [!DNL Commerce Intelligence] での設定に応じて、このタイムスタンプはデータベースのタイムゾーンとは異な [!DNL Commerce Intelligence] レポートタイムゾーンに変換される場合があります。 |
| `item_id` （PK） | テーブルの一意の識別子。 |
| `name` | 注文項目のテキスト名。 |
| `order_id` | `Foreign key` テーブルに関連付けられた `sales_order`。 `sales_order.entity_id` に結合して、受注品目に関連付けられた受注属性を決定します。 |
| `parent_item_id` | シンプルな製品を親バンドルまたは設定可能な製品に関連付ける `Foreign key` ール。 `sales_order_item.item_id` に結合して、単純製品に関連付けられた親製品属性を決定します。 親注文品目（バンドルまたは設定可能な商品タイプ）の場合、`parent_item_id` は `NULL` です。 |
| `product_id` | `Foreign key` テーブルに関連付けられた `catalog_product_entity`。 `catalog_product_entity.entity_id` に結合して、注文品目に関連付けられた製品属性を決定します。 |
| `product_type` | 販売された商品のタイプ。 可能な [ 製品タイプ ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) には、シンプル、設定可能、グループ化、仮想、バンドル、ダウンロード可能が含まれます。 |
| `qty_ordered` | 販売時に特定の注文品目の買い物かごに含まれる数量。 |
| `sku` | 購入した注文品目の一意の ID。 |
| `store_id` | `Foreign key` テーブルに関連付けられた `store`。 `store.store_id` に結合して、注文項目に関連付けられているCommerce ストア表示を判断します。 |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Customer's email` | 注文を行う顧客の電子メールアドレス。 `sales_order_item.order_id` を `sales_order.entity_id` に結合し、`customer_email` フィールドを返すことによって計算されます。 |
| `Customer's lifetime number of orders` | この顧客が注文した注文の合計数。 `sales_order_item.order_id` を `sales_order.entity_id` に結合し、`Customer's lifetime number of orders` フィールドを返すことによって計算されます。 |
| `Customer's lifetime revenue` | この顧客が行ったすべての注文の売上高の合計。 `sales_order_item.order_id` を `sales_order.entity_id` に結合し、`Customer's lifetime revenue` フィールドを返すことによって計算されます。 |
| `Customer's order number` | この顧客の注文の順次オーダーランク。 `sales_order_item.order_id` を `sales_order.entity_id` に結合し、`Customer's order number` フィールドを返すことによって計算されます。 |
| `Order item total value (quantity * price)` | [ カタログ価格ルール、段階的割引、特別価格 ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) が適用された後、税金、送料、買い物かごの割引が適用される前の、販売時の注文項目の合計値。 `qty_ordered` に `base_price` を乗じて計算されます。 |
| `Order's coupon_code` | 注文に適用されるクーポン。 `sales_order_item.order_id` を `sales_order.entity_id` に結合し、`coupon_code` フィールドを返すことによって計算されます。 |
| `Order's increment_id` | 注文の一意の ID。 `sales_order_item.order_id` を `sales_order.entity_id` に結合し、`increment_id` フィールドを返すことによって計算されます。 |
| `Order's status` | 注文のステータス。 `sales_order_item.order_id` を `sales_order.entity_id` に結合し、`status` フィールドを返すことによって計算されます。 |
| `Store name` | 注文項目に関連付けられているCommerce ストアの名前。 `sales_order_item.store_id` を `store.store_id` に結合し、`name` フィールドを返すことによって計算されます。 |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **建設** |
|---|---|---|
| `Products ordered` | 販売時の買い物かごに含まれる製品の合計数量 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | カタログ価格ルール、階層割引、特別価格が適用された後、税金、送料、買い物かごの割引が適用される前の、販売時に買い物かごに含まれる製品の合計値 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` 結合パス

`catalog_product_entity`

* テーブルに結合 `catalog_product_entity` て、注文品目に関連付けられた製品属性を返す列を作成します。
   * パス：`sales_order_item.product_id` （多） => `catalog_product_entity.entity_id` （1）

`sales_order`

* テーブルに結合 `sales_order` て、注文項目に関連付けられた新しい注文レベルの列を作成します。
   * パス：`sales_order_item.order_id` （多） => `sales_order.entity_id` （1）

`sales_order_item`

* `sales_order_item` に結合して、親の設定可能またはバンドル SKU の詳細を単純な製品に関連付ける列を作成します。 Data Warehouse Manager で構築する場合は、これらの計算の設定について [ サポートにお問い合わせください ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
   * パス：`sales_order_item.parent_item_id` （多） => `sales_order_item.item_id` （1）

`store`

* テーブルに結合 `store` て、注文項目に関連付けられたCommerce ストアに関連する詳細を返す列を作成します。
   * パス：`sales_order_item.store_id` （多） => `store.store_id` （1）
