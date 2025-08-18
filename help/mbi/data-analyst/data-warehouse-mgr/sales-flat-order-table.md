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

`sales_order` の表（M1 の `sales_flat_order`）は、各注文がキャプチャされる場所です。 通常、各行は 1 つの一意の注文を表しますが、Commerceには、注文を別々の行に分割するカスタム実装がいくつかあります。

この表には、ゲストのチェックアウトを通じてその注文が処理されたかどうかにかかわらず、すべての顧客の注文が含まれています。 ストアがゲストのチェックアウトを受け入れる場合は、この [ ユースケース ](../data-warehouse-mgr/guest-orders.md) に関する詳細を確認できます。

## 共通列

| **列名** | **説明** |
|---|---|
| `base_currency_code` | `base_*` のフィールドで取得されるすべての値の通貨（`base_grand_total`、`base_subtotal` など）。 これは通常、Commerce ストアのデフォルト通貨を反映します |
| `base_discount_amount` | 注文に適用される割引値 |
| `base_grand_total` | すべての税金、送料、割引が適用された後に、顧客が注文に対して支払った最終価格。 正確な計算はカスタマイズ可能ですが、通常、`base_grand_total` は `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` として計算されます |
| `base_subtotal` | 注文に含まれるすべての品目の総商品価値。 税金、送料、割引などは含まれません |
| `base_shipping_amount` | 注文に適用される配送料 |
| `base_tax_amount` | 注文に適用される税額 |
| `billing_address_id` | `Foreign key` テーブルに関連付けられた `sales_order_address`。 `sales_order_address.entity_id` に参加して、注文に関連付けられた請求先住所の詳細を決定します |
| `coupon_code` | クーポンが注文に適用されました。 クーポンが適用されない場合、このフィールドは `NULL` です |
| `created_at` | 注文の作成タイムスタンプ（UTC でローカルに保存）。 [!DNL Commerce Intelligence] での設定に応じて、このタイムスタンプはデータベースのタイムゾーンとは異な [!DNL Commerce Intelligence] レポートタイムゾーンに変換される場合があります |
| `customer_email` | 注文を行う顧客の電子メールアドレス。 これは、ゲストチェックアウトで処理された注文を含め、すべての状況で入力されます |
| `customer_group_id` | `customer_group` テーブルに関連付けられている外部キー。 `customer_group.customer_group_id` に結合して、注文に関連付けられている顧客グループを決定します |
| `customer_id` | 顧客が登録されている場合、`Foreign key` テーブルに関連付けられた `customer_entity` ール。 `customer_entity.entity_id` に結合して、注文に関連付けられている顧客属性を決定します。 ゲストのチェックアウトで注文された場合、このフィールドは `NULL` になります |
| `entity_id` （PK） | テーブルの一意の ID。Commerce インスタンス内の他のテーブルへの結合で一般的に使用されます |
| `increment_id` | 注文の一意の ID。Adobe Commerceでは `order_id` と呼ばれることが多いです。 `increment_id` は、[!DNL Google Ecommerce] などの外部ソースへの結合に最もよく使用されます |
| `shipping_address_id` | `sales_order_address` テーブルに関連付けられている外部キー。 `sales_order_address.entity_id` に結合して、注文に関連付けられた配送先住所の詳細を決定します |
| `status` | 注文のステータス。 「complete」、「processing」、「cancelled」、「refunded」、およびCommerce インスタンスに実装されているカスタムステータスなどの値を返す場合があります。 注文が処理されるたびに変更される場合があります |
| `store_id` | `Foreign key` テーブルに関連付けられた `store`。 `store` に参加します。どのCommerce ストアビューが注文に関連付けられているかを判断する `store_id` 法 |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Billing address city` | 注文の請求先市区町村。 `sales_order` を結合して計算されます。`billing_address_id`～`sales_order_address`。`entity_id` フィールドの `city` び出しと返し |
| `Billing address country` | 注文の請求国コード。 `sales_order` を結合して計算されます。`billing_address_id`～`sales_order_address`。`entity_id` ージの `country_id` ージと返し |
| `Billing address region` | 注文の請求地域（ほとんどの場合は都道府県）。 `sales_order` を結合して計算されます。`billing_address_id`～`sales_order_address`。`entity_id` フィールドの `region` び出しと返し |
| `Customer's first order date` | この顧客による最初の注文のタイムスタンプ。 多くの場合、顧客の「獲得日」と見なされます。 最小 `sales_order` を返すことによって計算されます。一意の各顧客の `created_at` 値 |
| `Customer's first order's billing region` | 注文を行った顧客の取得請求地域。 顧客の最初の注文に関連付けられた `Billing address region` を返すことにより計算されます |
| `Customer's first order's coupon_code` | この注文を行った顧客の獲得クーポンコード。 顧客の最初の注文に関連付けられた `coupon_code` を返すことにより計算されます |
| `Customer's group code` | この注文を行った顧客のグループ名。 `sales_order` を結合して計算されます。`customer_group_id`～`customer_group`。`customer_group_id` フィールドの `customer_group_code` び出しと返し |
| `Customer's lifetime number of coupons` | この顧客が発注したすべての注文に適用されたクーポンの合計数量。 一意の顧客ごとに、`coupon_code` が `NULL` しくない注文の数をカウントして計算されます |
| `Customer's lifetime number of orders` | この顧客が注文した注文の合計数。 一意の顧客ごとに `sales_order` テーブルの行数をカウントすることによって計算されます |
| `Customer's lifetime revenue` | この顧客が行ったすべての注文の売上高の合計。 一意の顧客ごとに、すべての注文の `base_grand_total` フィールドを合計して計算されます |
| `Customer's order number` | この顧客の注文の順次オーダーランク。 顧客から注文されたすべての注文を識別し、`created_at` タイムスタンプで昇順に並べ替え、各注文に増分する整数値を割り当てることによって計算されます。 例えば、顧客の最初の注文は `Customer's order number` 1 を返し、顧客の 2 番目の注文は `Customer's order number` 2 を返します。 |
| `Customer's order number (previous-current)` | 顧客の以前の注文のランクを、この注文のランクと連結し、`-` 文字で区切ります。 （「`Customer's order number` - 1」）を「`-`」に続いて「`Customer's order number`」で連結することによって計算されます。 例えば、顧客の 2 回目の購入に関連付けられた注文の場合、この列は `1-2` の値を返します。 2 つの注文イベント間の時間を表す（「注文間の時間」グラフ）場合に最もよく使用されます |
| `Is customer's last order?` | 注文が顧客の最後の注文に対応するか、最新の注文に対応するかを決定します。 `Customer's order number` 値を `Customer's lifetime number of orders` と比較して計算されます。 これら 2 つのフィールドが指定された順序で等しい場合、この列は `Yes` を返し、それ以外の場合は `No` を返します |
| `Number of items in order` | 注文に含まれる品目の合計数量。 `sales_order` を結合して計算されます。`entity_id`～`sales_order_item`。`order_id` を `sales_order_item` して合計します。`qty_ordered` フィールド |
| `Seconds between customer's first order date and this order` | この注文と顧客の最初の注文の間の経過時間。 各注文の `Customer's first order date` から `created_at` を減算して計算され、秒数の整数で返されます |
| `Seconds since previous order` | この注文と顧客の直前の注文の間の経過時間。 この注文の `created_at` から前の注文の `created_at` を引いて計算され、秒数の整数で返されます。 例えば、顧客の 3 番目の注文に対応する注文レコードの場合、この列は、顧客の 2 番目の注文から 3 番目の注文までの秒数を返します。 顧客の初回注文の場合、このフィールドは `NULL` を返します |
| `Shipping address city` | 注文の発送先市区町村。 `sales_order` を結合して計算されます。`shipping_address_id`～`sales_order_address`。`entity_id` フィールドの `city` び出しと返し |
| `Shipping address country` | 注文の発送国コード。 `sales_order` を結合して計算されます。`Shipping_address_id`～`sales_order_address`。`entity_id` ージの `country_id` ージと返し |
| `Shipping address region` | 注文の出荷地域（ほとんどの場合は都道府県）。 `sales_order` を結合して計算されます。`shipping_address_id`～`sales_order_address`。`entity_id` フィールドの `region` び出しと返し |
| `Store name` | この注文に関連付けられたCommerce ストアの名前。 `sales_order` を結合して計算されます。`store_id`～`store`。`store_id` フィールドの `name` び出しと返し |

