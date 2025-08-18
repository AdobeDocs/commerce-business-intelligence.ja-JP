---
title: customer_entity テーブル
description: すべての登録済みアカウントのレコードにアクセスする方法を説明します。
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# customer_entity テーブル

`customer_entity` テーブルには、すべての登録済みアカウントのレコードが含まれています。 購入を完了したかどうかに関係なく、アカウントに新規登録した場合、アカウントは登録済みと見なされます。 各行は、アカウントの `entity_id` によって識別される 1 つの一意の登録済みアカウントに対応します。

このテーブルには、ゲストのチェックアウト経由で注文した顧客のレコードは含まれていません。 ストアがゲストのチェックアウトを受け入れる場合は、それらの注文について [ ゲスト注文のアカウントを作成する方法 ](../data-warehouse-mgr/guest-orders.md) を参照してください。

## 共通列

| **列名** | **説明** |
|---|---|
| `created_at` | アカウントの登録日に対応するタイムスタンプ。UTC でローカルに保存されます。 [!DNL Commerce Intelligence] での設定に応じて、このタイムスタンプはデータベースのタイムゾーンとは異な [!DNL Commerce Intelligence] レポートタイムゾーンに変換される場合があります |
| `email` | アカウントに関連付けられているメールアドレス |
| `entity_id` （PK） | テーブルの一意の ID で、インスタンス内の他のテーブルの `customer_id` への結合で一般的に使用されます |
| `group_id` | `customer_group` テーブルに関連付けられている外部キー。 `customer_group.customer_group_id` に参加して、登録済みアカウントに関連付けられている顧客グループを決定します |
| `store_id` | `store` テーブルに関連付けられている外部キー。 `store` に参加します。登録済みのアカウントに関連付けられているCommerce ストア表示を確認する `store_id` 法 |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Customer's first 30 day revenue` | 顧客の最初の注文日から 30 日以内にこの顧客によって行われたすべての注文の売上高の合計。 `customer_entity.entity_id` を `sales_order.customer_id` に結合し、`base_grand_total` が 2592000 を≤すすべての注文の `sales_order.Seconds between customer's first order date and this order` フィールドを合計することによって計算されます。これは 30 日間の秒数です |
| `Customer's first order date` | この顧客による最初の注文のタイムスタンプ。 `customer_entity.entity_id` を `sales_order.customer_id` に結合し、最小 `sales_order` を返すことによって計算されます。`created_at` 値 |
| `Customer's first order's billing region` | 顧客の初回注文に関連付けられた請求リージョン。 `customer_entity.entity_id` を `sales_order.customer_id` に結合し、`Billing address region` = 1 の `sales_order.Customer's order number` を返すことによって計算されます |
| `Customer's first order's coupon_code` | 顧客の最初の注文に関連付けられたクーポンコード。 `customer_entity.entity_id` を `sales_order.customer_id` に結合し、`sales_order.coupon_code` = 1 の `sales_order.Customer's order number` を返すことによって計算されます |
| `Customer's group code` | 登録済み顧客のグループ名。 `customer_entity.group_id` を `customer_group` に結合して計算されます。`customer_group_id` フィールドの `customer_group_code` び出しと返し |
| `Customer's lifetime number of coupons` | この顧客が行ったすべての注文に適用されたクーポンの合計数。 `customer_entity.entity_id` を `sales_order.customer_id` に結合し、`sales_order.coupon_code` が `NULL` しくない注文の数をカウントすることで計算されます |
| `Customer's lifetime number of orders` | この顧客が注文した注文の合計数。 `customer_entity.entity_id` を `sales_order.customer_id` に結合し、`sales_order` テーブルの行数をカウントすることによって計算されます |
| `Customer's lifetime revenue` | この顧客が行ったすべての注文の売上高の合計。 `customer_entity.entity_id` を `sales_order.customer_id` に結合し、この顧客によって行われたすべての注文の `base_grand_total` フィールドを合計することによって計算されます |
| `Seconds since customer's first order date` | 顧客の初回注文日から現在までの経過時間。 クエリの実行時にサーバーのタイムスタンプから `Customer's first order date` を引いて計算され、秒数の整数で返されます |
| `Store name` | この登録済みアカウントに関連付けられたCommerce ストアの名前。 `customer_entity.store_id` を `store.store_id` に結合し、`name` フィールドを返すことによって計算されます |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **建設** |
|---|---|---|
| `Avg first 30 day revenue` | 顧客からの最初の注文から 30 日以内に行われた注文に対する顧客あたりの平均売上高 | 操作：Average<br/>Operand: `Customer's first 30 day revenue`<br/>Timestamp: `created_at`<br/>Filters:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 （最初の注文から 30 日が経過していない顧客を除外） |
| `Avg lifetime coupons` | 顧客ごとの注文に適用された、有効期間の平均クーポン数 | 操作：平均 <br/> オペランド：`Customer's lifetime number of coupons`<br/> タイムスタンプ：`created_at` |
| `Avg lifetime orders` | 顧客が全期間に注文した平均数 | 操作：平均 <br/> オペランド：`Customer's lifetime number of orders`<br/> タイムスタンプ：`created_at` |
| `Avg lifetime revenue` | 顧客の有効期間を通じて行われたすべての注文に関する、顧客あたりの平均合計売上高 | 操作：平均 <br/> オペランド：`Customer's lifetime revenue`<br/> タイムスタンプ：`created_at` |
| `New customers` | 最初の注文日にカウントされた、注文が 1 つ以上ある顧客の数。 登録はしたが注文しないアカウントを除外 | 操作：カウント <br/> オペランド：`entity_id`<br/> タイムスタンプ：`Customer's first order date` |
| `Registered accounts` | 登録されたアカウントの数。 注文されたかどうかに関係なく、すべての登録済みアカウントが含まれます | 操作：カウント <br/> オペランド：`entity_id`<br/> タイムスタンプ：`created_at` |

{style="table-layout:auto"}

## 外部キー結合パス

`customer_group`

* テーブルに結合 `customer_group` て、登録済みアカウントの顧客グループ名を返す列を作成します。
   * パス：`customer_entity.group_id` （多） => `customer_group.customer_group_id` （1）

`store`

* テーブルに結合 `store` て、登録済みアカウントに関連付けられたストアに関連する詳細を返す列を作成します。
   * パス：`customer_entity.store_id` （多） => `store.store_id` （1）
