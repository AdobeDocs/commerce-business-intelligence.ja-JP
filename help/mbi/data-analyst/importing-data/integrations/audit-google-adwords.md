---
title: Google Adwords データの監査
description: Google Adwords データを書き出す手順を説明します。
exl-id: f619801f-e789-44ad-945e-268d430bf583
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# データ [!DNL Google Adwords] 監査

[[!DNL Google Adwords]](../integrations/google-adwords.md) に何か奇妙なものを見つけたの？ 問題を特定するには、データを調査する必要があります。 これを行うには、[!DNL Google Adwords] データを `.csv` ファイルに書き出します。

1. 無料の [[!DNL Google Adwords] Editor](https://ads.google.com/home/tools/ads-editor/) アプリケーションをダウンロードしてインストールします。

1. インストールが完了したら、`Add Count` のパネルで「`Add/manage accounts`」を選択します。

1. [!DNL Google Adwords] アカウント情報を入力します。

1. アカウントが [!DNL Google Adwords] Editor に追加されたら、**[!UICONTROL File** > **&#x200B; スプレッドシート（CSV）の書き出し） &#x200B;**/**アカウント全体の書き出し]** を選択します。

これにより、現在の `.csv` アカウントに保存されているすべての情報を含む [!DNL Google Adwords] ファイルがビルドされます。 この時点で、[ サポートチケット ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja) を送信します（必ずこのファイルを添付してください）。これにより、データを詳しく確認できます。 ファイルが大きすぎる場合は、[!DNL Commerce Intelligence] または [!DNL Dropbox] を使用して [!DNL Google Drive] チームと共有します。

[!DNL Google Adwords] ファイルの書き出 `.csv` について詳しくは、公式の [[!DNL Google Adwords]  ドキュメント ](https://support.google.com/google-ads/editor/answer/38657?hl=en) を参照してください。
