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

この `customer_entity` テーブルには、すべての登録済みアカウントのレコードが含まれています。 購入を完了したかどうかに関係なく、アカウントに新規登録した場合、アカウントは登録済みと見なされます。 各行は、アカウントで識別される 1 つの一意の登録済みアカウントに対応します `entity_id`.

このテーブルには、ゲストのチェックアウト経由で注文した顧客のレコードは含まれていません。 ストアがゲストのチェックアウトを許可する場合は、 [ゲストの注文のアカウントを作成する方法](../data-warehouse-mgr/guest-orders.md) その命令に対して。

## 共通列

| **列名** | **説明** |
|---|---|
| `created_at` | アカウントの登録日に対応するタイムスタンプ。UTC でローカルに保存されます。 での設定に応じて [!DNL Commerce Intelligence]、このタイムスタンプはのレポートタイムゾーンに変換される場合があります [!DNL Commerce Intelligence] データベースのタイムゾーンとは異なる |
| `email` | アカウントに関連付けられているメールアドレス |
| `entity_id` （PK） | テーブルの一意の ID で、 `customer_id` インスタンス内の他のテーブルの |
| `group_id` | に関連付けられた外部キー `customer_group` テーブル。 に参加 `customer_group.customer_group_id` 登録済みのアカウントに関連付けられている顧客グループを特定するには |
| `store_id` | に関連付けられた外部キー `store` テーブル。 に参加 `store`.`store_id` 登録済みアカウントに関連付けられているCommerce ストア表示を確認するには |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Customer's first 30 day revenue` | 顧客の最初の注文日から 30 日以内にこの顧客によって行われたすべての注文の売上高の合計。 結合によって計算 `customer_entity.entity_id` 対象： `sales_order.customer_id` を合計する `base_grand_total` すべての注文のフィールドに次の条件を満たす場合 `sales_order.Seconds between customer's first order date and this order` ≤ 2592000 （30 日間の秒数） |
| `Customer's first order date` | この顧客による最初の注文のタイムスタンプ。 結合によって計算 `customer_entity.entity_id` 対象： `sales_order.customer_id` 最小値を返します `sales_order`.`created_at` value |
| `Customer's first order's billing region` | 顧客の初回注文に関連付けられた請求リージョン。 結合によって計算 `customer_entity.entity_id` 対象： `sales_order.customer_id` およびを返します `Billing address region` ここで、 `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | 顧客の最初の注文に関連付けられたクーポンコード。 結合によって計算 `customer_entity.entity_id` 対象： `sales_order.customer_id` およびを返します `sales_order.coupon_code` ここで、 `sales_order.Customer's order number` = 1 |
| `Customer's group code` | 登録済み顧客のグループ名。 結合によって計算 `customer_entity.group_id` 対象： `customer_group`.`customer_group_id` およびを返します `customer_group_code` フィールド |
| `Customer's lifetime number of coupons` | この顧客が行ったすべての注文に適用されたクーポンの合計数。 結合によって計算 `customer_entity.entity_id` 対象： `sales_order.customer_id` 注文数をカウントする場合 `sales_order.coupon_code` 等しくない `NULL` |
| `Customer's lifetime number of orders` | この顧客が注文した注文の合計数。 結合によって計算 `customer_entity.entity_id` 対象： `sales_order.customer_id` および内の行数のカウント `sales_order` テーブル |
| `Customer's lifetime revenue` | この顧客が行ったすべての注文の売上高の合計。 結合によって計算 `customer_entity.entity_id` 対象： `sales_order.customer_id` を合計する `base_grand_total` この顧客が注文したすべてのフィールド |
| `Seconds since customer's first order date` | 顧客の初回注文日から現在までの経過時間。 引いて計算される `Customer's first order date` クエリ実行時のサーバーのタイムスタンプから、秒数の整数で返されます |
| `Store name` | この登録済みアカウントに関連付けられたCommerce ストアの名前。 結合によって計算 `customer_entity.store_id` 対象： `store.store_id` およびを返します `name` フィールド |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **建設** |
|---|---|---|
| `Avg first 30 day revenue` | 顧客からの最初の注文から 30 日以内に行われた注文に対する顧客あたりの平均売上高 | 操作：平均<br/>オペランド： `Customer's first 30 day revenue`<br/>タイムスタンプ： `created_at`<br/>フィルター：<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 （最初の注文から 30 日が経過していない顧客を除く） |
| `Avg lifetime coupons` | 顧客ごとの注文に適用された、有効期間の平均クーポン数 | 操作：平均<br/>オペランド： `Customer's lifetime number of coupons`<br/>タイムスタンプ： `created_at` |
| `Avg lifetime orders` | 顧客が全期間に注文した平均数 | 操作：平均<br/>オペランド： `Customer's lifetime number of orders`<br/>タイムスタンプ： `created_at` |
| `Avg lifetime revenue` | 顧客の有効期間を通じて行われたすべての注文に関する、顧客あたりの平均合計売上高 | 操作：平均<br/>オペランド： `Customer's lifetime revenue`<br/>タイムスタンプ： `created_at` |
| `New customers` | 最初の注文日にカウントされた、注文が 1 つ以上ある顧客の数。 登録はしたが注文しないアカウントを除外 | 操作：カウント<br/>オペランド： `entity_id`<br/>タイムスタンプ： `Customer's first order date` |
| `Registered accounts` | 登録されたアカウントの数。 注文されたかどうかに関係なく、すべての登録済みアカウントが含まれます | 操作：カウント<br/>オペランド： `entity_id`<br/>タイムスタンプ： `created_at` |

{style="table-layout:auto"}

## 外部キー結合パス

`customer_group`

* に参加 `customer_group` 登録済みアカウントの顧客グループ名を返す列を作成するテーブル。
   * パス： `customer_entity.group_id` （多） => `customer_group.customer_group_id` （1）

`store`

* に参加 `store` 登録済みアカウントに関連付けられたストアに関連する詳細を返す列を作成するテーブル。
   * パス： `customer_entity.store_id` （多） => `store.store_id` （1）
