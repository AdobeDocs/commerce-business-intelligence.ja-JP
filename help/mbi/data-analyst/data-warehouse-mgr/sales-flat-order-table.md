---
title: sales_order テーブル
description: sales_order テーブルの操作方法を説明します。
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/zdxIx9qHzEyoCbFzh0EBv1BKJEWiShtAt33-dtkEGNo
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
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
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 1200
ht-degree: 0%

---

# `sales_order` テーブル

`sales_order` テーブル （`sales_flat_order` on M1）は、各注文がキャプチャされる場所です。 通常、各行は1つの一意の順序を表しますが、Commerceのカスタム実装では、順序を別々の行に分割することになります。

このテーブルには、その注文がゲストチェックアウトを通じて処理されたかどうかにかかわらず、すべての顧客の注文が含まれます。 お客様のストアがゲストチェックアウトを受け付けている場合は、この[&#x200B; ユースケース &#x200B;](../data-warehouse-mgr/guest-orders.md)に関する詳細情報を確認できます。

## 共通の列

| **列名** | **説明** |
|---|---|
| `base_currency_code` | `base_*` フィールドにキャプチャされたすべての値の通貨（つまり、`base_grand_total`、`base_subtotal`など）。 これは通常、Commerce ストアのデフォルトの通貨を反映しています |
| `base_discount_amount` | 注文に適用された割引値 |
| `base_grand_total` | すべての税金、送料、割引が適用された後、注文でお客様が支払った最終価格。 正確な計算はカスタマイズ可能ですが、一般的に`base_grand_total`は`base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount`として計算されます |
| `base_subtotal` | 注文に含まれるすべてのアイテムの総商品価値。 税金、送料、割引などは含まれていません |
| `base_shipping_amount` | 注文に適用された出荷金額 |
| `base_tax_amount` | 注文に適用される税額 |
| `billing_address_id` | `Foreign key`が`sales_order_address` テーブルに関連付けられています。 `sales_order_address.entity_id`に参加して、注文に関連付けられている請求先住所の詳細を決定します |
| `coupon_code` | 注文に適用されたクーポン。 クーポンが適用されない場合、このフィールドは`NULL`です |
| `created_at` | 注文の作成タイムスタンプ。ローカルにUTCで保存されます。 [!DNL Commerce Intelligence]の設定に応じて、このタイムスタンプは、データベースのタイムゾーンとは異なる[!DNL Commerce Intelligence]のレポートタイムゾーンに変換される場合があります |
| `customer_email` | 注文する顧客の電子メールアドレス。 ゲストチェックアウトを通じて処理された注文を含め、あらゆる状況で収集されます |
| `customer_group_id` | `customer_group` テーブルに関連付けられている外部キー。 `customer_group.customer_group_id`に参加して、注文に関連付けられている顧客グループを決定します |
| `customer_id` | お客様が登録されている場合は、`Foreign key`が`customer_entity` テーブルに関連付けられます。 `customer_entity.entity_id`に参加して、注文に関連付けられている顧客属性を決定します。 ゲストチェックアウトを通じて注文が行われた場合、このフィールドは`NULL`です |
| `entity_id` （PK） | テーブルの一意のID。Commerce インスタンス内の他のテーブルへの結合で一般的に使用されます |
| `increment_id` | 注文の一意のIDで、Adobe Commerce内では一般的に`order_id`と呼ばれます。 `increment_id`は、[!DNL Google Ecommerce]などの外部ソースへの結合に最もよく使用されます |
| `shipping_address_id` | `sales_order_address` テーブルに関連付けられている外部キー。 `sales_order_address.entity_id`に参加して、注文に関連付けられている配送先住所の詳細を決定します |
| `status` | 注文のステータス。 Commerce インスタンスに実装された「complete」、「processing」、「canceled」、「refunded」などの値を返すことができます。 注文が処理されるにつれて変更される可能性があります |
| `store_id` | `Foreign key`が`store` テーブルに関連付けられています。 `store`に参加しましょう。`store_id`は、どのCommerce ストアビューが注文に関連付けられているかを判断します |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Billing address city` | 注文の請求先です。 `sales_order`に参加することで計算されます。`billing_address_id` ～ `sales_order_address`。`entity_id`と`city` フィールドの返し |
| `Billing address country` | 注文の請求国コード。 `sales_order`に参加することで計算されます。`billing_address_id` ～ `sales_order_address`。`entity_id`と`country_id`を返しています |
| `Billing address region` | 注文の請求地域（最も頻繁には州または州）。 `sales_order`に参加することで計算されます。`billing_address_id` ～ `sales_order_address`。`entity_id`と`region` フィールドの返し |
| `Customer's first order date` | この顧客が最初に行った注文のタイムスタンプ。 顧客の「取得日」とみなされることがよくあります。 最小`sales_order`を返して計算しました。一意の顧客ごとに`created_at`個の値 |
| `Customer's first order's billing region` | 注文を行った顧客の購買請求地域。 顧客の最初の注文に関連付けられている`Billing address region`を返すことによって計算されます |
| `Customer's first order's coupon_code` | この注文を行った顧客の獲得クーポンコード。 顧客の最初の注文に関連付けられている`coupon_code`を返すことによって計算されます |
| `Customer's group code` | この注文を行った顧客のグループ名。 `sales_order`に参加することで計算されます。`customer_group_id` ～ `customer_group`。`customer_group_id`と`customer_group_code` フィールドの返し |
| `Customer's lifetime number of coupons` | この顧客が行ったすべての注文に適用されたクーポンの合計数量。 一意の顧客ごとに`coupon_code`が`NULL`以外の注文数をカウントして計算 |
| `Customer's lifetime number of orders` | この顧客による注文の合計数です。 一意の顧客ごとに`sales_order` テーブルの行数をカウントして計算 |
| `Customer's lifetime revenue` | この顧客が行ったすべての注文の収益の合計。 一意の顧客ごとに、すべての注文の`base_grand_total` フィールドを合計して計算します |
| `Customer's order number` | この顧客の注文に対する順序付き注文ランク。 顧客によって行われたすべての注文を識別し、`created_at` タイムスタンプで昇順に並べ替え、各注文に増分整数値を割り当てることで計算されます。 例えば、顧客の最初の注文は`Customer's order number` of 1を返し、顧客の2番目の注文は`Customer's order number` of 2を返します。 |
| `Customer's order number (previous-current)` | 顧客の前の注文のランクは、この注文のランクと連結され、`-`文字で区切られます。 （「`Customer's order number` - 1」）を「`-`」に続いて「`Customer's order number`」を連結して計算します。 例えば、顧客の2回目の購入に関連付けられた注文の場合、この列は`1-2`の値を返します。 2つの注文イベント間の時間を表す場合に最もよく使用されます（つまり、「注文の間の時間」グラフで） |
| `Is customer's last order?` | 注文が顧客の最後の注文と最新の注文のどちらに対応するかを指定します。 `Customer's order number`の値を`Customer's lifetime number of orders`と比較して計算しました。 これらの2つのフィールドが指定された順序に等しい場合、この列は`Yes`を返します。そうでない場合は`No`を返します |
| `Number of items in order` | 注文に含まれる品目の合計数量。 `sales_order`に参加することで計算されます。`entity_id` ～ `sales_order_item`。`order_id`と`sales_order_item`の合計。`qty_ordered` フィールド |
| `Seconds between customer's first order date and this order` | この注文と顧客の最初の注文との間の経過時間。 各注文の`Customer's first order date`から`created_at`を差し引いて計算し、秒数の整数値として返されます |
| `Seconds since previous order` | この注文と顧客の直前の注文との間の経過時間。 この注文の`created_at`から前の注文の`created_at`を減算して計算し、秒数の整数値として返されます。 例えば、顧客の3番目の注文に対応する注文レコードの場合、この列は、顧客の2番目の注文と3番目の注文の間の秒数を返します。 顧客の最初の注文の場合、このフィールドは`NULL`を返します |
| `Shipping address city` | 注文の配送先です。 `sales_order`に参加することで計算されます。`shipping_address_id` ～ `sales_order_address`。`entity_id`と`city` フィールドの返し |
| `Shipping address country` | 注文の配送国コード。 `sales_order`に参加することで計算されます。`Shipping_address_id` ～ `sales_order_address`。`entity_id`と`country_id`を返しています |
| `Shipping address region` | 注文の配送地域（最も頻繁には州または州）。 `sales_order`に参加することで計算されます。`shipping_address_id` ～ `sales_order_address`。`entity_id`と`region` フィールドの返し |
| `Store name` | この注文に関連付けられているCommerce ストアの名前。 `sales_order`に参加することで計算されます。`store_id` ～ `store`。`store_id`と`name` フィールドの返し |

## 共通指標

| **指標の名前** | **説明** | **建設** |
|---|---|---|
| `Avg order value` | 注文あたりの平均収益。収益は`base_grand_total`として定義されます | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | すべての顧客と注文の顧客（n-1）の注文からn番目の注文までの平均時間 | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | すべての税金と割引が適用される前に、GMVが小計として定義されるすべての注文の商品総額の合計 | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | すべての顧客と注文について、顧客（n-1）の注文からn番目の注文までの中央値 | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | 注文の合計数 | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | すべての注文の収益の合計。すべての税金、割引、配送などが適用された後、収益が顧客が支払った最終価格として定義されます | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | すべての注文の配送金額の合計 | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | すべての注文に適用される税金の合計 | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | 特定のレポート期間に注文を行ったユニーク顧客の数。 たとえば、レポートの間隔が週単位の場合、1週間に少なくとも1回の注文をした各顧客は、その週に何回注文したかにかかわらず、1回だけカウントされます | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key`個の参加パス

`customer_entity`

* `customer_entity` テーブルに結合して、注文した顧客に関連付けられた新しい顧客レベルの列を作成します。
   * パス：`sales_order.customer_id` （多数） => `customer_entity.entity_id` （1つ）

`customer_group`

* `customer_group` テーブルに結合して、注文した顧客の顧客グループ名を返す列を作成します。
   * パス：`sales_order.customer_group_id` （多数） => `customer_group.customer_group_id` （1つ）

`sales_order_address`

* `sales_order_address` テーブルに結合して、注文に関連付けられた請求先と配送先を返す列を作成します。 請求または発送の詳細が必要かどうかに応じて、2つの参加パスが可能です。
   * パス：
      * 発送：`sales_order.shipping_address_id` （多数） => `sales_order_address.entity_id` （1件）
      * 請求：`sales_order.billing_address_id` （多数） => `sales_order_address.entity_id` （1件）

`store`

* `store` テーブルに結合して、注文に関連付けられたCommerce ストアに関連する詳細を返す列を作成します。
   * パス：`sales_order.store_id` （多数） => `store.store_id` （1つ）