## 一般的な指標

| **指標名** | **説明** | **建設** |
|---|---|---|
| `Avg order value` | 売上高が `base_grand_total` として定義される、注文あたりの平均売上高 | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | すべての顧客および注文について、顧客の（n-1）番目の注文から n 番目の注文までの平均時間 | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | すべての注文の総商品価値の合計（GMV が小計として定義される）。すべての税金と割引が適用される前です | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | すべての顧客および注文について、顧客の（n-1）注文と n 番目の注文の間の中央値の時間 | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | 注文の合計数 | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | すべての税金、割引、送料などが適用された後、売上高が顧客によって支払われた最終価格として定義されるすべての注文の売上高の合計 | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | すべての注文の出荷金額の合計 | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | すべての注文に適用される税の合計 | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | 特定のレポート時間間隔で注文を行った一意の顧客の数。 例えば、レポートの間隔が毎週の場合、特定の週に少なくとも 1 つの注文を行った各顧客は、その週に行った注文数に関係なく、正確に 1 回とカウントされます | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` 結合パス

`customer_entity`

* テーブルに結合 `customer_entity` て、注文した顧客に関連付けられた新しい顧客レベルの列を作成します。
   * パス：`sales_order.customer_id` （多） => `customer_entity.entity_id` （1）

`customer_group`

* テーブルに結合 `customer_group` て、注文した顧客の顧客グループ名を返す列を作成します。
   * パス：`sales_order.customer_group_id` （多） => `customer_group.customer_group_id` （1）

`sales_order_address`

* テーブルに結合 `sales_order_address` て、注文に関連付けられた請求および出荷場所を返す列を作成します。 請求または出荷の詳細が必要かどうかに応じて、2 つの結合パスを使用できます。
   * パス：
      * 送料：`sales_order.shipping_address_id` （多） => `sales_order_address.entity_id` （1）
      * 請求：`sales_order.billing_address_id` （多） => `sales_order_address.entity_id` （1）

`store`

* テーブルに結合 `store` て、注文に関連付けられたCommerce ストアに関連する詳細を返す列を作成します。
   * パス：`sales_order.store_id` （多） => `store.store_id` （1）
