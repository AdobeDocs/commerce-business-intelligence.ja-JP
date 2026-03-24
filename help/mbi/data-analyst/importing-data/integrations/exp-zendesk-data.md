---
title: 予想されるZendesk データ
description: Zendesk データに関する追加ドキュメントへのリンクなど、ZendeskからCommerce Intelligenceに読み込むことができる主なデータテーブルについて説明します。
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/0p4SOrpj7wM-y5j3CMpHTs7HpysB5znJu3jSNiVJ2YY
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 362
ht-degree: 0%

---

# [!DNL Zendesk] データが必要です

[&#x200B; アカウント  [!DNL Zendesk] を接続した後、](../integrations/zendesk.md)Data Warehouse Manager[を使用して、分析用の関連データフィールドを簡単に追跡できます。](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)

このトピックでは、[!DNL Zendesk]から[!DNL Adobe Commerce Intelligence]に読み込むことができる主なデータテーブルについて説明します。これには、[!DNL Zendesk] データに関する追加ドキュメントへのリンクが含まれます。

| テーブル名 | 説明 |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | `Audits` テーブルには、ステータスの変更や、顧客とエージェントの両方の応答など、チケットに関連付けられたアクティビティが記録されます。 このテーブルには、`Tickets` テーブルにリンクするチケット IDが含まれています。これにより、各チケットの最初の応答までの時間と解決までの時間を分析できます。 |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | `audit_~\_events` テーブルは`audits` テーブルの子であり、チケットイベントの追加の詳細を記録します。 |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | `Organizations` テーブルには、名前、ID、関連するドメイン名、タグ、カスタムフィールドなど、エンドユーザーに関する企業情報が記録されます。 |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | `Tickets` テーブルには、`created_at` タイムスタンプと`requester\_id`および`assignee\_id`を含むすべてのチケットの詳細が記録されます。これにより、チケットを`Users` テーブルのエンドユーザーとエージェントにそれぞれリンクできます。 |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | `ticket fields` テーブルには、アカウントの基本テキストフィールドとカスタムチケットフィールドに関する情報が含まれています。 このテーブルの属性には、フィールド `ID`、`URL`、`type`、`title`、`description`、`position`、`requirement setting`、エージェントおよびエンドユーザー固有の情報、作成および更新情報が含まれます。 |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | `Users` テーブルには、個人の名前と電子メールを含む、エンドユーザーとエージェントに関するすべての詳細が含まれています。 これにより、エンドユーザーのエンゲージメントとエージェントのパフォーマンスの両方を分析できます。 |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | グループとは、エージェントがZendesk アカウント内でどのように整理されるかです。 `Groups` テーブルには、`group ID`、`URL`、`name`および作成と更新の情報などの情報が記録されます。 |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | マクロは、チケットのフィールドの値を変更するユーザーによって定義されたアクションです。 このテーブルには、マクロのタイトル、ID、アクション、制限、作成および更新情報などの属性が含まれます。 |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | `Tags` テーブルには、アカウント内のすべてのタグのリストが含まれています。 |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | このテーブルには、チケット指標に関するデータが含まれています。 フィールドには、`ticket ID`、`URL`およびグループ数、担当者、再開数、返信、返信時間（分）、完全解決時間、最終更新日（ステータス、担当者、依頼者など）の情報が含まれます。 |

{style="table-layout:auto"}

## 関連

* [Zendeskの接続](../integrations/zendesk.md)
* [統合を再認証しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
