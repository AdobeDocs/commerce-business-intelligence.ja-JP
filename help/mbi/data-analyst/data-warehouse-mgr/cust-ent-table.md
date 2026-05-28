---
title: customer_entity テーブル
description: 登録したすべてのアカウントのレコードにアクセスする方法を説明します。
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/iTzls4nEtW9ep-3s536ZnRCCr2TeMD6AsDecZc3Cdys
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
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
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 604
ht-degree: 0%

---

# customer_entity テーブル

`customer_entity` テーブルには、登録されたすべてのアカウントのレコードが含まれています。 購入を完了したかどうかに関係なく、アカウントに登録した場合、アカウントは登録されたとみなされます。 各行は、そのアカウントの`entity_id`によって識別される1つの一意の登録アカウントに対応します。

このテーブルには、ゲストチェックアウトを介して注文した顧客の記録は含まれません。 ストアがゲストチェックアウトを受け付けている場合は、これらの注文について[&#x200B; ゲスト注文のアカウント化方法](../data-warehouse-mgr/guest-orders.md)を参照してください。

## 共通の列

| **列名** | **説明** |
|---|---|
| `created_at` | アカウントの登録日に対応するタイムスタンプ。ローカルのUTCに保存されます。 [!DNL Commerce Intelligence]の設定に応じて、このタイムスタンプは、データベースのタイムゾーンとは異なる[!DNL Commerce Intelligence]のレポートタイムゾーンに変換される場合があります |
| `email` | アカウントに関連付けられている電子メールアドレス |
| `entity_id` （PK） | テーブルの一意の識別子。インスタンス内の他のテーブルの`customer_id`への結合で一般的に使用されます |
| `group_id` | `customer_group` テーブルに関連付けられている外部キー。 `customer_group.customer_group_id`に参加して、登録済みアカウントに関連付けられている顧客グループを決定します |
| `store_id` | `store` テーブルに関連付けられている外部キー。 `store`に参加しましょう。`store_id` 登録されたアカウントに関連付けられているCommerce ストアビューを判断するには |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Customer's first 30 day revenue` | お客様が最初の注文日から30日以内に行ったすべての注文の収益の合計。 `customer_entity.entity_id`を`sales_order.customer_id`に結合し、`sales_order.Seconds between customer's first order date and this order`が2592000い≤すべての注文の`base_grand_total` フィールドを合計して計算します（30日間の秒数） |
| `Customer's first order date` | この顧客が最初に行った注文のタイムスタンプ。 `customer_entity.entity_id`から`sales_order.customer_id`に参加し、最小`sales_order`を返すことによって計算されます。`created_at` 値 |
| `Customer's first order's billing region` | 顧客の最初の注文に関連付けられている請求地域。 `customer_entity.entity_id`を`sales_order.customer_id`に結合し、`Billing address region`を返すことによって計算されます（`sales_order.Customer's order number` = 1） |
| `Customer's first order's coupon_code` | 顧客の最初の注文に関連付けられたクーポンコード。 `customer_entity.entity_id`を`sales_order.customer_id`に結合し、`sales_order.coupon_code`を返すことによって計算されます（`sales_order.Customer's order number` = 1） |
| `Customer's group code` | 登録済み顧客のグループ名。 `customer_entity.group_id`から`customer_group`への参加で計算されました。`customer_group_id` `customer_group_code` フィールドを返しています |
| `Customer's lifetime number of coupons` | この顧客が行ったすべての注文に適用されたクーポンの合計数。 `customer_entity.entity_id`から`sales_order.customer_id`に参加し、`sales_order.coupon_code`が`NULL`ではない注文数をカウントして計算します |
| `Customer's lifetime number of orders` | この顧客による注文の合計数です。 `customer_entity.entity_id`を`sales_order.customer_id`に結合し、`sales_order` テーブルの行数をカウントして計算します |
| `Customer's lifetime revenue` | この顧客が行ったすべての注文の収益の合計。 `customer_entity.entity_id`に`sales_order.customer_id`を結合し、この顧客が行ったすべての注文の`base_grand_total` フィールドを合計して計算します |
| `Seconds since customer's first order date` | 顧客の最初の注文日から現在までの経過時間。 クエリの実行時にサーバーのタイムスタンプから`Customer's first order date`を減算して計算し、整数の秒数で返します |
| `Store name` | この登録済みアカウントに関連付けられているCommerce ストアの名前。 `customer_entity.store_id`を`store.store_id`に結合し、`name` フィールドを返すことによって計算されます |

{style="table-layout:auto"}

## 共通指標

| **指標の名前** | **説明** | **建設** |
|---|---|---|
| `Avg first 30 day revenue` | 顧客の最初の注文から30日以内に行われた注文の顧客あたりの平均収益 | 操作：平均<br/> オペランド：`Customer's first 30 day revenue`<br/> タイムスタンプ：`created_at`<br/> フィルター：<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 （最初の注文から30日に達していない顧客を除く） |
| `Avg lifetime coupons` | 顧客が生涯にわたって注文に適用したクーポンの平均数 | 操作：平均<br/> オペランド：`Customer's lifetime number of coupons`<br/> タイムスタンプ：`created_at` |
| `Avg lifetime orders` | 顧客が生涯にわたって行った平均注文数 | 操作：平均<br/> オペランド：`Customer's lifetime number of orders`<br/> タイムスタンプ：`created_at` |
| `Avg lifetime revenue` | 生涯にわたる全注文に対する顧客1人当たりの平均総売上 | 操作：平均<br/> オペランド：`Customer's lifetime revenue`<br/> タイムスタンプ：`created_at` |
| `New customers` | 1つ以上の注文がある顧客の数。最初の注文日にカウントされます。 登録はするものの、注文はしないアカウントを除く | 操作：Count<br/> オペランド：`entity_id`<br/> タイムスタンプ：`Customer's first order date` |
| `Registered accounts` | 登録されたアカウントの数。 アカウントが注文したかどうかに関係なく、すべての登録アカウントが含まれます | 操作：Count<br/> オペランド：`entity_id`<br/> タイムスタンプ：`created_at` |

{style="table-layout:auto"}

## 外部キー結合パス

`customer_group`

* `customer_group` テーブルに結合して、登録されたアカウントの顧客グループ名を返す列を作成します。
   * パス：`customer_entity.group_id` （多数） => `customer_group.customer_group_id` （1つ）

`store`

* `store` テーブルに結合して、登録済みアカウントに関連付けられているストアに関連する詳細を返す列を作成します。
   * パス：`customer_entity.store_id` （多数） => `store.store_id` （1つ）
