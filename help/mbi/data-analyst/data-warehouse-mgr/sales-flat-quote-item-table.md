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

この `quote_item` テーブル （`sales_flat_quote_item` M1 について）には、買い物かごに追加されたすべてのアイテムに関するレコードが含まれます。このレコードは、買い物かごが放棄されたか、購入に変換されたかに関係なく含まれます。 各行は、1 つの買い物かご項目を表します。 このテーブルの潜在的なサイズにより、Adobeでは、60 日を超える未変換の買い物かごがある場合など、特定の条件を満たした場合に、レコードを定期的に削除することをお勧めします。

>[!NOTE]
>
>履歴の放棄された買い物かごの分析は、からレコードを削除しない場合にのみ可能です `quote` および `quote_item` テーブル。 レコードを削除すると、データベースからまだ削除されていない買い物かごのみが表示されます。

## 共通ネイティブ列

| **列名** | **説明** |
|---|---|
| `base_price` | 商品が買い物かごに追加された時点での、商品の個々の単位の価格 [カタログ価格ルール、段階的な割引、特別価格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 税金、送料、買い物かごの割引が適用される前に適用されます。 これは、ストアのベース通貨で表されます。 |
| `created_at` | UTC でローカルに保存された、買い物かご項目の作成タイムスタンプ。 での設定に応じて [!DNL Commerce Intelligence]、このタイムスタンプはのレポートタイムゾーンに変換される場合があります [!DNL Commerce Intelligence] データベースのタイムゾーンとは異なる |
| `item_id` （PK） | テーブルの一意の識別子 |
| `name` | 注文項目のテキスト名 |
| `parent_item_id` | `Foreign key` これにより、シンプルな製品が親バンドルまたは設定可能な製品に関連付けられます。 に参加 `quote_item.item_id` 単純な製品に関連付けられた親製品属性を決定する。 親カート項目（バンドルまたは設定可能な製品タイプ）の場合、 `parent_item_id` 等しい `NULL` |
| `product_id` | `Foreign key` に関連付ける `catalog_product_entity` テーブル。 に参加 `catalog_product_entity.entity_id` 受注品目に関連付けられている製品属性を決定する手順は、次のとおりです。 |
| `product_type` | 買い物かごに追加された商品のタイプ。 潜在的 [製品タイプ](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) 含む：シンプル、設定可能、グループ化、仮想、バンドルおよびダウンロード可能 |
| `qty` | 特定の買い物かご品目に関して買い物かごに含まれる数量 |
| `quote_id` | `Foreign key` に関連付ける `quote` テーブル。 に参加 `quote.entity_id` 買い物かご項目に関連付けられている買い物かご属性を決定するには、次の手順に従います |
| `sku` | 買い物かご項目の一意の ID |
| `store_id` | に関連付けられた外部キー `store` テーブル。 に参加 `store.store_id` 買い物かご項目に関連付けられているCommerce ストア表示を特定するには |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Cart creation date` | 買い物かごの作成日に関連付けられたタイムスタンプ。 結合によって計算 `quote_item.quote_id` 対象： `quote.entity_id` およびを返します `created_at` timestamp |
| `Cart is active? (1/0)` | 買い物かごが顧客によって作成され、まだ注文に変換されていない場合に「1」を返すブール値フィールド。 変換された買い物かごまたは管理者が作成した買い物かごに対して「0」を返します。 結合によって計算 `quote_item.quote_id` 対象： `quote.entity_id` およびを返します `is_active` フィールド |
| `Cart item total value (qty * base_price)` | 買い物かごに項目が追加された時点における、次の後の項目の合計値 [カタログ価格ルール、段階的な割引、特別価格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) 税金、送料、買い物かごの割引が適用される前に適用されます。 乗じて計算 `qty` 基準： `base_price` |
| `Seconds since cart creation` | 買い物かごの作成日から現在までの経過時間。 結合によって計算 `quote_item.quote_id` 対象： `quote.entity_id` およびを返します `Seconds since cart creation` フィールド |
| `Store name` | 注文項目に関連付けられているCommerce ストアの名前。 結合によって計算 `sales_order_item.store_id` 対象： `store.store_id` およびを返します `name` フィールド |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **建設** |
|---|---|---|
| `Number of abandoned cart items` | 特定の「放棄」条件を満たす買い物かごに追加された品目の合計数量 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>フィルター：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x。ここで「x」は、買い物かごが作成されてからの経過時間（秒）を表します。この時間を超えると、買い物かごは放棄されたと見なされます |
| `Abandoned cart item value` | 特定の「放棄」条件を満たす買い物かごに関連付けられている合計売上高の合計 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>フィルター：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x。ここで「x」は、買い物かごが作成されてからの経過時間（秒）を表します。この時間を超えると、買い物かごは放棄されたと見なされます |

{style="table-layout:auto"}

## 外部キー結合パス

`catalog_product_entity`

* に参加 `catalog_product_entity` 買い物かご品目に関連付けられた製品属性を返す列を作成するテーブル。
   * パス： `quote_item.product_id` （多） => `catalog_product_entity.entity_id` （1）

`quote`

* に参加 `quote` 買い物かご項目に関連付けられた新しい買い物かごレベル列を作成するテーブル。
   * パス： `quote_item.quote_id` （多） => `quote.entity_id` （1）

`quote_item`

* に参加 `quote_item` 親設定可能またはバンドル SKU の詳細をシンプルな製品に関連付ける列を作成します。 [サポートに連絡する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) Data Warehouseマネージャで構築する場合は、これらの計算の設定に役立ちます。
   * パス： `quote_item.parent_item_id` （多） => `quote_item.item_id` （1）

`store`

* に参加 `store` 買い物かご項目に関連付けられたCommerceストアに関連する詳細を返す列を作成するテーブル。
   * パス： `quote_item.store_id` （多） => `store.store_id` （1）
