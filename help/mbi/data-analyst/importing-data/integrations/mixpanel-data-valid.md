---
title: Mixpanel でのデータの検証
description: Mixpanel 内で直接使用可能な同じデータをすべて同期したことを確認する方法を説明します。
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# でのデータ検証 `Mixpanel`

条件 [!DNL MBI] 最初に [!DNL Mixpanel] データを使用する場合、アカウントマネージャーまたはアナリストは、検証のために Mixpanel からのデータエクスポートを提供するように要求する場合があります。 これにより、以内で直接利用可能な同じデータをすべて同期したことを確認できます [!DNL Mixpanel].

## データの書き出しプロセス： `Events`

1. 次のサイトにアクセス： `Segmentation` セクションとビュー `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. 選択 `Past 96 Hours` 時間範囲

   ![](../../../assets/past-96-hours.png)

1. レポートの右下までスクロールし、 `.csv` ファイル：

   ![](../../../assets/export-csv-mixpanel.png)

1. を `.csv` ファイルを、この検証プロセスで作業しているアカウントマネージャーまたはアナリストに送信します。
