---
title: 予想されるSalesforce データ
description: Salesforce データでサポートされているオブジェクトとサポートされていないオブジェクトについて説明します。
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/eBX3Y0luu60A8PSAF43H6O3fsYjJnSWzyIybSOcSELE
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
source-wordcount: 117
ht-degree: 0%

---

# [!DNL Salesforce] データが必要です

[[!DNL Salesforce] setup](../integrations/salesforce.md)が完了すると、クエリ可能な[&#x200B; オブジェクト &#x200B;](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) （`sf_/\{sobject-name}`という名前）ごとにテーブルがData Warehouseに作成されます。

>[!NOTE]
>
>各テーブルの構造（列）は、オブジェクトに含まれるフィールドによって異なります。

組織で使用可能なオブジェクトのリストを取得するには、[!DNL Salesforce] [&#x200B; オブジェクトのリストの取得に関するドキュメント &#x200B;](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm)を参照してください。 オブジェクトのリストを作成したら、[&#x200B; ドキュメントの](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) エンティティ関係図（ERD）セクション [!DNL Salesforce]を参照して、エンティティ同士がどのように関連付けられているかを確認します。

## サポートされていないオブジェクト

現在、[!DNL Salesforce]は現在、APIで次のオブジェクトを公開していません。

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [外部オブジェクトとは何ですか？](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
* `CollaborationGroupRecord`
* `ContentDocument`
* `ContentDocumentLink`
* `FeedItem`
* `FieldDefinition`
* `IdeaComment`
* `ListViewChartInstance`
* `Order`
* `PlatformAction`

* `KnowledgeArticleVersion`
* `NewsFeed`
* `RecentlyViewed`
* `TopicAssignment`
* `UserRecordAccess`
* `UserProfileFeed`
* `Vote`

## 関連：

* [接続中 [!DNL Salesforce]](../integrations/salesforce.md)
* [統合を再認証しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
