---
title: Zendesk データが期待されます
description: Zendesk から MBI に読み込むことができる主なデータテーブルについて説明します。このテーブルには、Zendesk データに関する追加ドキュメントへのリンクも含まれます。
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# Zendesk データが期待されます

後 [接続しました [!DNL Zendesk] アカウント](../integrations/zendesk.md)を使用する場合、 [Data Warehouse管理](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 分析に関連するデータフィールドを容易に追跡する。

この記事では、インポート元となる主なデータテーブルを確認します。 [!DNL Zendesk] into [!DNL MBI]（に関する追加ドキュメントへのリンクを含む） [!DNL Zendesk] データ。

| テーブル名 | 説明 |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | この `Audits` テーブルは、ステータスの変更や、顧客とエージェントの応答の両方を含む、チケットに関連付けられたアクティビティを記録します。 このテーブルには、 `Tickets` 表：各チケットの最初の応答時間と解決までの時間を分析できます。 |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | この `audit_~\_events` テーブルは `audits` の表に、チケットイベントの追加の詳細を記録します。 |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | この `Organizations` テーブルには、名前、ID、関連するドメイン名、タグ、カスタムフィールドなど、エンドユーザーに関する会社情報が記録されます。 |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | この `Tickets` テーブルには、次を含むすべてのチケットの詳細が記録されます。 `created_at` タイムスタンプと `requester\_id` および `assignee\_id`: `Users` 表に含まれます。 |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | この `ticket fields` 「 」の表には、基本的なテキストフィールドと、アカウント内のカスタムチケットフィールドに関する情報が含まれています。 このテーブルの属性には、フィールドが含まれます `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`、エージェントおよびエンドユーザー固有の情報、および情報の作成と更新。 |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | この `Users` この表には、個人の名前や E メールなど、エンドユーザーとエージェントに関するすべての詳細が含まれています。 これにより、エンドユーザーの関与とエージェントのパフォーマンスの両方を分析できます。 |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | グループとは、Zendesk アカウントでエージェントがどのように整理されるかを指します。 この `Groups` テーブルには、次のような情報が記録されます。 `group ID`, `URL`, `name`、および情報の作成と更新。 |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | マクロは、チケットのフィールドの値を変更するユーザーが定義するアクションです。 このテーブルには、マクロのタイトル、ID、アクション、制限、作成および更新情報などの属性が含まれます。 |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | この `Tags` 表には、アカウントのすべてのタグのリストが含まれます。 |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | この表には、チケット指標に関するデータが含まれています。 フィールドには `ticket ID`, `URL`、およびグループ、担当者、再開、返信、返信時間（分単位）、全解決時間、最終更新（ステータス、担当者、要求者など）の情報の数です。 |

{style=&quot;table-layout:auto&quot;}

## 関連

* [Zendesk の接続](../integrations/zendesk.md)
* [統合の再認証](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
