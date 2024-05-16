---
title: Zendesk に必要なデータ
description: Zendesk データに関する追加ドキュメントへのリンクなど、Zendesk からCommerce Intelligence に読み込めるメインデータテーブルについて説明します。
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 予測 [!DNL Zendesk] データ

後 [を接続しました [!DNL Zendesk] アカウント](../integrations/zendesk.md)を使用する場合は、 [Data Warehouse管理者](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 関連するデータフィールドを容易に追跡して分析できるようにする。

このトピックでは、インポート元となるメインのデータ テーブルについて説明します [!DNL Zendesk] 対象 [!DNL Adobe Commerce Intelligence]（に関する追加ドキュメントへのリンクを含む） [!DNL Zendesk] データ。

| テーブル名 | 説明 |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | この `Audits` テーブルには、ステータスの変更や顧客とエージェントの両方の応答など、チケットに関連付けられたアクティビティが記録されます。 このテーブルには、にリンクするチケット ID が含まれています `Tickets` テーブル。各チケットに対する最初の応答までの時間と解決までの時間を分析できます。 |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | この `audit_~\_events` テーブルは、の子です `audits` テーブルとレコードには、チケットイベントの追加の詳細が含まれます。 |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | この `Organizations` テーブルには、名前、ID、関連するドメイン名、タグ、カスタムフィールドなど、エンドユーザーに関する会社情報が記録されます。 |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | この `Tickets` テーブルには、次を含むすべてのチケット詳細が記録されます `created_at` タイムスタンプと `requester\_id` および `assignee\_id`でチケットをエンドユーザーおよびエージェントにリンクできます。 `Users` テーブルごとに。 |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | この `ticket fields` テーブルには、アカウントの基本的なテキストフィールドとカスタムチケットフィールドに関する情報が含まれています。 このテーブルの属性にはフィールドが含まれます `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`、エージェントおよびエンドユーザー固有の情報、作成および更新情報です。 |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | この `Users` 表には、エンドユーザーとエージェントに関するすべての詳細（個人の名前とメールを含む）が含まれます。 これにより、エンドユーザーのエンゲージメントとエージェントのパフォーマンスの両方を分析できます。 |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | グループは、Zendesk アカウントでエージェントを整理する方法です。 この `Groups` テーブルには、などの情報が記録されます `group ID`, `URL`, `name`、および作成と更新の情報です。 |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | マクロは、チケットのフィールドの値を変更する、ユーザーが定義したアクションです。 この表には、マクロのタイトル、ID、アクション、制限、作成および更新情報などの属性が含まれています。 |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | この `Tags` テーブルには、アカウント内のすべてのタグのリストが含まれています。 |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | このテーブルには、チケット指標に関するデータが含まれています。 次のフィールドがあります `ticket ID`, `URL`、グループ数、担当者、再開数、返信数、返信時間（分単位）、完全解決時間および最終更新（ステータス、担当者、依頼者など）に関する情報。 |

{style="table-layout:auto"}

## 関連

* [Zendesk への接続](../integrations/zendesk.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
