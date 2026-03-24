---
title: Mixpanelでのデータ検証
description: Mixpanel内で直接利用可能なすべての同じデータを同期したことを確認する方法について説明します。
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/D6qvHVgPX0WEbKZSYel4siWMLTu9BloFBQMTxXxnbY0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
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
source-wordcount: 134
ht-degree: 0%

---

# [!DNL Mixpanel]でのデータ検証

[!DNL Adobe Commerce Intelligence]が最初に[!DNL Mixpanel] データに接続すると、アカウントマネージャーまたはアナリストは、検証目的で[!DNL Mixpanel]からのデータ書き出しを提供するようリクエストする場合があります。 これにより、[!DNL Mixpanel]内で直接利用可能なすべての同じデータを同期したことを確認できます。

## データ書き出しプロセス：`Events`

1. `Segmentation` セクションにアクセスして`Your Top Events`を表示します。

   ![Mixpanel ダッシュボードで上位のイベントを表示](../../../assets/your-top-events.png)

1. 時間範囲の`Past 96 Hours`を選択

   過去96時間オプションを表示する![Mixpanel時間範囲セレクター](../../../assets/past-96-hours.png)

1. レポートの右下部分までスクロールして、`.csv` ファイルを書き出します。

   ![MixpanelのCSVへの書き出しオプション（メニュー](../../../assets/export-csv-mixpanel.png)）

1. この検証プロセスで作業しているアカウントマネージャーまたはアナリストに`.csv` ファイルを送信します。

