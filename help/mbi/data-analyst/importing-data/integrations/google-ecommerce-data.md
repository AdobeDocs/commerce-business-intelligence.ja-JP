---
title: 予測[!DNL Google ECommerce]データ
description: Google E コマースと共有されるデータのタイプについて説明します。
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 3f16484f189f6b4a8b072d2e3514d2f170993d60
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# 予測 [!DNL Google ECommerce] データ

あなたの後で [!DNL Google ECommerce] アカウントがに正常に接続されました [!DNL Commerce Intelligence]を選択すると、システムがという名前のテーブルへのデータのインポートを開始します `ecommerce`. このテーブルは、各トランザクションのデータ行を記録します。 これには、次の順序レベルのデータ列が含まれます。

| 列名 | 説明 |
|-----|-----|
| `\_id` | この列はプライマリキーです。 |
| `accountId` | この列には、に関連付けられたアカウント ID が含まれています [!DNL Google Analytics] e コマースアカウント。 |
| `profileName` | この列には、が含まれます [!DNL Google Analytics] プロファイル名。 |
| `profileId` | この列には、が含まれます [!DNL Google Analytics] プロファイル ID。 |
| `socialNetwork` | この列にはソーシャルネットワークの名前が含まれます（例：） [!DNL Facebook]、または [!DNL YouTube]） |
| `campaign` | この列にはキャンペーン名が表示されます（例：） [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)）に設定します。 |
| `medium` | この列には、中程度の名前が含まれています（例： [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)） |
| `source` | この列にはソース名が含まれます。 （例： [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)） |
| `keyword` | この列には、キーワードの説明が含まれます（例：） [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)） |
| `transactionId` | この列には注文 ID が含まれています。 これは、リファラルデータを注文データに結合するために使用されます。 |
| `updated\_at` | この列には、データ行が最後に更新された時刻が含まれています。 |

{style="table-layout:auto"}
