---
title: 見積もりテーブル
description: 見積もりテーブルの操作方法を説明します。
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# 見積もりテーブル

`quote` テーブル（M1 の `sales_flat_quote`）には、放棄されたか購入に変換されたかに関わらず、ストアで作成されたすべての買い物かごに関するレコードが含まれています。 各行は 1 つの買い物かごを表します。 このテーブルの潜在的なサイズにより、Adobeでは、60 日を超える未変換の買い物かごがある場合など、特定の条件を満たした場合に、レコードを定期的に削除することをお勧めします。

>[!NOTE]
>
>履歴の放棄された買い物かごを分析することは、`quote` テーブルからレコードを削除しない場合にのみ可能です。 レコードを削除すると、データベースからまだ削除されていない買い物かごのみが表示されます。

## 共通ネイティブ列

| **列名** | **説明** |
|---|---|
| `base_currency_code` | `base_*` のフィールドで取得されるすべての値の通貨（`base_grand_total`、`base_subtotal` など）。 これは通常、Commerce ストアのデフォルト通貨を反映します |
| `base_grand_total` | すべての税金、送料、割引が適用された後、買い物かごに対して顧客に見積もられた最終価格。 正確な計算はカスタマイズ可能ですが、通常、`base_grand_total` は `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` として計算されます |
| `base_subtotal` | 買い物かごに含まれるすべての品目の総商品価値。 税金、送料、割引などは含まれません |
| `created_at` | UTC でローカルに保存された、買い物かごの作成タイムスタンプ。 [!DNL Commerce Intelligence] での設定に応じて、このタイムスタンプはデータベースのタイムゾーンとは異な [!DNL Commerce Intelligence] レポートタイムゾーンに変換される場合があります |
| `customer_email` | 買い物かごを作成した顧客のメールアドレス |
| `customer_id` | 顧客が登録されている場合、`customer_entity` テーブルに関連付けられた `Foreign key` ール。 `customer_entity.entity_id` に結合して、買い物かごを作成したユーザーに関連付けられた顧客属性を決定します。 ゲストのチェックアウトで買い物かごが作成された場合、このフィールドは `NULL` になります |
| `entity_id` （PK） | テーブルの一意の ID。Commerce インスタンス内の他のテーブルへの結合で一般的に使用されます |
| `is_active` | 買い物かごが顧客によって作成され、まだ注文に変換されていない場合に「1」を返すブール値フィールド。 変換された買い物かごまたは管理者を通じて作成された買い物かごに対して「0」を返します |
| `items_qty` | 買い物かごに含まれているすべての品目の合計数量の合計 |
| `reserved_order_id` | `sales_order` テーブルに関連付けられた `Foreign key`。 `sales_order.increment_id` に結合して、コンバート済み買い物かごに関連付けられている注文の詳細を判断します。 変換された注文に関連付けられていない買い物かごの場合、`reserved_order_id` は `NULL` のままになります |
| `store_id` | `store` テーブルに関連付けられた `Foreign key`。 `store` に参加します。買い物かごに関連付けられているCommerce ストア表示を確認する `store_id` 法 |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Order date` | コンバート済み買い物かごの注文作成日を反映するタイムスタンプ。 `quote.reserved_order_id` を `sales_order.increment_id` に結合し、`sales_order.created_at` フィールドを返すことによって計算されます |
| `Seconds between cart creation and order` | 買い物かごの作成と注文の作成の間の経過時間。 `Order date` から `created_at` を引いて計算され、秒数の整数で返されます |
| `Seconds since cart creation` | 買い物かごの作成日から現在までの経過時間。 クエリの実行時にサーバーのタイムスタンプから `created_at` を引いて計算され、秒数の整数で返されます。 買い物かごの年齢を識別するために最も一般的に使用される |
| `Store name` | この注文に関連付けられたCommerce ストアの名前。 `quote.store_id` を `store.store_id` に結合し、`name` フィールドを返すことによって計算されます |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **建設** |
|---|---|---|
| `Number of abandoned carts` | 特定の「放棄」条件を満たす買い物かごの数 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>Filters:<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x。ここで「x」は、買い物かごが作成されてからの経過時間（秒）を表し、それ以降は買い物かごが放棄されたと見なされます。 |
| `Avg time to cart conversion` | コンバート済み買い物かごの作成から注文の作成までの平均時間 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 売上高が `base_grand_total` ールフィールドとして定義されている、放棄された買い物かごの潜在的な売上高の合計 | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>Filters:<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x。ここで「x」は、買い物かごが作成されてからの経過時間（秒）を表し、それ以降は買い物かごが放棄されたと見なされます。 |

{style="table-layout:auto"}

## 外部キー結合パス

`customer_entity`

* テーブルに結合 `customer_entity` て、買い物かごを作成した顧客に関連付けられた、新しい顧客レベルの列を作成します。
   * パス：`quote.customer_id` （多） => `customer_entity.entity_id` （1）

`sales_order`

* テーブルに結合 `sales_order` て、変換済みの買い物かごに関連付けられた注文の詳細を返す列を作成します。
   * パス：`quote.reserved_order_id` （多） => `sales_order.increment_id` （1）

`store`

* テーブルに結合 `store` て、買い物かごに関連付けられたCommerce ストアに関連する詳細を返す列を作成します。
   * パス：`quote.store_id` （多） => `store.store_id` （1）
