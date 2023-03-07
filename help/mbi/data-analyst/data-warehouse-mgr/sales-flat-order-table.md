---
title: sales_order テーブル
description: sales_order テーブルの操作方法を説明します。
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# `sales_order` テーブル

この `sales_order` テーブル (`sales_flat_order` M1) では、各注文がキャプチャされます。 通常、各行は 1 つの一意の順序を表しますが、Commerce のカスタム実装では、順序を別々の行に分割することになります。

このテーブルには、その注文がゲストのチェックアウトで処理されたかどうかに関わらず、すべての顧客注文が含まれます。 ストアがゲストによるチェックアウトを受け入れる場合、これに関する詳細を確認できます [使用例](../data-warehouse-mgr/guest-orders.md).

## 共通列

| **列名** | **説明** |
|---|---|
| `base_currency_code` | で取り込まれるすべての値の通貨 `base_*` フィールド ( `base_grand_total`, `base_subtotal`など )。 これは、通常、コマースストアのデフォルトの通貨を反映します |
| `base_discount_amount` | 注文に適用される割引値 |
| `base_grand_total` | すべての税金、送料、割引が適用された後に、注文に関して顧客が支払った最終的な価格。 正確な計算はカスタマイズできますが、一般に、 `base_grand_total` は次のように計算されます。 `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | 注文に含まれるすべての品目の総商品価格。 税、送料、割引などは含まれません |
| `base_shipping_amount` | 注文に適用される送料の値 |
| `base_tax_amount` | 注文に適用される税額 |
| `billing_address_id` | `Foreign key` ～と関連している `sales_order_address` 表。 結合先 `sales_order_address.entity_id` 注文に関連付けられた請求先住所の詳細を決定するには |
| `coupon_code` | 注文に適用されたクーポン。 クーポンが適用されていない場合、このフィールドは「 `NULL` |
| `created_at` | 注文の作成タイムスタンプ。ローカルの UTC に保存されます。 の設定に応じて、 [!DNL MBI]の場合、このタイムスタンプは [!DNL MBI] データベースのタイムゾーンと異なる |
| `customer_email` | 注文をする顧客の電子メールアドレス。 これは、ゲストによるチェックアウトで処理される注文を含め、すべての状況で設定されます |
| `customer_group_id` | に関連付けられた外部キー `customer_group` 表。 結合先 `customer_group.customer_group_id` オーダーに関連付けられた顧客グループを特定するには、以下を実行します。 |
| `customer_id` | `Foreign key` ～と関連している `customer_entity` 顧客が登録されている場合は、テーブル。 結合先 `customer_entity.entity_id` を使用して、注文に関連付けられている顧客属性を特定します。 注文がゲストによるチェックアウトを通じておこなわれた場合、このフィールドは `NULL` |
| `entity_id` (PK) | テーブルの一意の識別子。Commerce インスタンス内の他のテーブルへの結合で一般的に使用されます |
| `increment_id` | 注文の一意の識別子 ( 一般的に `order_id` Adobe Commerceの この `increment_id` は、外部ソースへの結合に最も多く使用されます。 [!DNL Google Ecommerce] |
| `shipping_address_id` | に関連付けられた外部キー `sales_order_address` 表。 結合先 `sales_order_address.entity_id` 注文に関連付けられた配送先住所の詳細を決定するには |
| `status` | 注文のステータス。 「complete」、「processing」、「cancelled」、「refunded」などの値と、Commerce インスタンスに実装されているカスタムステータスを返す場合があります。 オーダーの処理時に変更される場合があります |
| `store_id` | `Foreign key` ～と関連している `store` 表。 結合先 `store`.`store_id` 注文に関連付けられているコマースストア表示を特定するには |

{style="table-layout:auto"}

## 共通の計算列

| **列名** | **説明** |
|---|---|
| `Billing address city` | 注文の請求先住所（市区町村）。 結合によって計算 `sales_order`.`billing_address_id` から `sales_order_address`.`entity_id` そして `city` フィールド |
| `Billing address country` | 注文の請求国コード。 結合によって計算 `sales_order`.`billing_address_id` から `sales_order_address`.`entity_id` そして `country_id` |
| `Billing address region` | 注文の請求地域（多くの場合、州または都道府県）。 結合によって計算 `sales_order`.`billing_address_id` から `sales_order_address`.`entity_id` そして `region` フィールド |
| `Customer's first order date` | この顧客が最初に発注した注文のタイムスタンプ。 多くの場合、顧客の「獲得日」と見なされます。 最小値を返すことで計算 `sales_order`.`created_at` 各ユニーク顧客の価値 |
| `Customer's first order's billing region` | 注文をした顧客の獲得請求地域。 を返すことで計算されます。 `Billing address region` 顧客の最初の注文に関連している |
| `Customer's first order's coupon_code` | この注文をした顧客の獲得クーポンコード。 を返すことで計算されます。 `coupon_code` 顧客の最初の注文に関連している |
| `Customer's group code` | この注文を行った顧客のグループ名。 結合によって計算 `sales_order`.`customer_group_id` から `customer_group`.`customer_group_id` そして `customer_group_code` フィールド |
| `Customer's lifetime number of coupons` | この顧客が行ったすべての注文に適用されたクーポンの合計数。 注文の数をカウントして計算します。 `coupon_code` 等しくない `NULL` ユニーク顧客ごとに |
| `Customer's lifetime number of orders` | この顧客が行った注文の合計数。 行数を `sales_order` 個別顧客ごとの表 |
| `Customer's lifetime revenue` | この顧客が行ったすべての注文に関する売上高の合計。 計算方法は `base_grand_total` 各ユニーク顧客のすべての注文のフィールド |
| `Customer's order number` | この顧客の注文の順次注文ランク。 顧客が発注したすべての注文を識別し、 `created_at` タイムスタンプを設定し、各注文に増分整数値を割り当てます。 例えば、顧客の最初の注文では、 `Customer's order number` が 1 の場合、顧客の 2 番目の注文は `Customer's order number` 2 など。 |
| `Customer's order number (previous-current)` | 顧客の前のオーダーのランクとこのオーダーのランクを連結したもので、 `-` 文字。 連結 (&quot;`Customer's order number` - 1&quot;) を&quot;`-`&quot;の後に&quot;`Customer's order number`&quot;. 例えば、顧客の 2 回目の購入に関連付けられた注文の場合、この列は、 `1-2`. 最も頻繁に使用されるのは、2 つの注文イベントの間の時間を表す場合です（つまり、「注文間の時間」グラフ）。 |
| `Is customer's last order?` | 注文が顧客の最後の注文に対応するか、最新の注文に対応するかを決定します。 比較によって計算される `Customer's order number` 値 `Customer's lifetime number of orders`. これら 2 つのフィールドが指定された順序に等しい場合、この列は「はい」を返します。それ以外の場合は、「No」を返します。 |
| `Number of items in order` | 注文に含まれる品目の合計数量。 結合によって計算 `sales_order`.`entity_id` から `sales_order_item`.`order_id` そして要約すると `sales_order_item`.`qty_ordered` フィールド |
| `Seconds between customer's first order date and this order` | この注文から顧客の最初の注文までの経過時間。 減算で計算 `Customer's first order date` から `created_at` 各注文に対して、秒数の整数で返されます。 |
| `Seconds since previous order` | この注文から顧客の直前の注文までの経過時間。 計算には `created_at` 以前の `created_at` の値を返します。 例えば、顧客の 3 番目の注文に対応する注文レコードの場合、この列は顧客の 2 番目の注文から 3 番目の注文までの秒数を返します。 顧客の最初の注文に対して、このフィールドは `NULL` |
| `Shipping address city` | 注文の配送先の市区町村。 結合によって計算 `sales_order`.`shipping_address_id` から `sales_order_address`.`entity_id` そして `city` フィールド |
| `Shipping address country` | 注文の配送先国コード。 結合によって計算 `sales_order`.`Shipping_address_id` から `sales_order_address`.`entity_id` そして `country_id` |
| `Shipping address region` | 注文の出荷地域（ほとんどの場合、州または都道府県）。 結合によって計算 `sales_order`.`shipping_address_id` から `sales_order_address`.`entity_id` そして `region` フィールド |
| `Store name` | この注文に関連付けられたコマースストアの名前。 結合によって計算 `sales_order`.`store_id` から `store`.`store_id` そして `name` フィールド |

