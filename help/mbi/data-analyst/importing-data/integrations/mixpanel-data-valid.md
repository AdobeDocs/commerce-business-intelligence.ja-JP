---
title: Mixpanel でのデータ検証
description: Mixpanel 内で直接使用可能な同じデータをすべて同期したことを確認する方法を説明します。
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# [!DNL Mixpanel] でのデータ検証

[!DNL Adobe Commerce Intelligence] が [!DNL Mixpanel] データに初めて接続する際、アカウントマネージャーまたはアナリストは、検証を目的として、[!DNL Mixpanel] からのデータ書き出しを提供するようリクエストする場合があります。 これにより、[!DNL Mixpanel] 内で直接使用可能な同じデータをすべて同期したことを確認できます。

## データ エクスポート プロセス：`Events`

1. `Segmentation` のセクションにアクセスして、`Your Top Events` を表示します。

   ![](../../../assets/your-top-events.png)

1. 時間範囲の `Past 96 Hours` を選択

   ![](../../../assets/past-96-hours.png)

1. レポートの右下部分までスクロールし、`.csv` ファイルを書き出します。

   ![](../../../assets/export-csv-mixpanel.png)

1. `.csv` ファイルを、この検証プロセスで使用しているアカウントマネージャーまたはアナリストに送信します。
