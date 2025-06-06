---
title: Zendesk のヘルプデスクレポート
description: 最も価値の高いリファラルチャネルについて説明します。
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# [!DNL Zendesk] のヘルプ デスク レポート

>[!NOTE]
>
>これは、`Pro` プラン上で新しいアーキテクチャを使用しているクライアントでのみ使用できます。 メインのツールバーから `Manage Data` を選択した後で「`Data Warehouse Views`」セクションを使用できる場合は、新しいアーキテクチャを使用できます。

[!DNL Zendesk] データをトランザクションデータベースと統合することは、顧客がセールスチームやカスタマーサクセスチームとどのようにやり取りしているかを深く理解するための優れた方法です。 また、サポートプラットフォームを使用している顧客のタイプを把握するのにも役立ちます。 このトピックでは、ダッシュボードを設定して、[!DNL Zendesk] のパフォーマンスに関する詳細なレポートを取得し、トランザクション顧客と結び付ける方法を示します。

開始する前に、[[!DNL Zendesk]](../integrations/zendesk.md) を接続します。 この分析には [ 高度な計算列 ](../../data-warehouse-mgr/adv-calc-columns.md) が含まれています。

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

## 計算される列

### 作成する列

* **`[!DNL Zendesk] user's`** テーブル
   * `User is agent? (Yes/No) `
   * &#x200B;
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`、`email`

      * `SQL Calculation` `- case when `A` is not `null` and `A!=`end-user` 次に、`B` が `null` でない場合は `Yes` を `B` し、`%@magento.com` のような場合は `Yes` を `No` します

      * `@magento.com` をお使いのドメインに置き換えます

      * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`** テーブル
   * 定義を選択：`Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * [!UICONTROL table] を選択：`[!DNL Zendesk] users`
   * [!UICONTROL column] を選択：`User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`** テーブル
   * 定義を選択：`Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[!DNL Zendesk] audits._id`

   * [!UICONTROL table] を選択：`[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * 定義を選択：`Exists`
   * [!UICONTROL table] を選択：`[!DNL Zendesk] audits_~_events`
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

   * [!UICONTROL table] を選択：`[!DNL Zendesk] users`
   * [!UICONTROL column] を選択：`email`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 定義を選択：`Joined Column`
   * [!UICONTROL table] を選択：`[!DNL Zendesk] users`
   * [!UICONTROL column] を選択：`role`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * 定義を選択：`Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[!DNL Zendesk] tickets.id`

   * [!UICONTROL table] を選択：`[!DNL Zendesk] audits`
   * [!UICONTROL column] を選択：`created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` が `solved = 1` に変更されました

   * 定義を選択：`Min`
   * [!UICONTROL table] を選択：`[!DNL Zendesk] audits`
   * [!UICONTROL column] を選択：`created_at`
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
      * `Column type` – 「同じテーブル/計算」

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` – 整数

* **`Ticket created_at (day of week)`**
   * &#x200B;
      * `Column type` – 「同じテーブル/計算」

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

     *`Datatype` - `String`

* **`customer_entity`** テーブル
   * 定義を選択：`Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.email`
   * &#x200B;

     [!UICONTROL One]: `customer_entity.email`

   * [!UICONTROL table] を選択：`[!DNL Zendesk] tickets`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * &#x200B;
      * `Column type` – 「同じテーブル/計算」

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` - `String`

* **`[!DNL Zendesk] Tickets`** テーブル
   * 定義を選択：`Joined Column`
   * [!UICONTROL table] を選択：`customer_entity`
   * [!UICONTROL column] を選択：`User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## 指標

* 新 **[!DNL Zendesk]いチケット**
   * `Tickets we count`

* **`[!DNL Zendesk] tickets`** のテーブル内
* このメトリックは、**カウント** を実行します。
* **`id`** 列
* **`created_at`** タイムスタンプで並べ替え
* [!UICONTROL Filter]:

* **[!DNL Zendesk]チケットを解決しました**
   * `Tickets we count`
   * ステータス `closed, solved`

* **`[!DNL Zendesk] tickets`** のテーブル内
* このメトリックは、**カウント** を実行します。
* **`id`** 列
* **`created_at`** タイムスタンプで並べ替え
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Distinct ユーザーがチケットを申請する**
   * `Tickets we count`

* **`[!DNL Zendesk] tickets`** のテーブル内
* このメトリックは **個別カウント** を実行します。
* **`requester_id`** 列
* **`created_at`** タイムスタンプで並べ替え
* [!UICONTROL Filter]:

* **[!DNL Zendesk]平均/チケット解決時間の中央値**
   * `Tickets we count`
   * ステータス `closed, solved`

* **`[!DNL Zendesk] tickets`** のテーブル内
* この指標は、**平均（または中央値）** を実行します。
* **`Seconds to resolution`** 列
* **`created_at`** タイムスタンプで並べ替え
* [!UICONTROL Filter]:

* **[!DNL Zendesk]最初の応答までの平均/中央値の時間**
   * カウントされるチケット
   * ステータス IN がクローズ済み、解決済み

* **`[!DNL Zendesk] tickets`** のテーブル内
* この指標は、**平均（または中央値）** を実行します。
* **`Seconds to first response`** 列
* **`created_at`** タイムスタンプで並べ替え
* [!UICONTROL Filter]:

>[!NOTE]
>
>新しいレポートを作成する前に、必ず [ すべての新しい列をディメンションとして指標に追加する ](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) ようにしてください。

### レポート

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * ステータス `new, open, pending`

* 指標 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * ステータス `solved, closed`

* 指標 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* 指標 `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * ステータス `solved, closed`

* 指標 `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]: `New Tickets`

* 指標 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `status`
* `Chart Type`: `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`

   * [!UICONTROL Metric]: `New Tickets`

* 指標 `A`: `New tickets`
* 指標 `B`: `Solved tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* 指標 `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * ステータス `solved, closed`

* 指標 `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]: `Distinct users filing tickets`

* 指標 `A`: `Distinct users filing tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]: `New Tickets`

* 指標 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (day of week)`
* `Chart Type`: `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]:`New Tickets`

   * `Show top/bottom`: `Top 100% sorted by created_at (hour of the day)`

* 指標 `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (hour of the day)`
* `Chart Type`: `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 指標 `A`: `Average lifetime revenue`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * &#x200B;

     [!UICONTROL 指標]: Users

* 指標 `A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
