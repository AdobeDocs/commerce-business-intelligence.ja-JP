---
title: sales_order テーブル
description: sales_order テーブルの操作方法を説明します。
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# `sales_order` テーブル

この `sales_order` テーブル （`sales_flat_order` m1 では）各注文がキャプチャされる場所です。 通常、各行は 1 つの一意の注文を表しますが、Commerceには、注文を別々の行に分割するカスタム実装がいくつかあります。

この表には、ゲストのチェックアウトを通じてその注文が処理されたかどうかにかかわらず、すべての顧客の注文が含まれています。 ストアがゲストのチェックアウトを受け入れる場合は、これに関する詳細を確認できます [ユースケース](../data-warehouse-mgr/guest-orders.md).

## 共通列

| **列名** | **説明** |
|---|---|
| `base_currency_code` | で取得されるすべての値の通貨 `base_*` フィールド（つまり、 `base_grand_total`, `base_subtotal`など）。 これは通常、Commerce ストアのデフォルト通貨を反映します |
| `base_discount_amount` | 注文に適用される割引値 |
| `base_grand_total` | すべての税金、送料、割引が適用された後に、顧客が注文に対して支払った最終価格。 正確な計算はカスタマイズできますが、一般的には `base_grand_total` 次のように計算されます `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | 注文に含まれるすべての品目の総商品価値。 税金、送料、割引などは含まれません |
| `base_shipping_amount` | 注文に適用される配送料 |
| `base_tax_amount` | 注文に適用される税額 |
| `billing_address_id` | `Foreign key` に関連付ける `sales_order_address` テーブル。 に参加 `sales_order_address.entity_id` 注文に関連する請求先住所の詳細を決定するには |
| `coupon_code` | クーポンが注文に適用されました。 クーポンが適用されない場合、このフィールドは `NULL` |
| `created_at` | 注文の作成タイムスタンプ（UTC でローカルに保存）。 での設定に応じて [!DNL Commerce Intelligence]、このタイムスタンプはのレポートタイムゾーンに変換される場合があります [!DNL Commerce Intelligence] データベースのタイムゾーンとは異なる |
| `customer_email` | 注文を行う顧客の電子メールアドレス。 これは、ゲストチェックアウトで処理された注文を含め、すべての状況で入力されます |
| `customer_group_id` | に関連付けられた外部キー `customer_group` テーブル。 に参加 `customer_group.customer_group_id` 注文に関連付けられている顧客グループを特定するには |
| `customer_id` | `Foreign key` に関連付ける `customer_entity` 表（顧客が登録されている場合） に参加 `customer_entity.entity_id` 注文に関連付けられている顧客属性を決定します。 ゲストのチェックアウトで注文された場合、このフィールドは `NULL` |
| `entity_id` （PK） | テーブルの一意の ID。Commerce インスタンス内の他のテーブルへの結合で一般的に使用されます |
| `increment_id` | 注文の一意の ID。一般的にと呼ばれます `order_id` Adobe Commerce内。 この `increment_id` 次のような外部ソースへの結合に最もよく使用されます [!DNL Google Ecommerce] |
| `shipping_address_id` | に関連付けられた外部キー `sales_order_address` テーブル。 に参加 `sales_order_address.entity_id` 注文に関連する配送先住所の詳細を決定するには |
| `status` | 注文のステータス。 「complete」、「processing」、「cancelled」、「refunded」、およびCommerce インスタンスに実装されているカスタムステータスなどの値を返す場合があります。 注文が処理されるたびに変更される場合があります |
| `store_id` | `Foreign key` に関連付ける `store` テーブル。 に参加 `store`.`store_id` 注文に関連付けられているCommerce ストア表示を特定するには |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Billing address city` | 注文の請求先市区町村。 結合によって計算 `sales_order`.`billing_address_id` 対象： `sales_order_address`.`entity_id` およびを返します `city` フィールド |
| `Billing address country` | 注文の請求国コード。 結合によって計算 `sales_order`.`billing_address_id` 対象： `sales_order_address`.`entity_id` およびを返します `country_id` |
| `Billing address region` | 注文の請求地域（ほとんどの場合は都道府県）。 結合によって計算 `sales_order`.`billing_address_id` 対象： `sales_order_address`.`entity_id` およびを返します `region` フィールド |
| `Customer's first order date` | この顧客による最初の注文のタイムスタンプ。 多くの場合、顧客の「獲得日」と見なされます。 最小値を返すことにより計算 `sales_order`.`created_at` 一意の各顧客の値 |
| `Customer's first order's billing region` | 注文を行った顧客の取得請求地域。 を返すことによって計算されます。 `Billing address region` 顧客の最初の注文に関連付けられる |
| `Customer's first order's coupon_code` | この注文を行った顧客の獲得クーポンコード。 を返すことによって計算されます。 `coupon_code` 顧客の最初の注文に関連付けられる |
| `Customer's group code` | この注文を行った顧客のグループ名。 結合によって計算 `sales_order`.`customer_group_id` 対象： `customer_group`.`customer_group_id` およびを返します `customer_group_code` フィールド |
| `Customer's lifetime number of coupons` | この顧客が発注したすべての注文に適用されたクーポンの合計数量。 注文数をカウントすることで計算され、 `coupon_code` 等しくない `NULL` 一意の顧客ごとの |
| `Customer's lifetime number of orders` | この顧客が注文した注文の合計数。 の行数をカウントすることによって計算されます。 `sales_order` 各一意の顧客のテーブル |
| `Customer's lifetime revenue` | この顧客が行ったすべての注文の売上高の合計。 を合計して計算 `base_grand_total` 一意の各顧客のすべての注文のフィールド |
| `Customer's order number` | この顧客の注文の順次オーダーランク。 顧客からの注文をすべて識別し、で昇順に並べ替えることで計算されます `created_at` タイムスタンプを入力し、注文ごとに増分する整数値を割り当てます。 例えば、顧客の最初の注文は `Customer's order number` 1 のうち、顧客の 2 番目の注文はを返します `Customer's order number` （2）など。 |
| `Customer's order number (previous-current)` | 顧客の以前の注文のランクを、この注文のランクと連結し、で区切ります `-` 文字。 （&quot;を連結して計算`Customer's order number` - 1&quot;）、&quot;`-`「」の後に「」が続きます`Customer's order number`」と入力します。 例えば、顧客の 2 番目の購入に関連付けられた注文の場合、この列はの値を返します。 `1-2`. 2 つの注文イベント間の時間を表す（「注文間の時間」グラフ）場合に最もよく使用されます |
| `Is customer's last order?` | 注文が顧客の最後の注文に対応するか、最新の注文に対応するかを決定します。 を比較して計算されます `Customer's order number` 次を使用して値 `Customer's lifetime number of orders`. これら 2 つのフィールドが指定の順序で等しい場合、この列はを返します `Yes`；それ以外の場合はを返します `No` |
| `Number of items in order` | 注文に含まれる品目の合計数量。 結合によって計算 `sales_order`.`entity_id` 対象： `sales_order_item`.`order_id` を合計する `sales_order_item`.`qty_ordered` フィールド |
| `Seconds between customer's first order date and this order` | この注文と顧客の最初の注文の間の経過時間。 引いて計算される `Customer's first order date` から `created_at` 各注文に対して、秒数の整数で返されます |
| `Seconds since previous order` | この注文と顧客の直前の注文の間の経過時間。 を減算して計算されます `created_at` （以前の注文の場合） `created_at` この順序の場合、秒数の整数として返されます。 例えば、顧客の 3 番目の注文に対応する注文レコードの場合、この列は、顧客の 2 番目の注文から 3 番目の注文までの秒数を返します。 顧客の最初の注文の場合、このフィールドは次を返します `NULL` |
| `Shipping address city` | 注文の発送先市区町村。 結合によって計算 `sales_order`.`shipping_address_id` 対象： `sales_order_address`.`entity_id` およびを返します `city` フィールド |
| `Shipping address country` | 注文の発送国コード。 結合によって計算 `sales_order`.`Shipping_address_id` 対象： `sales_order_address`.`entity_id` およびを返します `country_id` |
| `Shipping address region` | 注文の出荷地域（ほとんどの場合は都道府県）。 結合によって計算 `sales_order`.`shipping_address_id` 対象： `sales_order_address`.`entity_id` およびを返します `region` フィールド |
| `Store name` | この注文に関連付けられたCommerce ストアの名前。 結合によって計算 `sales_order`.`store_id` 対象： `store`.`store_id` およびを返します `name` フィールド |

