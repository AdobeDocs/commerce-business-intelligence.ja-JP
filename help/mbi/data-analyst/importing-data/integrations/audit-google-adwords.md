---
title: Google Adwords データの監査
description: Google Adwords データを書き出す手順について説明します。
exl-id: f619801f-e789-44ad-945e-268d430bf583
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/2M1Lo7m11aCB5GZrcnA7hQX1qqZ6DHPdAt9wesbfL98
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 135
ht-degree: 0%

---

# [!DNL Google Adwords] データの監査

[[!DNL Google Adwords]](../integrations/google-adwords.md)で何か変なものを見つけましたか？ 課題を特定するには、データを分析する必要があります。 これは、[!DNL Google Adwords] データを`.csv` ファイルに書き出すことによって実行できます。

1. 無料の[[!DNL Google Adwords] Editor](https://ads.google.com/home/tools/ads-editor/) アプリケーションをダウンロードしてインストールします。

1. インストールが完了したら、`Add Count` パネルで`Add/manage accounts`を選択します。

1. [!DNL Google Adwords] アカウント情報を入力してください。

1. アカウントが[!DNL Google Adwords] エディターに追加されたら、**[!UICONTROL File** > ** スプレッドシートの書き出し（CSV） **> **アカウント全体の書き出し]**&#x200B;を選択します

これにより、現在の`.csv` アカウントに保存されているすべての情報を含む[!DNL Google Adwords] ファイルが作成されます。 この時点で、[ サポートチケット ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)を送信します（必ずこのファイルを添付してください）。そうすると、データを詳細に確認できます。 ファイルが大きすぎる場合は、[!DNL Commerce Intelligence]または[!DNL Dropbox]を介して[!DNL Google Drive] チームと共有します。

[!DNL Google Adwords] `.csv` ファイルの書き出しについて詳しくは、公式[[!DNL Google Adwords]  ドキュメント ](https://support.google.com/google-ads/editor/answer/38657?hl=en)を参照してください。
