---
title: customer_entity テーブル
description: すべての登録済みアカウントのレコードにアクセスする方法を説明します。
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# customer_entity テーブル

この `customer_entity` テーブルには、すべての登録済みアカウントのレコードが含まれます。 アカウントがアカウントに新規登録された場合、購入を完了したかどうかに関係なく、そのアカウントが登録済みと見なされます。 各行は、そのアカウントの `entity_id`.

このテーブルには、ゲストチェックアウトで注文をした顧客のレコードは含まれません。 ストアがゲストによるチェックアウトを受け入れる場合、 [アカウント方法を学ぶ](../data-warehouse-mgr/guest-orders.md) を設定します。

## 共通列

| **列名** | **説明** |
|---|---|
| `created_at` | アカウントの登録日に対応するタイムスタンプ。通常はローカルの UTC に保存されます。 の設定に応じて、 [!DNL MBI]の場合、このタイムスタンプは [!DNL MBI] データベースのタイムゾーンと異なる |
| `email` | アカウントに関連付けられた電子メールアドレス |
| `entity_id` (PK) | テーブルの一意の識別子（ID の結合で一般的に使用） `customer_id` インスタンス内の他のテーブル内 |
| `group_id` | に関連付けられた外部キー `customer_group` 表。 結合先 `customer_group.customer_group_id` 登録済みアカウントに関連付けられている顧客グループを特定するには |
| `store_id` | に関連付けられた外部キー `store` 表。 結合先 `store`.`store_id` 登録されたアカウントに関連付けられているコマースストア表示を特定するには |

{style=&quot;table-layout:auto&quot;}

## 共通の計算列

| **列名** | **説明** |
|---|---|
| `Customer's first 30 day revenue` | 顧客の最初の注文日から 30 日以内にこの顧客が行ったすべての注文に対する売上高の合計。 結合によって計算 `customer_entity.entity_id` から `sales_order.customer_id` そして要約すると `base_grand_total` すべての注文のフィールド `sales_order.Seconds between customer's first order date and this order` ≤ 2592000（30 日の秒数） |
| `Customer's first order date` | この顧客が最初に発注した注文のタイムスタンプ。 結合によって計算 `customer_entity.entity_id` から `sales_order.customer_id` 最小値を返す `sales_order`.`created_at` 値 |
| `Customer's first order's billing region` | 顧客の最初の注文に関連付けられた請求地域。 結合によって計算 `customer_entity.entity_id` から `sales_order.customer_id` そして `Billing address region` 場所 `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | 顧客の最初の注文に関連付けられたクーポンコード。 結合によって計算 `customer_entity.entity_id` から `sales_order.customer_id` そして `sales_order.coupon_code` 場所 `sales_order.Customer's order number` = 1 |
| `Customer's group code` | 登録済み顧客のグループ名。 結合によって計算 `customer_entity.group_id` から `customer_group`.`customer_group_id` そして `customer_group_code` フィールド |
| `Customer's lifetime number of coupons` | この顧客がおこなったすべての注文に適用されたクーポンの合計数。 結合によって計算 `customer_entity.entity_id` から `sales_order.customer_id` また、 `sales_order.coupon_code` 等しくない `NULL` |
| `Customer's lifetime number of orders` | この顧客が行った注文の合計数。 結合によって計算 `customer_entity.entity_id` から `sales_order.customer_id` また、 `sales_order` 表 |
| `Customer's lifetime revenue` | この顧客が行ったすべての注文に関する売上高の合計。 結合によって計算 `customer_entity.entity_id` から `sales_order.customer_id` そして要約すると `base_grand_total` この顧客が行ったすべての注文のフィールド |
| `Seconds since customer's first order date` | 顧客の最初の注文日から今までの経過時間。 減算で計算 `Customer's first order date` クエリの実行時のサーバータイムスタンプから、整数の秒数で返されます。 |
| `Store name` | この登録済みアカウントに関連付けられたコマースストアの名前。 結合によって計算 `customer_entity.store_id` から `store.store_id` そして `name` フィールド |

{style=&quot;table-layout:auto&quot;}

## 一般的な指標

| **指標名** | **説明** | **構築** |
|---|---|---|
| `Avg first 30 day revenue` | 顧客の最初の注文から 30 日以内に行われた注文に対する顧客あたりの平均売上高 | 操作：平均<br/>オペランド： `Customer's first 30 day revenue`<br/>タイムスタンプ： `created_at`<br/>フィルター：<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000（初回注文から 30 日に達していない顧客を除く） |
| `Avg lifetime coupons` | 全期間で顧客ごとの注文に適用されたクーポンの平均数 | 操作：平均<br/>オペランド： `Customer's lifetime number of coupons`<br/>タイムスタンプ： `created_at` |
| `Avg lifetime orders` | 顧客の全期間における顧客あたりの平均注文数 | 操作：平均<br/>オペランド： `Customer's lifetime number of orders`<br/>タイムスタンプ： `created_at` |
| `Avg lifetime revenue` | 全期間におこなわれたすべての注文に対する、顧客あたりの平均合計売上高 | 操作：平均<br/>オペランド： `Customer's lifetime revenue`<br/>タイムスタンプ： `created_at` |
| `New customers` | 1 つ以上の注文を持つ顧客の数。最初の注文日にカウントされます。 登録したが決して注文しなかったアカウントを除外 | 操作：カウント<br/>オペランド： `entity_id`<br/>タイムスタンプ： `Customer's first order date` |
| `Registered accounts` | 登録されたアカウントの数。 アカウントが注文したかどうかに関係なく、すべての登録済みアカウントが含まれます | 操作：カウント<br/>オペランド： `entity_id`<br/>タイムスタンプ： `created_at` |

{style=&quot;table-layout:auto&quot;}

## 外部キー結合パス

`customer_group`

* 結合先 `customer_group` 登録済みアカウントの顧客グループ名を返す新しい列を作成するテーブル。
   * パス： `customer_entity.group_id` （多数） => `customer_group.customer_group_id` (1)

`store`

* 結合先 `store` 登録済みアカウントに関連付けられたストアに関連する詳細を返す新しい列を作成するためのテーブル。
   * パス： `customer_entity.store_id` （多数） => `store.store_id` (1)