## 一般的な指標

| **指標名** | **説明** | **建設** |
|---|---|---|
| `Avg order value` | 売上高が次のように定義されている場合の、注文あたりの平均売上高 `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | すべての顧客および注文について、顧客の（n-1）番目の注文から n 番目の注文までの平均時間 | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | すべての注文の総商品価値の合計（GMV が小計として定義される）。すべての税金と割引が適用される前です | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | すべての顧客および注文について、顧客の（n-1）注文と n 番目の注文の間の中央値の時間 | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | 注文の合計数 | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | すべての税金、割引、送料などが適用された後、売上高が顧客によって支払われた最終価格として定義されるすべての注文の売上高の合計 | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | すべての注文の出荷金額の合計 | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | すべての注文に適用される税の合計 | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | 特定のレポート時間間隔で注文を行った一意の顧客の数。 例えば、レポートの間隔が毎週の場合、特定の週に少なくとも 1 つの注文を行った各顧客は、その週に行った注文数に関係なく、正確に 1 回とカウントされます | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` パスの結合

`customer_entity`

* に参加 `customer_entity` 注文を行った顧客に関連付けられた、新しい顧客レベルの列を作成する表。
   * パス： `sales_order.customer_id` （多） => `customer_entity.entity_id` （1）

`customer_group`

* に参加 `customer_group` 注文した顧客の顧客グループ名を返す列を作成するテーブル。
   * パス： `sales_order.customer_group_id` （多） => `customer_group.customer_group_id` （1）

`sales_order_address`

* に参加 `sales_order_address` 受注に関連付けられた請求事業所および出荷事業所を戻す列を作成する表。 請求または出荷の詳細が必要かどうかに応じて、2 つの結合パスを使用できます。
   * パス：
      * 送料： `sales_order.shipping_address_id`（多） => `sales_order_address.entity_id` （1）
      * 請求： `sales_order.billing_address_id`（多） => `sales_order_address.entity_id` （1）

`store`

* に参加 `store` 注文に関連付けられたCommerce ストアに関連する詳細を返す列を作成するテーブル。
   * パス： `sales_order.store_id` （多） => `store.store_id` （1）
