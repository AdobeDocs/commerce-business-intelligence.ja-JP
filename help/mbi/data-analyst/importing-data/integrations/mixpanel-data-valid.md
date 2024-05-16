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

# でのデータ検証 [!DNL Mixpanel]

条件 [!DNL Adobe Commerce Intelligence] 最初にに接続 [!DNL Mixpanel] データ、担当のアカウントマネージャーまたはアナリストは、次からのデータ書き出しを行うようリクエストする場合があります [!DNL Mixpanel] 検証の目的で使用します。 これにより、直接内で使用可能なすべての同じデータを同期したことを確認できます [!DNL Mixpanel].

## データの書き出しプロセス： `Events`

1. にアクセス `Segmentation` セクションとビュー `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. を選択 `Past 96 Hours` 時間範囲

   ![](../../../assets/past-96-hours.png)

1. レポートの右下部分までスクロールし、 `.csv` ファイル：

   ![](../../../assets/export-csv-mixpanel.png)

1. を送信 `.csv` この検証プロセスで使用するアカウント・マネージャまたはアナリストにファイルを送信します。
