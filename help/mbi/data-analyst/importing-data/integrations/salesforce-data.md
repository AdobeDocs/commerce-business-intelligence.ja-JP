---
title: Salesforce の期待データ
description: Salesforce データでサポートされるオブジェクトとサポートされないオブジェクトについて説明します。
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# 予測 [!DNL Salesforce] データ

後 [[!DNL Salesforce] 設定](../integrations/salesforce.md) 完了（クエリ可能ごとに 1 つのテーブル） [オブジェクト](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm)  – 名前付き `sf_/\{sobject-name}`  – がData Warehouse内に作成されます。

>[!NOTE]
>
>各テーブルの構造（列）は、オブジェクトに含まれるフィールドに応じて異なります。

組織で使用できるオブジェクトのリストを取得するには、を参照してください。 [!DNL Salesforce] [オブジェクトのリストの取得に関するドキュメント](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). オブジェクトのリストを取得したら、 [ERD （Entity Relationship Diagram）セクション](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) 件中 [!DNL Salesforce] エンティティの相互関係を確認するドキュメント。

## サポートされていないオブジェクト

現在、 [!DNL Salesforce] は現在、次のオブジェクトを API で公開していません。

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [外部オブジェクトとは](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
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
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
