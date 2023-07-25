---
title: Mixpanel でのデータの検証
description: Mixpanel 内で直接使用できる同じデータをすべて同期したことを確認する方法を説明します。
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# でのデータ検証 [!DNL Mixpanel]

条件 [!DNL Adobe Commerce Intelligence] 最初に [!DNL Mixpanel] データを使用する場合、アカウントマネージャーまたはアナリストは、次の場所からデータエクスポートを提供するように要求できます： [!DNL Mixpanel] 検証の目的で使用します。 これにより、内で直接使用可能な同じデータをすべて同期したことを確認できます [!DNL Mixpanel].

## データの書き出しプロセス： `Events`

1. 次のサイトにアクセス： `Segmentation` セクションとビュー `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. 選択 `Past 96 Hours` 時間範囲

   ![](../../../assets/past-96-hours.png)

1. レポートの右下部分までスクロールし、 `.csv` ファイル：

   ![](../../../assets/export-csv-mixpanel.png)

1. を `.csv` ファイルを、この検証プロセスで作業しているアカウントマネージャーまたはアナリストに送信します。
