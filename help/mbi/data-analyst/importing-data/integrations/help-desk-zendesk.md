---
title: Zendeskのヘルプデスクのレポート
description: 最も価値のある紹介チャネルの詳細。
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/2X87aaT7tJ-Rn6TK7g084p5OB-iML0vPaJlRUYAIesQ
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
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
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 390
ht-degree: 0%

---

# [!DNL Zendesk]のヘルプデスクのレポート

>[!NOTE]
>
>これは、`Pro` プランを使用しており、新しいアーキテクチャを使用しているクライアントでのみ使用できます。 メインツールバーから「`Manage Data`」を選択した後に「`Data Warehouse Views`」セクションを使用できる場合は、新しいアーキテクチャを使用しています。

[!DNL Zendesk] データをトランザクションデータベースと統合することは、顧客がセールス部門やカスタマーサクセス部門とどのように関わっているかを詳細に把握するための優れた方法です。 また、どのような顧客がサポートプラットフォームを利用しているのかを把握するのにも役立ちます。 このトピックでは、ダッシュボードを設定して、[!DNL Zendesk]のパフォーマンスに関する詳細なレポートを取得し、取引顧客と関連付ける方法を説明します。

開始する前に、[[!DNL Zendesk]](../integrations/zendesk.md)を接続する必要があります。 この分析には、[高度な計算列](../../data-warehouse-mgr/adv-calc-columns.md)が含まれています。

<!-- Getting Started -->

## はじめに

### 追跡する列

* `audits` テーブル
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` テーブル
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` テーブル
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` テーブル
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### 作成するフィルターセット

* `[!DNL Zendesk] Tickets` テーブル
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## 予定列

### 作成する列

* **`[!DNL Zendesk] user's`** テーブル
   * `User is agent? (Yes/No) `
   * &#x200B;
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `null` and `A!=`end-user`次に`Yes` （`B`が`null`ではなく`B`と`%@magento.com`と同じ）、`Yes`その他`No`終了

      * `@magento.com`をドメインに置き換えます

      * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`** テーブル
   * 定義を選択：`Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * [!UICONTROL table]を選択：`[!DNL Zendesk] users`
   * [!UICONTROL column]を選択：`User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`** テーブル
   * 定義を選択：`Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[!DNL Zendesk] audits._id`

   * [!UICONTROL table]を選択：`[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * 定義を選択：`Exists`
   * [!UICONTROL table]を選択：`[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[!DNL Zendesk] Tickets`** テーブル
   * 定義を選択：`Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * [!UICONTROL table]を選択：`[!DNL Zendesk] users`
   * [!UICONTROL column]を選択：`email`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 定義を選択：`Joined Column`
   * [!UICONTROL table]を選択：`[!DNL Zendesk] users`
   * [!UICONTROL column]を選択：`role`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 定義を選択：`Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[!DNL Zendesk] tickets.id`

   * [!UICONTROL table]を選択：`[!DNL Zendesk] audits`
   * [!UICONTROL column]を選択：`created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status`が`solved = 1`に変更されました

   * 定義を選択：`Min`
   * [!UICONTROL table]を選択：`[!DNL Zendesk] audits`
   * [!UICONTROL column]を選択：`created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * &#x200B;
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` マイナス `created_at`

* **`Seconds to first response`**
   * &#x200B;
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` マイナス `created_at`

* **`Requester's ticket number`**
   * &#x200B;
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * &#x200B;
      * `Column type` - 「同じテーブル >計算」

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` – 整数

* **`Ticket created_at (day of week)`**
   * &#x200B;
      * `Column type` - 「同じテーブル >計算」

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

     *`Datatype` - `String`

* **`customer_entity`** テーブル
   * 定義を選択：`Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.email`
   * &#x200B;
     [!UICONTROL One]: `customer_entity.email`

   * [!UICONTROL table]を選択：`[!DNL Zendesk] tickets`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * &#x200B;
      * `Column type` - 「同じテーブル >計算」

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` - `String`

* **`[!DNL Zendesk] Tickets`** テーブル
   * 定義を選択：`Joined Column`
   * [!UICONTROL table]を選択：`customer_entity`
   * [!UICONTROL column]を選択：`User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## 指標

* **[!DNL Zendesk]件の新規チケット**
   * `Tickets we count`

* **`[!DNL Zendesk] tickets`** テーブル内
* この指標は&#x200B;**カウント**&#x200B;を実行します
* **`id`**&#x200B;列
* **`created_at`** タイムスタンプで注文
* [!UICONTROL Filter]:

* **[!DNL Zendesk]件の解決済みチケット**
   * `Tickets we count`
   * `closed, solved`の状態

* **`[!DNL Zendesk] tickets`** テーブル内
* この指標は&#x200B;**カウント**&#x200B;を実行します
* **`id`**&#x200B;列
* **`created_at`** タイムスタンプで注文
* [!UICONTROL Filter]:

* **[!DNL Zendesk]人の個別ユーザーがチケットを提出**
   * `Tickets we count`

* **`[!DNL Zendesk] tickets`** テーブル内
* この指標は、**個数**&#x200B;を実行します
* **`requester_id`**&#x200B;列
* **`created_at`** タイムスタンプで注文
* [!UICONTROL Filter]:

* **[!DNL Zendesk]平均/中央値のチケット解決時間**
   * `Tickets we count`
   * `closed, solved`の状態

* **`[!DNL Zendesk] tickets`** テーブル内
* この指標は、**平均（または中央値）**&#x200B;を実行します
* **`Seconds to resolution`**&#x200B;列
* **`created_at`** タイムスタンプで注文
* [!UICONTROL Filter]:

* **[!DNL Zendesk]最初の応答までの平均/中央値**
   * カウントされるチケット
   * クローズ済み、解決済みのステータス

* **`[!DNL Zendesk] tickets`** テーブル内
* この指標は、**平均（または中央値）**&#x200B;を実行します
* **`Seconds to first response`**&#x200B;列
* **`created_at`** タイムスタンプで注文
* [!UICONTROL Filter]:

>[!NOTE]
>
>新しいレポートを作成する前に、必ず[すべての新しい列を指標](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md)にディメンションとして追加してください。

### レポート

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * `new, open, pending`の状態

* 指標`A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * `solved, closed`の状態

* 指標`A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* 指標`A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * `solved, closed`の状態

* 指標`A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]: `New Tickets`

* 指標`A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `status`
* `Chart Type`: `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`

   * [!UICONTROL Metric]: `New Tickets`

* 指標`A`: `New tickets`
* 指標`B`: `Solved tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* 指標`A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * `solved, closed`の状態

* 指標`A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]: `Distinct users filing tickets`

* 指標`A`: `Distinct users filing tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]: `New Tickets`

* 指標`A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (day of week)`
* `Chart Type`: `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]:`New Tickets`

   * `Show top/bottom`: `Top 100% sorted by created_at (hour of the day)`

* 指標`A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (hour of the day)`
* `Chart Type`: `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 指標`A`: `Average lifetime revenue`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * &#x200B;
     [!UICONTROL 指標]: Users

* 指標`A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
