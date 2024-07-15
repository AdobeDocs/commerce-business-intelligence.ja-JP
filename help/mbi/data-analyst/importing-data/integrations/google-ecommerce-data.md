---
title: Expected[!DNL Google ECommerce]data
description: Google E コマースと共有されるデータのタイプについて説明します。
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 3f16484f189f6b4a8b072d2e3514d2f170993d60
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# 予期される [!DNL Google ECommerce] データ

[!DNL Google ECommerce] アカウントが [!DNL Commerce Intelligence] に正常に接続されると、システムによって `ecommerce` という名前のテーブルへのデータのインポートが開始されます。 このテーブルは、各トランザクションのデータ行を記録します。 これには、次の順序レベルのデータ列が含まれます。

| 列名 | 説明 |
|-----|-----|
| `\_id` | この列はプライマリキーです。 |
| `accountId` | この列には、[!DNL Google Analytics] e コマースアカウントに関連付けられたアカウント ID が含まれています。 |
| `profileName` | この列には、[!DNL Google Analytics] プロファイル名が表示されます。 |
| `profileId` | この列には、[!DNL Google Analytics] プロファイル ID が表示されます。 |
| `socialNetwork` | この列には、ソーシャルネットワークの名前（例：[!DNL Facebook]、[!DNL YouTube]）が表示されます |
| `campaign` | この列にはキャンペーン名が表示されます（例：[`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)）。 |
| `medium` | この列には、中程度の名前（例：[`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)）が含まれています |
| `source` | この列にはソース名が含まれます。 （例：[`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)）。 |
| `keyword` | この列には、キーワードの説明（例：[`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)）が含まれます |
| `transactionId` | この列には注文 ID が含まれています。 これは、リファラルデータを注文データに結合するために使用されます。 |
| `updated\_at` | この列には、データ行が最後に更新された時刻が含まれています。 |

{style="table-layout:auto"}
