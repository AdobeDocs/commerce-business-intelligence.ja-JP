---
title: 予想される Salesforce データ
description: Salesforce データでサポートされるオブジェクトとサポートされないオブジェクトについて説明します。
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# 予測 [!DNL Salesforce] データ

[次の期間の後 [!DNL Salesforce] 設定が完了しました](../integrations/salesforce.md)、各クエリ可能なテーブル [object](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm)  — 名前 `sf_/\{sobject-name}`  — がData Warehouseに作成されました。

>[!NOTE]
>
>各テーブルの構造（列）は、オブジェクトに含まれるフィールドに応じて異なります。

組織で使用可能なオブジェクトのリストを取得するには、 [!DNL Salesforce] [Get a List of Objects ドキュメント](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). オブジェクトのリストを作成したら、 [エンティティ関係図 (ERD) セクション](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) / [!DNL Salesforce] エンティティの相互関係を確認するドキュメント

## サポートされていないオブジェクト

現在、 [!DNL Salesforce] では、現在、API で次のオブジェクトを公開していません。

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
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
