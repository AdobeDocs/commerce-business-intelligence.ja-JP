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

この `quote` テーブル （`sales_flat_quote` m1 について）には、放棄されたか購入に変換されたかに関わらず、ストアで作成されたすべての買い物かごに関するレコードが含まれます。 各行は 1 つの買い物かごを表します。 このテーブルの潜在的なサイズにより、Adobeでは、60 日を超える未変換の買い物かごがある場合など、特定の条件を満たした場合に、レコードを定期的に削除することをお勧めします。

>[!NOTE]
>
>履歴の放棄された買い物かごの分析は、からレコードを削除しない場合にのみ可能です `quote` テーブル。 レコードを削除すると、データベースからまだ削除されていない買い物かごのみが表示されます。

## 共通ネイティブ列

| **列名** | **説明** |
|---|---|
| `base_currency_code` | で取得されるすべての値の通貨 `base_*` フィールド（つまり、 `base_grand_total`, `base_subtotal`など）。 これは通常、Commerce ストアのデフォルト通貨を反映します |
| `base_grand_total` | すべての税金、送料、割引が適用された後、買い物かごに対して顧客に見積もられた最終価格。 正確な計算はカスタマイズできますが、一般的には `base_grand_total` 次のように計算されます `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | 買い物かごに含まれるすべての品目の総商品価値。 税金、送料、割引などは含まれません |
| `created_at` | UTC でローカルに保存された、買い物かごの作成タイムスタンプ。 での設定に応じて [!DNL Commerce Intelligence]、このタイムスタンプはのレポートタイムゾーンに変換される場合があります [!DNL Commerce Intelligence] データベースのタイムゾーンとは異なる |
| `customer_email` | 買い物かごを作成した顧客のメールアドレス |
| `customer_id` | `Foreign key` に関連付ける `customer_entity` 表（顧客が登録されている場合） に参加 `customer_entity.entity_id` 買い物かごを作成したユーザーに関連付けられている顧客属性を決定します。 ゲストのチェックアウトで買い物かごが作成された場合、このフィールドは `NULL` |
| `entity_id` （PK） | テーブルの一意の ID。Commerce インスタンス内の他のテーブルへの結合で一般的に使用されます |
| `is_active` | 買い物かごが顧客によって作成され、まだ注文に変換されていない場合に「1」を返すブール値フィールド。 変換された買い物かごまたは管理者を通じて作成された買い物かごに対して「0」を返します |
| `items_qty` | 買い物かごに含まれているすべての品目の合計数量の合計 |
| `reserved_order_id` | `Foreign key` に関連付ける `sales_order` テーブル。 に参加 `sales_order.increment_id` 変換済みの買い物かごに関連付けられている注文の詳細を判断する場合。 変換された注文に関連付けられていない買い物かごの場合、 `reserved_order_id` 残余 `NULL` |
| `store_id` | `Foreign key` に関連付ける `store` テーブル。 に参加 `store`.`store_id` 買い物かごに関連付けられているCommerce ストア表示を特定するには |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Order date` | コンバート済み買い物かごの注文作成日を反映するタイムスタンプ。 結合によって計算 `quote.reserved_order_id` 対象： `sales_order.increment_id` およびを返します `sales_order.created_at` フィールド |
| `Seconds between cart creation and order` | 買い物かごの作成と注文の作成の間の経過時間。 引いて計算される `created_at` から `Order date`、秒の整数として返されます |
| `Seconds since cart creation` | 買い物かごの作成日から現在までの経過時間。 引いて計算される `created_at` クエリ実行時のサーバーのタイムスタンプから、秒数の整数で返されます。 買い物かごの年齢を識別するために最も一般的に使用される |
| `Store name` | この注文に関連付けられたCommerce ストアの名前。 結合によって計算 `quote.store_id` 対象： `store.store_id` およびを返します `name` フィールド |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **建設** |
|---|---|---|
| `Number of abandoned carts` | 特定の「放棄」条件を満たす買い物かごの数 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>フィルター：<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x。ここで「x」は、買い物かごが作成されてからの経過時間（秒）を表します。この時間を超えると、買い物かごは放棄されたと見なされます |
| `Avg time to cart conversion` | コンバート済み買い物かごの作成から注文の作成までの平均時間 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 売上高が次のように定義されている、放棄された買い物かごの潜在的な売上高の合計 `base_grand_total` フィールド | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>フィルター：<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x。ここで「x」は、買い物かごが作成されてからの経過時間（秒）を表します。この時間を超えると、買い物かごは放棄されたと見なされます |

{style="table-layout:auto"}

## 外部キー結合パス

`customer_entity`

* に参加 `customer_entity` 買い物かごを作成した顧客に関連付けられた、新しい顧客レベルの列を作成するテーブル。
   * パス： `quote.customer_id` （多） => `customer_entity.entity_id` （1）

`sales_order`

* に参加 `sales_order` 変換後の買い物かごに関連付けられた注文の詳細を返す列を作成する表。
   * パス：`quote.reserved_order_id` （多） => `sales_order.increment_id` （1）

`store`

* に参加 `store` 買い物かごに関連付けられたCommerce ストアに関連する詳細を返す列を作成するテーブル。
   * パス： `quote.store_id` （多） => `store.store_id` （1）
