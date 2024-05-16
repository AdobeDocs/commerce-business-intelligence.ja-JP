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

この `sales_order_item` テーブル （`sales_flat_order_item` m1 では）には、注文で購入されたすべての製品のレコードが含まれています。 各行は一意のを表します `sku` 注文に含まれる。 特定の品目に対して購入された数量 `sku` ほとんどの場合、は `qty_ordered` フィールド。

## 製品タイプ

この `sales_order_item` すべてのの詳細を取得します [製品タイプ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) それは購入されました。 ～でよく行われている習慣 [!DNL Adobe Commerce] は、設定可能な製品、つまり、サイズ、色、その他の製品属性に応じてカスタマイズできる製品を提供することです。 設定可能な製品には独自の機能があります `sku`は複数のシンプルな製品に関連付けることができます。シンプルな製品はそれぞれ、一意の製品設定を表します。 こちらを参照してください [製品の設定](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) を参照してください。

例えば、設定可能な製品（T シャツなど）について考えてみます。 ユーザーはチェックアウト時に、カラーとサイズを変更するオプションを選択します。 お客様がのカラーを選択した場合 `blue`、およびサイズ `small`最終的に、次のようなシンプルな製品を購入することになります。 `t-shirt-blue-small` 親商品に関連する `t-shirt`.

設定可能な製品が注文に含まれている場合、には 2 行が生成されます。 `sales_order_item` テーブル：に対するもの [シンプル](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku` と 1 つ [設定可能](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) 親。 これら 2 つのレコード `sales_order_item` テーブルは、次の結合を通じて相互に関連付けることができます。

* （シンプル） `sales_order_item.parent_item_id` => （設定可能） `sales_order_item.item_id`

したがって、製品の売上に関するレポートを単純なレベルまたは構成可能なレベルで作成することが可能になります。 デフォルトでは、すべての標準 `order-item-level` の指標 [!DNL Commerce Intelligence] 単純製品を除外するように設定される *のみ* 設定可能なバージョンのレポート。 これは、次の方法で実現できます `Ordered products we count` フィルターセット。条件に基づいてフィルターします。 `parent_item_id` 等しい `NULL`.

## 共通列

| **列名** | **説明** |
|----|----|
| `base_price` | 販売時の商品の後の個々の単位の価格 [カタログ価格ルール、段階的な割引、特別価格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 税金、送料、買い物かごの割引が適用される前に適用されます。 これは、ストアのベース通貨で表されます。 |
| `created_at` | 注文項目の作成タイムスタンプ（UTC でローカルに保存）。 での設定に応じて [!DNL Commerce Intelligence]、このタイムスタンプはのレポートタイムゾーンに変換される場合があります [!DNL Commerce Intelligence] これは、データベースのタイムゾーンとは異なります。 |
| `item_id` （PK） | テーブルの一意の識別子。 |
| `name` | 注文項目のテキスト名。 |
| `order_id` | `Foreign key` に関連付ける `sales_order` テーブル。 に参加 `sales_order.entity_id` 受注品目に関連付けられている受注属性を決定する手順は、次のとおりです。 |
| `parent_item_id` | `Foreign key` これにより、シンプルな製品が親バンドルまたは設定可能な製品に関連付けられます。 に参加 `sales_order_item.item_id` 単純な製品に関連付けられた親製品属性を決定する。 親注文項目（バンドルまたは設定可能な商品タイプ）の場合、 `parent_item_id` 等しい `NULL`. |
| `product_id` | `Foreign key` に関連付ける `catalog_product_entity` テーブル。 に参加 `catalog_product_entity.entity_id` 受注品目に関連付けられている製品属性を決定する手順は、次のとおりです。 |
| `product_type` | 販売された商品のタイプ。 潜在的 [製品タイプ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) これには、シンプル、設定可能、グループ化、仮想、バンドル、ダウンロード可能が含まれます。 |
| `qty_ordered` | 販売時に特定の注文品目の買い物かごに含まれる数量。 |
| `sku` | 購入した注文品目の一意の ID。 |
| `store_id` | `Foreign key` に関連付ける `store` テーブル。 に参加 `store.store_id` 注文項目に関連付けられているCommerce ストア表示を特定します。 |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Customer's email` | 注文を行う顧客の電子メールアドレス。 結合によって計算 `sales_order_item.order_id` 対象： `sales_order.entity_id` およびを返します `customer_email` フィールド。 |
| `Customer's lifetime number of orders` | この顧客が注文した注文の合計数。 結合によって計算 `sales_order_item.order_id` 対象： `sales_order.entity_id` およびを返します `Customer's lifetime number of orders` フィールド。 |
| `Customer's lifetime revenue` | この顧客が行ったすべての注文の売上高の合計。 結合によって計算 `sales_order_item.order_id` 対象： `sales_order.entity_id` およびを返します `Customer's lifetime revenue` フィールド。 |
| `Customer's order number` | この顧客の注文の順次オーダーランク。 結合によって計算 `sales_order_item.order_id` 対象： `sales_order.entity_id` およびを返します `Customer's order number` フィールド。 |
| `Order item total value (quantity * price)` | 販売時の注文項目の後の合計値 [カタログ価格ルール、段階的な割引、特別価格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 税金、送料、買い物かごの割引が適用される前に適用されます。 乗じて計算 `qty_ordered` 基準： `base_price`. |
| `Order's coupon_code` | 注文に適用されるクーポン。 結合によって計算 `sales_order_item.order_id` 対象： `sales_order.entity_id` およびを返します `coupon_code` フィールド。 |
| `Order's increment_id` | 注文の一意の ID。 結合によって計算 `sales_order_item.order_id` 対象： `sales_order.entity_id` およびを返します `increment_id` フィールド。 |
| `Order's status` | 注文のステータス。 結合によって計算 `sales_order_item.order_id` 対象： `sales_order.entity_id` およびを返します `status` フィールド。 |
| `Store name` | 注文項目に関連付けられているCommerce ストアの名前。 結合によって計算 `sales_order_item.store_id` 対象： `store.store_id` およびを返します `name` フィールド。 |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **建設** |
|---|---|---|
| `Products ordered` | 販売時の買い物かごに含まれる製品の合計数量 | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | カタログ価格ルール、階層割引、特別価格が適用された後、税金、送料、買い物かごの割引が適用される前の、販売時に買い物かごに含まれる製品の合計値 | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` パスの結合

`catalog_product_entity`

* に参加 `catalog_product_entity` 受注品目に関連付けられた製品属性を戻す列を作成する表。
   * パス： `sales_order_item.product_id` （多） => `catalog_product_entity.entity_id` （1）

`sales_order`

* に参加 `sales_order` 受注品目に関連付けられた新規受注レベル列を作成する表。
   * パス： `sales_order_item.order_id` （多） => `sales_order.entity_id` （1）

`sales_order_item`

* に参加 `sales_order_item` 親設定可能またはバンドル SKU の詳細をシンプルな製品に関連付ける列を作成します。 [サポートに連絡する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) Data Warehouseマネージャで構築する場合は、これらの計算の設定に役立ちます。
   * パス： `sales_order_item.parent_item_id` （多） => `sales_order_item.item_id` （1）

`store`

* に参加 `store` 注文項目に関連付けられたCommerce ストアに関連する詳細を返す列を作成するテーブル。
   * パス： `sales_order_item.store_id` （多） => `store.store_id` （1）
