---
title: 期待される[!DNL Google ECommerce] データ
description: Google ECommerceでどのような種類のデータが共有されるのかをご確認ください。
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/tGcSyz6DHcusK-RomMkRZoyY7acXb0dmXlHcc5pW7cg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
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
source-wordcount: 158
ht-degree: 0%

---

# [!DNL Google ECommerce] データが必要です

[!DNL Google ECommerce] アカウントが[!DNL Commerce Intelligence]に正常に接続されると、システムは`ecommerce`というタイトルのテーブルへのデータの読み込みを開始します。 このテーブルには、各トランザクションのデータ行が記録されます。 これには、次の順序レベルのデータ列が含まれます。

| 列名 | 説明 |
|-----|-----|
| `\_id` | この列はプライマリキーです。 |
| `accountId` | この列には、[!DNL Google Analytics] e コマースアカウントに関連付けられているアカウント IDが含まれています。 |
| `profileName` | この列には、[!DNL Google Analytics] プロファイル名が含まれています。 |
| `profileId` | この列には、[!DNL Google Analytics] プロファイル IDが含まれています。 |
| `socialNetwork` | この列には、ソーシャルネットワークの名前（[!DNL Facebook]や[!DNL YouTube]など）が含まれます |
| `campaign` | この列には、キャンペーン名（例：[`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)）が含まれます。 |
| `medium` | この列には、中程度の名前（[`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)など）が含まれます |
| `source` | この列には、ソース名が含まれます。 （例：[`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)） |
| `keyword` | この列には、キーワードの説明が含まれています（例：[`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)） |
| `transactionId` | この列には注文IDが含まれます。 これは、紹介データを注文データに結合するために使用されます。 |
| `updated\_at` | この列には、データ行が最後に更新された時刻が含まれます。 |

{style="table-layout:auto"}
