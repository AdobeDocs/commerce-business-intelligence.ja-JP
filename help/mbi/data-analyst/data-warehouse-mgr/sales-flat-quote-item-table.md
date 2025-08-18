---
title: quote_item テーブル
description: quote_item テーブルの使用方法を説明します。
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# quote_item 表

`quote_item` テーブル（M1 の `sales_flat_quote_item`）には、買い物かごに追加されたすべての商品に関するレコードが含まれています。このレコードは、買い物かごが放棄されたか購入に変換されたかに関係なく含まれます。 各行は、1 つの買い物かご項目を表します。 Adobeこのテーブルの潜在的なサイズのため、60 日を超える未変換の買い物かごがある場合など、特定の条件を満たした場合は、レコードを定期的に削除することをお勧めします。

>[!NOTE]
>
>履歴、放棄された買い物かごを分析することは、`quote` と `quote_item` のテーブルからレコードを削除しない場合にのみ可能です。 レコードを削除すると、データベースからまだ削除されていない買い物かごのみが表示されます。

## 共通ネイティブ列

| **列名** | **説明** |
|---|---|
| `base_price` | 商品が買い物かごに追加された際の、商品の個々の単位の価格。[ カタログ価格ルール、階層別の割引、特別価格 ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) が適用された後、税金、送料、買い物かごの割引が適用される前の価格。 これは、ストアのベース通貨で表されます。 |
| `created_at` | UTC でローカルに保存された、買い物かご項目の作成タイムスタンプ。 [!DNL Commerce Intelligence] での設定に応じて、このタイムスタンプはデータベースのタイムゾーンとは異な [!DNL Commerce Intelligence] レポートタイムゾーンに変換される場合があります |
| `item_id` （PK） | テーブルの一意の識別子 |
| `name` | 注文項目のテキスト名 |
| `parent_item_id` | シンプルな製品を親バンドルまたは設定可能な製品に関連付ける `Foreign key` ール。 `quote_item.item_id` に結合して、単純製品に関連付けられた親製品属性を決定します。 親カート項目（バンドルまたは設定可能な製品タイプ）の場合、`parent_item_id` は `NULL` です |
| `product_id` | `Foreign key` テーブルに関連付けられた `catalog_product_entity`。 `catalog_product_entity.entity_id` に結合して、注文品目に関連付けられた製品属性を決定します |
| `product_type` | 買い物かごに追加された商品のタイプ。 利用可能な [ 製品タイプ ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) には、シンプル、設定可能、グループ化、仮想、バンドル、ダウンロード可能などがあります |
| `qty` | 特定の買い物かご品目に関して買い物かごに含まれる数量 |
| `quote_id` | `Foreign key` テーブルに関連付けられた `quote`。 `quote.entity_id` に結合して、買い物かご項目に関連付けられた買い物かご属性を決定します |
| `sku` | 買い物かご項目の一意の ID |
| `store_id` | `store` テーブルに関連付けられている外部キー。 `store.store_id` に結合して、買い物かご項目に関連付けられているCommerce ストア表示を特定します |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Cart creation date` | 買い物かごの作成日に関連付けられたタイムスタンプ。 `quote_item.quote_id` を `quote.entity_id` に結合し、`created_at` タイムスタンプを返すことによって計算されます |
| `Cart is active? (1/0)` | 買い物かごが顧客によって作成され、まだ注文に変換されていない場合に「1」を返すブール値フィールド。 変換された買い物かごまたは管理者が作成した買い物かごに対して「0」を返します。 `quote_item.quote_id` を `quote.entity_id` に結合し、`is_active` フィールドを返すことによって計算されます |
| `Cart item total value (qty * base_price)` | [ カタログ価格ルール、階層割引、特別価格 ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) が適用された後、税金、送料、買い物かごの割引が適用される前の、買い物かごに項目が追加された際の項目の合計値。 `qty` に `base_price` を乗じて計算 |
| `Seconds since cart creation` | 買い物かごの作成日から現在までの経過時間。 `quote_item.quote_id` を `quote.entity_id` に結合し、`Seconds since cart creation` フィールドを返すことによって計算されます |
| `Store name` | 注文項目に関連付けられているCommerce ストアの名前。 `sales_order_item.store_id` を `store.store_id` に結合し、`name` フィールドを返すことによって計算されます |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **建設** |
|---|---|---|
| `Number of abandoned cart items` | 特定の「放棄」条件を満たす買い物かごに追加された品目の合計数量 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filters:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x。ここで「x」は、買い物かごが作成されてからの経過時間（秒単位）を表し、それ以降は買い物かごが放棄されたと見なされます。 |
| `Abandoned cart item value` | 特定の「放棄」条件を満たす買い物かごに関連付けられている合計売上高の合計 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filters:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x。ここで「x」は、買い物かごが作成されてからの経過時間（秒単位）を表し、それ以降は買い物かごが放棄されたと見なされます |

{style="table-layout:auto"}

## 外部キー結合パス

`catalog_product_entity`

* テーブルに結合 `catalog_product_entity` て、買い物かご品目に関連付けられた製品属性を返す列を作成します。
   * パス：`quote_item.product_id` （多） => `catalog_product_entity.entity_id` （1）

`quote`

* テーブルに結合 `quote` て、買い物かご項目に関連付けられた新しい買い物かごレベルの列を作成します。
   * パス：`quote_item.quote_id` （多） => `quote.entity_id` （1）

`quote_item`

* `quote_item` に結合して、親の設定可能またはバンドル SKU の詳細を単純な製品に関連付ける列を作成します。 Data Warehouse Manager で構築する場合は、これらの計算の設定について [ サポートにお問い合わせください ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
   * パス：`quote_item.parent_item_id` （多） => `quote_item.item_id` （1）

`store`

* テーブルに結合 `store` て、買い物かご項目に関連付けられたCommerce ストアに関連する詳細を返す列を作成します。
   * パス：`quote_item.store_id` （多） => `store.store_id` （1）