## 一般的な指標

| **指標名** | **説明** | **構築** |
|---|---|---|
| `Avg order value` | 注文あたりの平均売上高。売上高は `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | すべての顧客および注文に関して、顧客の (n-1) 注文から n 番目の注文までの平均時間 | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | すべての税金と割引が適用される前の、GMV が小計として定義されているすべての注文の総商品額の合計 | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | すべての顧客および注文について、顧客の (n-1) 注文から n 番目の注文までの中央値時間 | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | 発注の総数 | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | すべての注文の売上高の合計。売上高は、すべての税金、割引、送料などの後に、顧客が支払った最終的な価格として定義されます | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | すべての注文の送料の合計 | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | すべての注文に適用される税金の合計 | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | 特定のレポート期間に注文をしたユニーク顧客の数。 例えば、レポートの間隔が毎週の場合、特定の週に 1 回以上注文した各顧客は、その週に注文した注文数に関係なく、正確に 1 回とカウントされます | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` パスの結合

`customer_entity`

* 結合先 `customer_entity` 注文した顧客に関連付けられた新しい顧客レベルの列を作成するテーブル。
   * パス： `sales_order.customer_id` （多数） => `customer_entity.entity_id` (1)

`customer_group`

* 結合先 `customer_group` 注文をした顧客の顧客グループ名を返す列を作成するテーブル。
   * パス： `sales_order.customer_group_id` （多数） => `customer_group.customer_group_id` (1)

`sales_order_address`

* 結合先 `sales_order_address` 表を使用して、注文に関連付けられた請求先と配送先を返す列を作成します。 請求または配送の詳細が必要かに応じて、2 つの結合パスが可能です。
   * パス：
      * 送料： `sales_order.shipping_address_id`（多数） => `sales_order_address.entity_id` (1)
      * 請求： `sales_order.billing_address_id`（多数） => `sales_order_address.entity_id` (1)

`store`

* 結合先 `store` 注文に関連付けられたコマースストアに関連する詳細を返す列を作成するテーブル。
   * パス： `sales_order.store_id` （多数） => `store.store_id` (1)
