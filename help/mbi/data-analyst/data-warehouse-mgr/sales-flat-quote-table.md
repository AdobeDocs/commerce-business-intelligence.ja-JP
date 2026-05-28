---
title: 見積もりテーブル
description: 見積もりテーブルの操作方法について説明します。
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/Q-46fusr2IS4ZQDrR8IjHEttueSBpT2-LQBtsejMEC4
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 613
ht-degree: 0%

---

# 見積もりテーブル

`quote` テーブル（M1の`sales_flat_quote`）には、ストアで作成されたすべてのショッピングカートに関するレコードが、放棄されたか購入に変換されたかにかかわらず含まれています。 各行は1つのカートを表します。 この表のサイズが大きくなる可能性があるため、Adobeでは、60日を超える未変換のカートがある場合など、特定の条件を満たす場合は、レコードを定期的に削除することをお勧めします。

>[!NOTE]
>
>過去のカートを分析することは、`quote` テーブルからレコードを削除しない場合にのみ可能です。 レコードを削除すると、まだデータベースから削除されていないカートのみが表示されます。

## 共通のネイティブ列

| **列名** | **説明** |
|---|---|
| `base_currency_code` | `base_*` フィールドにキャプチャされたすべての値の通貨（つまり、`base_grand_total`、`base_subtotal`など）。 これは通常、Commerce ストアのデフォルトの通貨を反映しています |
| `base_grand_total` | すべての税金、送料、割引が適用された後、カートの顧客に見積もられた最終価格。 正確な計算はカスタマイズ可能ですが、一般的に`base_grand_total`は`base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount`として計算されます |
| `base_subtotal` | 買い物かごに含まれるすべての商品の総商品価値。 税金、送料、割引などは含まれていません |
| `created_at` | カートの作成タイムスタンプ。ローカルでUTCに保存されます。 [!DNL Commerce Intelligence]の設定に応じて、このタイムスタンプは、データベースのタイムゾーンとは異なる[!DNL Commerce Intelligence]のレポートタイムゾーンに変換される場合があります |
| `customer_email` | カートを作成した顧客のメールアドレス |
| `customer_id` | お客様が登録されている場合は、`Foreign key`が`customer_entity` テーブルに関連付けられます。 `customer_entity.entity_id`に参加して、買い物かごを作成したユーザーに関連付けられている顧客属性を決定します。 カートがゲストチェックアウトを通じて作成された場合、このフィールドは`NULL`です |
| `entity_id` （PK） | テーブルの一意のID。Commerce インスタンス内の他のテーブルへの結合で一般的に使用されます |
| `is_active` | 買い物かごが顧客によって作成され、注文に変換されていない場合に「1」を返すブール型フィールド。 変換されたカート、または管理者を通じて作成されたカートの「0」を返します |
| `items_qty` | 買い物かごに含まれるすべての品目の合計数量の合計 |
| `reserved_order_id` | `Foreign key`が`sales_order` テーブルに関連付けられています。 `sales_order.increment_id`に参加して、変換済みのカートに関連付けられている注文の詳細を確認します。 変換済み注文に関連付けられていないカートの場合、`reserved_order_id`は`NULL`のままです |
| `store_id` | `Foreign key`が`store` テーブルに関連付けられています。 `store`に参加しましょう。`store_id` どのCommerce ストアビューがカートに関連付けられているかを判断するには |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Order date` | コンバージョンしたカートの注文作成日を反映したタイムスタンプ。 `quote.reserved_order_id`を`sales_order.increment_id`に結合し、`sales_order.created_at` フィールドを返すことによって計算されます |
| `Seconds between cart creation and order` | カート作成から注文作成までの時間。 `Order date`から`created_at`を減算して計算し、秒数の整数値として返されます |
| `Seconds since cart creation` | カートの作成日から現在までの経過時間。 クエリの実行時にサーバーのタイムスタンプから`created_at`を減算して計算し、整数の秒数で返します。 買い物かごの年齢を特定するために最もよく使用される |
| `Store name` | この注文に関連付けられているCommerce ストアの名前。 `quote.store_id`を`store.store_id`に結合し、`name` フィールドを返すことによって計算されます |

{style="table-layout:auto"}

## 共通指標

| **指標の名前** | **説明** | **建設** |
|---|---|---|
| `Number of abandoned carts` | 特定の「放棄」条件を満たすカートの数 | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/> フィルター：<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x。ここで、「x」は、カートを放棄したと見なされるまでの経過時間（秒単位）に対応します |
| `Avg time to cart conversion` | カート作成からコンバージョン済みカートの注文作成までの平均時間 | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | 放棄されたカートの潜在的な収益の合計。収益は`base_grand_total` フィールドとして定義されます | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br> フィルター：<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x。ここで、「x」は、買い物かごが放棄されたと見なされるまでの経過時間（秒単位）に対応します |

{style="table-layout:auto"}

## 外部キー結合パス

`customer_entity`

* `customer_entity` テーブルに結合して、買い物かごを作成した顧客に関連付けられた新しい顧客レベルの列を作成します。
   * パス：`quote.customer_id` （多数） => `customer_entity.entity_id` （1つ）

`sales_order`

* `sales_order` テーブルに結合して、変換済みのカートに関連付けられた注文の詳細を返す列を作成します。
   * パス：`quote.reserved_order_id` （多数） => `sales_order.increment_id` （1つ）

`store`

* `store` テーブルに結合して、カートに関連付けられているCommerce ストアに関連する詳細を返す列を作成します。
   * パス：`quote.store_id` （多数） => `store.store_id` （1つ）
