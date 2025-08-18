---
title: Zendesk に必要なデータ
description: Zendesk データに関する追加ドキュメントへのリンクなど、Zendesk からCommerce Intelligenceに読み込むことができるメインデータテーブルについて説明します。
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# 予期される [!DNL Zendesk] データ

[ アカウントに接続  [!DNL Zendesk]  た ](../integrations/zendesk.md) 後、[Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) を使用して、関連するデータフィールドを簡単に追跡して分析できます。

このトピックでは、[!DNL Zendesk] から [!DNL Adobe Commerce Intelligence] に読み込むことができるメインのデータテーブルについて説明します。これには、データに関する追加ドキュメントへのリンク [!DNL Zendesk] 含まれます。

| テーブル名 | 説明 |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | `Audits` のテーブルには、ステータスの変更や、顧客とエージェントの両方の応答など、チケットに関連するアクティビティが記録されます。 このテーブルには、`Tickets` のテーブルにリンクするチケット ID が含まれています。このテーブルを使用すると、各チケットに対する最初の応答までの時間と解決までの時間を分析できます。 |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | `audit_~\_events` テーブルは `audits` テーブルの子であり、チケットイベントの追加の詳細を記録します。 |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | `Organizations` のテーブルには、名前、ID、関連するドメイン名、タグ、カスタムフィールドなど、エンドユーザーに関する会社情報が記録されます。 |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | `Tickets` テーブルは、`created_at` タイムスタンプ、`requester\_id` および `assignee\_id` を含むすべてのチケットの詳細を記録します。これにより、チケットをそれぞれ `Users` テーブルのエンドユーザーおよびエージェントにリンクできます。 |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | `ticket fields` の表には、アカウントの基本的なテキストフィールドとカスタムチケットフィールドに関する情報が含まれています。 このテーブルの属性には、フィールド `ID`、`URL`、`type`、`title`、`description`、`position`、`requirement setting`、エージェントおよびエンドユーザー固有の情報、作成および更新情報が含まれます。 |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | `Users` の表には、エンドユーザーとエージェントに関するすべての詳細（名前やメールアドレスなど）が含まれています。 これにより、エンドユーザーのエンゲージメントとエージェントのパフォーマンスの両方を分析できます。 |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | グループは、Zendesk アカウントでエージェントを整理する方法です。 `Groups` のテーブルには、`group ID`、`URL`、`name`、作成および更新に関する情報が記録されます。 |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | マクロは、チケットのフィールドの値を変更する、ユーザーが定義したアクションです。 この表には、マクロのタイトル、ID、アクション、制限、作成および更新情報などの属性が含まれています。 |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | `Tags` のテーブルには、アカウント内のすべてのタグのリストが含まれます。 |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | このテーブルには、チケット指標に関するデータが含まれています。 フィールドには、`ticket ID`、`URL`、グループ数、担当者、再開者、返信、返信時間（分単位）、完全解決時間、最終更新（ステータス、担当者、依頼者など）に関する情報が含まれます。 |

{style="table-layout:auto"}

## 関連

* [Zendesk への接続](../integrations/zendesk.md)
* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
