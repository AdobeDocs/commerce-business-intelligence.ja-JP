---
title: sales_order_item テーブル
description: sales_order_item テーブルの操作方法を説明します。
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# `sales_order_item` テーブル

The `sales_order_item` テーブル (`sales_flat_order_item` (M1) には、注文で購入されたすべての製品のレコードが含まれます。 各行は、 `sku` を注文に含めます。 特定ののの購入数量 `sku` は、 `qty_ordered` フィールドに入力します。

## 製品タイプ

The `sales_order_item` すべての詳細をキャプチャ [製品タイプ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 購入された の一般的な慣行 [!DNL Adobe Commerce] は、設定可能な製品（つまり、サイズ、色、その他の製品属性に従ってカスタマイズ可能な製品）を提供するために使用します。 設定可能な製品には独自の `sku`を使用すると、複数のシンプルな製品に関連付けることができます。シンプルな各製品は、一意の製品設定を表します。 参照： [製品の設定](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) を参照してください。

例えば、T シャツなどの設定可能な製品について考えてみましょう。 顧客がチェックアウトする際に、色とサイズを変更するオプションを選択します。 顧客が次の色を選択した場合： `blue`、および `small`その結果、などのシンプルな製品を購入することになります。 `t-shirt-blue-small` これは～の親産物に関係する `t-shirt`.

設定可能な製品が 1 つの注文に含まれると、 `sales_order_item` テーブル： 1 つは [単純](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku` そして 1 つは [設定可能](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) 親。 次の 2 つのレコード： `sales_order_item` テーブルは、次の結合を通じて相互に関連付けることができます。

* （シンプル） `sales_order_item.parent_item_id` => （設定可能） `sales_order_item.item_id`

したがって、製品の販売に関するレポートは、シンプルなレベルまたは設定可能なレベルで作成できます。 デフォルトでは、すべての標準 `order-item-level` の指標 [!DNL Commerce Intelligence] 単純な製品を除外するように設定され、 *のみ* 設定可能なバージョンに関するレポート。 これは、 `Ordered products we count` フィルターセット。 `parent_item_id` 次に該当 `NULL`.

## 共通列

| **列名** | **説明** |
|----|----|
| `base_price` | 販売時以降の製品の個々の単位の価格 [カタログ価格ルール、階層型割引、特別価格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) が適用され、税、送料、買い物かごの割引が適用される前に、が適用されます。 これは、ストアのベース通貨で表されます。 |
| `created_at` | 注文項目の作成タイムスタンプ（ローカルの UTC に保存）。 の設定に応じて、 [!DNL Commerce Intelligence]の場合、このタイムスタンプは、 [!DNL Commerce Intelligence] データベースのタイムゾーンと異なる |
| `item_id` (PK) | テーブルの一意の ID。 |
| `name` | 注文項目のテキスト名。 |
| `order_id` | `Foreign key` ～と関連している `sales_order` 表。 結合先 `sales_order.entity_id` ：受注品目に関連付けられている受注属性を判別します。 |
| `parent_item_id` | `Foreign key` シンプルな製品をその親バンドルまたは設定可能な製品に関連付けます。 結合先 `sales_order_item.item_id` を使用して、単純な製品に関連付けられた親製品属性を特定します。 親の注文品目（バンドルまたは設定可能な製品タイプ）の場合、 `parent_item_id` 次に該当 `NULL`. |
| `product_id` | `Foreign key` ～と関連している `catalog_product_entity` 表。 結合先 `catalog_product_entity.entity_id` を使用して、受注品目に関連付けられている製品属性を判別します。 |
| `product_type` | 販売された製品のタイプ。 潜在的な [製品タイプ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 含まれる機能：シンプル、設定可能、グループ化、仮想、バンドル、ダウンロード可能 |
| `qty_ordered` | 販売時に特定の注文品目の買い物かごに含まれる数量。 |
| `sku` | 購入された注文品目の一意の識別子。 |
| `store_id` | `Foreign key` ～と関連している `store` 表。 結合先 `store.store_id` をクリックして、注文項目に関連付けられたコマースストア表示を特定します。 |

{style="table-layout:auto"}

## 共通の計算列

| **列名** | **説明** |
|---|---|
| `Customer's email` | 注文をする顧客の電子メールアドレス。 結合によって計算 `sales_order_item.order_id` から `sales_order.entity_id` そして `customer_email` フィールドに入力します。 |
| `Customer's lifetime number of orders` | この顧客が行った注文の合計数。 結合によって計算 `sales_order_item.order_id` から `sales_order.entity_id` そして `Customer's lifetime number of orders` フィールドに入力します。 |
| `Customer's lifetime revenue` | この顧客が行ったすべての注文に関する売上高の合計。 結合によって計算 `sales_order_item.order_id` から `sales_order.entity_id` そして `Customer's lifetime revenue` フィールドに入力します。 |
| `Customer's order number` | この顧客の注文の順番のランク。 結合によって計算 `sales_order_item.order_id` から `sales_order.entity_id` そして `Customer's order number` フィールドに入力します。 |
| `Order item total value (quantity * price)` | 販売時以降の注文項目の合計値 [カタログ価格ルール、階層型割引、特別価格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) が適用され、税、送料、買い物かごの割引が適用される前に、が適用されます。 次の乗算で計算： `qty_ordered` によって `base_price`. |
| `Order's coupon_code` | 注文に適用されたクーポン。 結合によって計算 `sales_order_item.order_id` から `sales_order.entity_id` そして `coupon_code` フィールドに入力します。 |
| `Order's increment_id` | 注文の一意の ID。 結合によって計算 `sales_order_item.order_id` から `sales_order.entity_id` そして `increment_id` フィールドに入力します。 |
| `Order's status` | オーダーのステータス。 結合によって計算 `sales_order_item.order_id` から `sales_order.entity_id` そして `status` フィールドに入力します。 |
| `Store name` | 注文項目に関連付けられたコマースストアの名前。 結合によって計算 `sales_order_item.store_id` から `store.store_id` そして `name` フィールドに入力します。 |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **構築** |
|---|---|---|
| `Products ordered` | 販売時に買い物かごに含まれる製品の合計数量 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | カタログ価格ルール、階層割引、特別価格が適用され、税、送料、買い物かご割引が適用される前の販売時に買い物かごに含まれる製品の合計値 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` パスの結合

`catalog_product_entity`

* 結合先 `catalog_product_entity` 注文項目に関連付けられた製品属性を返す列を作成するテーブル。
   * パス： `sales_order_item.product_id` （多数） => `catalog_product_entity.entity_id` (1)

`sales_order`

* 結合先 `sales_order` オーダー項目に関連付けられた新しいオーダーレベルの列を作成するテーブル。
   * パス： `sales_order_item.order_id` （多数） => `sales_order.entity_id` (1)

`sales_order_item`

* 結合先 `sales_order_item` 親の設定可能な SKU またはバンドル SKU の詳細をシンプルな製品に関連付ける列を作成する場合。 [サポートへの問い合わせ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) を参照してください。
   * パス： `sales_order_item.parent_item_id` （多数） => `sales_order_item.item_id` (1)

`store`

* 結合先 `store` 注文項目に関連付けられたコマースストアに関連する詳細を返す列を作成するテーブル。
   * パス： `sales_order_item.store_id` （多数） => `store.store_id` (1)
