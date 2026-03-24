---
title: quote_item テーブル
description: quote_item テーブルの操作方法について説明します。
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/wLNm1g1L6-0Ded-bZT991KvJi3dVO6zA4i2qftiX2J0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
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
source-wordcount: 646
ht-degree: 0%

---

# quote_item Table

`quote_item` テーブル （`sales_flat_quote_item` on M1）には、買い物かごに追加されたすべてのアイテムに関するレコードが含まれています（買い物かごが放棄されたか、購入に変換されたか）。 各行は、1つの買い物かごアイテムを表します。 この表のサイズが大きくなる可能性があるため、Adobeでは、60日を超える未変換のカートがある場合など、特定の条件を満たす場合は、レコードを定期的に削除することをお勧めします。

>[!NOTE]
>
>過去のカートを分析することは、`quote`および`quote_item` テーブルからレコードを削除しない場合にのみ可能です。 レコードを削除すると、まだデータベースから削除されていないカートのみが表示されます。

## 共通のネイティブ列

| **列名** | **説明** |
|---|---|
| `base_price` | 商品がカートに追加された時点での商品の個々の単位の価格で、[&#x200B; カタログ価格ルール、階層割引、特別価格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)が適用され、税金、送料、カートの割引が適用される前に適用されます。 これは、ストアの基本通貨で表されます。 |
| `created_at` | 買い物かごアイテムの作成タイムスタンプ。ローカルでUTCに保存されます。 [!DNL Commerce Intelligence]の設定に応じて、このタイムスタンプは、データベースのタイムゾーンとは異なる[!DNL Commerce Intelligence]のレポートタイムゾーンに変換される場合があります |
| `item_id` （PK） | テーブルの一意のID |
| `name` | 注文項目のテキスト名 |
| `parent_item_id` | 単純な製品を親バンドルまたは設定可能な製品に関連付ける`Foreign key`。 `quote_item.item_id`に参加して、単純な製品に関連付けられている親製品属性を決定します。 親カート項目（バンドルまたは設定可能な製品タイプ）の場合、`parent_item_id`は`NULL`です |
| `product_id` | `Foreign key`が`catalog_product_entity` テーブルに関連付けられています。 `catalog_product_entity.entity_id`に結合して、注文項目に関連付けられている製品属性を決定します |
| `product_type` | カートに追加された商品のタイプ。 潜在的な[製品タイプ &#x200B;](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types)には、シンプル、設定可能、グループ化、仮想、バンドル、ダウンロード可能などがあります |
| `qty` | 特定の買い物かご品目の買い物かごに含まれる単位の数量 |
| `quote_id` | `Foreign key`が`quote` テーブルに関連付けられています。 `quote.entity_id`に参加して、買い物かごアイテムに関連付けられている買い物かご属性を決定します |
| `sku` | カート項目の一意のID |
| `store_id` | `store` テーブルに関連付けられている外部キー。 `store.store_id`に結合して、買い物かごアイテムに関連付けられているCommerce ストアビューを特定します |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Cart creation date` | カート作成日に関連付けられたタイムスタンプ。 `quote_item.quote_id`を`quote.entity_id`に結合し、`created_at` タイムスタンプを返すことによって計算されます |
| `Cart is active? (1/0)` | 買い物かごが顧客によって作成され、注文に変換されていない場合に「1」を返すブール型フィールド。 変換されたカート、または管理者を通じて作成されたカートの場合は「0」を返します。 `quote_item.quote_id`を`quote.entity_id`に結合し、`is_active` フィールドを返すことによって計算されます |
| `Cart item total value (qty * base_price)` | 商品がカートに追加された時点での商品の合計金額は、[&#x200B; カタログ価格ルール、階層割引、特別価格](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html)が適用された後、税金、送料、カートの割引が適用される前に計算されます。 `qty`に`base_price`を掛けて計算しました |
| `Seconds since cart creation` | カートの作成日から現在までの経過時間。 `quote_item.quote_id`を`quote.entity_id`に結合し、`Seconds since cart creation` フィールドを返すことによって計算されます |
| `Store name` | 注文項目に関連付けられているCommerce ストアの名前。 `sales_order_item.store_id`を`store.store_id`に結合し、`name` フィールドを返すことによって計算されます |

{style="table-layout:auto"}

## 共通指標

| **指標の名前** | **説明** | **建設** |
|---|---|---|
| `Number of abandoned cart items` | 特定の「放棄」条件を満たすカートに追加された商品の合計数量 | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br> フィルター：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x。ここで、「x」は、買い物かごが放棄されたと見なされるまでの経過時間（秒単位）に対応します |
| `Abandoned cart item value` | 特定の「放棄」条件を満たすカートに関連する総売上の合計 | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br> フィルター：<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x。ここで、「x」は、買い物かごが放棄されたと見なされるまでの経過時間（秒単位）に対応します |

{style="table-layout:auto"}

## 外部キー結合パス

`catalog_product_entity`

* `catalog_product_entity` テーブルに結合して、買い物かご項目に関連付けられた製品属性を返す列を作成します。
   * パス：`quote_item.product_id` （多数） => `catalog_product_entity.entity_id` （1つ）

`quote`

* `quote` テーブルに結合して、買い物かごアイテムに関連付けられた新しい買い物かごレベルの列を作成します。
   * パス：`quote_item.quote_id` （多数） => `quote.entity_id` （1つ）

`quote_item`

* `quote_item`に結合して、親の設定可能なSKUまたはバンドル SKUの詳細をシンプルな製品に関連付ける列を作成します。 Data Warehouse Managerでビルドする場合は、[&#x200B; サポート &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)に連絡して、これらの計算の設定についてサポートを受けてください。
   * パス：`quote_item.parent_item_id` （多数） => `quote_item.item_id` （1つ）

`store`

* `store` テーブルに結合して、買い物かご商品に関連付けられているCommerce ストアに関連する詳細を返す列を作成します。
   * パス：`quote_item.store_id` （多数） => `store.store_id` （1つ）
