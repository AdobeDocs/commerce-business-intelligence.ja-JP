---
title: 期待値[!DNL Google ECommerce]データ
description: Google E コマースと共有されるデータの種類を説明します。
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 3f16484f189f6b4a8b072d2e3514d2f170993d60
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# 期待値 [!DNL Google ECommerce] データ

次に [!DNL Google ECommerce] アカウントが次に正常に接続されました： [!DNL Commerce Intelligence]を指定した場合、システムは「 」というタイトルのテーブルへのデータのインポートを開始します。 `ecommerce`. このテーブルには、トランザクションごとに 1 つのデータ行が記録されます。 これには、次の順序レベルのデータ列が含まれます。

| 列名 | 説明 |
|-----|-----|
| `\_id` | この列はプライマリキーです。 |
| `accountId` | この列には、 [!DNL Google Analytics] e コマースアカウント。 |
| `profileName` | この列には、 [!DNL Google Analytics] プロファイル名。 |
| `profileId` | この列には、 [!DNL Google Analytics] プロファイル ID。 |
| `socialNetwork` | この列には、ソーシャルネットワークの名前が含まれます ( 例： [!DNL Facebook]または [!DNL YouTube]) |
| `campaign` | この列には、キャンペーン名 ( 例： [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)) をクリックします。 |
| `medium` | この列には、メディア名が含まれます ( 例： [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | この列には、ソース名が含まれます。 ( 例： [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | この列には、キーワードの説明が含まれます ( 例： [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | この列には、注文 ID が含まれます。 これは、紹介データを注文データに結合するために使用されます。 |
| `updated\_at` | この列には、データ行が最後に更新された日時が含まれます。 |

{style="table-layout:auto"}
