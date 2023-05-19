---
title: 見積表
description: 見積もり表の使用方法を説明します。
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# 見積表

この `quote` テーブル (`sales_flat_quote` (M1) には、店舗で作成された各買い物かごのレコードが含まれます。放棄された買い物かごか、購入に変換された買い物かごかが含まれます。 各行は 1 つの買い物かごを表します。 このテーブルの潜在的なサイズにより、Adobeでは、60 日を超える未変換の買い物かごがある場合など、特定の条件を満たした場合に、レコードを定期的に削除することをお勧めします。

>[!NOTE]
>
>履歴の放棄された買い物かごの分析は、 `quote` 表。 レコードを削除した場合は、データベースからまだ削除されていない買い物かごのみを表示できます。

## 共通のネイティブ列

| **列名** | **説明** |
|---|---|
| `base_currency_code` | で取り込まれるすべての値の通貨 `base_*` フィールド ( `base_grand_total`, `base_subtotal`など )。 これは、通常、コマースストアのデフォルトの通貨を反映します |
| `base_grand_total` | すべての税金、送料、割引が適用された後、買い物かごに対する顧客に引用された最終価格。 正確な計算はカスタマイズできますが、一般に、 `base_grand_total` は次のように計算されます。 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | 買い物かごに含まれるすべての品目の総商品価格。 税、送料、割引などは含まれません |
| `created_at` | 買い物かごの作成タイムスタンプ（UTC でローカルに保存）。 の設定に応じて、 [!DNL Commerce Intelligence]の場合、このタイムスタンプは [!DNL Commerce Intelligence] データベースのタイムゾーンと異なる |
| `customer_email` | 買い物かごを作成した顧客の電子メールアドレス |
| `customer_id` | `Foreign key` ～と関連している `customer_entity` 顧客が登録されている場合は、テーブル。 結合先 `customer_entity.entity_id` を使用して、買い物かごを作成したユーザーに関連付けられている顧客属性を特定します。 買い物かごがゲストによるチェックアウトで作成された場合、このフィールドは `NULL` |
| `entity_id` (PK) | テーブルの一意の識別子。Commerce インスタンス内の他のテーブルへの結合で一般的に使用されます |
| `is_active` | 買い物かごが顧客によって作成され、まだ注文に変換されていない場合に「1」を返すブール値フィールド。 コンバージョンされた買い物かごに対しては「0」、管理者が作成した買い物かごに対しては「0」を返します |
| `items_qty` | 買い物かごに含まれるすべての品目の合計数量の合計 |
| `reserved_order_id` | `Foreign key` ～と関連している `sales_order` 表。 結合先 `sales_order.increment_id` 変換後の買い物かごに関連する注文の詳細を判断するために使用します。 変換後の注文に関連付けられていない買い物かごの場合、 `reserved_order_id` 件 `NULL` |
| `store_id` | `Foreign key` ～と関連している `store` 表。 結合先 `store`.`store_id` 買い物かごに関連付けられているコマースストア表示を特定するには |

{style="table-layout:auto"}

## 共通の計算列

| **列名** | **説明** |
|---|---|
| `Order date` | コンバートされた買い物かごの注文作成日を反映したタイムスタンプ。 結合によって計算 `quote.reserved_order_id` から `sales_order.increment_id` そして `sales_order.created_at` フィールド |
| `Seconds between cart creation and order` | 買い物かごの作成から注文の作成までの経過時間。 減算で計算 `created_at` から `Order date`を返します。 |
| `Seconds since cart creation` | 買い物かごの作成日から今までの経過時間。 減算で計算 `created_at` クエリの実行時のサーバーのタイムスタンプから、整数の秒数で返されます。 買い物かごの年齢を識別するのに最も一般的に使用されます |
| `Store name` | この注文に関連付けられたコマースストアの名前。 結合によって計算 `quote.store_id` から `store.store_id` そして `name` フィールド |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **構築** |
|---|---|---|
| `Number of abandoned carts` | 特定の「放棄」条件を満たす買い物かごの数 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>フィルター：<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x(「x」は、買い物かごが破棄されたと見なされる、買い物かごが作成されてからの経過時間（秒）) です。 |
| `Avg time to cart conversion` | コンバージョンされた買い物かごに対する、買い物かご作成から注文作成までの平均時間 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 放棄された買い物かごの潜在的な売上高の合計。売上高は `base_grand_total` フィールド | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>フィルター：<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x(「x」は、買い物かごが破棄されたと見なされる、買い物かごが作成されてからの経過時間（秒）) です。 |

{style="table-layout:auto"}

## 外部キー結合パス

`customer_entity`

* 結合先 `customer_entity` 買い物かごを作成した顧客に関連付けられた、新しい顧客レベルの列を作成するテーブル。
   * パス： `quote.customer_id` （多数） => `customer_entity.entity_id` (1)

`sales_order`

* 結合先 `sales_order` 変換後の買い物かごに関連付けられた注文の詳細を返す列を作成するテーブル。
   * パス：`quote.reserved_order_id` （多数） => `sales_order.increment_id` (1)

`store`

* 結合先 `store` 買い物かごに関連付けられたコマースストアに関連する詳細を返す列を作成するテーブル。
   * パス： `quote.store_id` （多数） => `store.store_id` (1)
