---
title: quote_item テーブル
description: quote_item テーブルの操作方法を説明します。
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# quote_item テーブル

The `quote_item` テーブル (`sales_flat_quote_item` (M1) には、買い物かごに追加された各品目のレコードが含まれます。買い物かごが破棄されたか、購入に変換されたかに関わらずです。 各行は 1 つの買い物かご項目を表します。 このテーブルの潜在的なサイズにより、Adobeでは、60 日を超える未変換の買い物かごがある場合など、特定の条件を満たした場合に、レコードを定期的に削除することをお勧めします。

>[!NOTE]
>
>履歴の放棄された買い物かごの分析は、 `quote` および `quote_item` 表。 レコードを削除した場合は、データベースからまだ削除されていない買い物かごのみを表示できます。

## 共通のネイティブ列

| **列名** | **説明** |
|---|---|
| `base_price` | 品目が買い物かごに追加された時点での商品の個々の単位の価格（後） [カタログ価格ルール、階層型割引、特別価格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) が適用され、税、送料、買い物かごの割引が適用される前に、が適用されます。 これは、ストアのベース通貨で表されます。 |
| `created_at` | 買い物かご項目の作成タイムスタンプ（UTC でローカルに保存）。 の設定に応じて、 [!DNL Commerce Intelligence]の場合、このタイムスタンプは、 [!DNL Commerce Intelligence] データベースのタイムゾーンと異なる |
| `item_id` (PK) | テーブルの一意の ID |
| `name` | 注文項目のテキスト名 |
| `parent_item_id` | `Foreign key` シンプルな製品をその親バンドルまたは設定可能な製品に関連付けます。 結合先 `quote_item.item_id` を使用して、単純な製品に関連付けられた親製品属性を特定します。 親買い物かごの品目（つまり、バンドルまたは設定可能な製品タイプ）の場合、 `parent_item_id` 次に該当 `NULL` |
| `product_id` | `Foreign key` ～と関連している `catalog_product_entity` 表。 結合先 `catalog_product_entity.entity_id` 注文品目に関連付けられた製品属性を決定するには |
| `product_type` | 買い物かごに追加された商品のタイプ。 潜在的な [製品タイプ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 以下を含む：シンプル、設定可能、グループ化、仮想、バンドル、ダウンロード可能 |
| `qty` | 特定の買い物かご品目の買い物かごに含まれる数量 |
| `quote_id` | `Foreign key` ～と関連している `quote` 表。 結合先 `quote.entity_id` 買い物かご項目に関連付けられた買い物かご属性を特定するには |
| `sku` | 買い物かご項目の一意の ID |
| `store_id` | に関連付けられた外部キー `store` 表。 結合先 `store.store_id` 買い物かご項目に関連付けられているコマースストア表示を特定するには |

{style="table-layout:auto"}

## 共通の計算列

| **列名** | **説明** |
|---|---|
| `Cart creation date` | 買い物かごの作成日に関連付けられたタイムスタンプ。 結合によって計算 `quote_item.quote_id` から `quote.entity_id` そして `created_at` timestamp |
| `Cart is active? (1/0)` | 買い物かごが顧客によって作成され、まだ注文に変換されていない場合に「1」を返すブール値フィールド。 コンバージョンされた買い物かごに対しては「0」、管理者が作成した買い物かごに対しては「0」を返します。 結合によって計算 `quote_item.quote_id` から `quote.entity_id` そして `is_active` フィールド |
| `Cart item total value (qty * base_price)` | 品目が買い物かごに追加された時点での、買い物かごに追加された後の品目の合計値 [カタログ価格ルール、階層型割引、特別価格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) が適用され、税、送料、買い物かごの割引が適用される前に、が適用されます。 次の乗算で計算： `qty` によって `base_price` |
| `Seconds since cart creation` | 買い物かごの作成日から今までの経過時間。 結合によって計算 `quote_item.quote_id` から `quote.entity_id` そして `Seconds since cart creation` フィールド |
| `Store name` | 注文項目に関連付けられたコマースストアの名前。 結合によって計算 `sales_order_item.store_id` から `store.store_id` そして `name` フィールド |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **構築** |
|---|---|---|
| `Number of abandoned cart items` | 特定の「放棄」条件を満たす買い物かごに追加された品目の合計数 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>フィルター：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x(「x」は、買い物かごが破棄されたと見なされる、買い物かごが作成されてからの経過時間（秒）) です。 |
| `Abandoned cart item value` | 特定の「放棄」条件を満たす買い物かごに関連付けられた合計売上高の合計 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>フィルター：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x(「x」は、買い物かごが破棄されたと見なされる、買い物かごが作成されてからの経過時間（秒）) です。 |

{style="table-layout:auto"}

## 外部キー結合パス

`catalog_product_entity`

* 結合先 `catalog_product_entity` 買い物かご項目に関連付けられた製品属性を返す列を作成するテーブル。
   * パス： `quote_item.product_id` （多数） => `catalog_product_entity.entity_id` (1)

`quote`

* 結合先 `quote` 買い物かご項目に関連付けられた、新しい買い物かごレベルの列を作成するテーブル。
   * パス： `quote_item.quote_id` （多数） => `quote.entity_id` (1)

`quote_item`

* 結合先 `quote_item` 親の設定可能な SKU またはバンドル SKU の詳細をシンプルな製品に関連付ける列を作成する場合。 [サポートへの問い合わせ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) を参照してください。
   * パス： `quote_item.parent_item_id` （多数） => `quote_item.item_id` (1)

`store`

* 結合先 `store` 買い物かご項目に関連付けられたコマースストアに関連する詳細を返す列を作成するテーブル。
   * パス： `quote_item.store_id` （多数） => `store.store_id` (1)
