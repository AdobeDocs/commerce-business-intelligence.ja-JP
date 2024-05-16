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

# 監査 [!DNL Google Adwords] データ

～で何か奇妙なものを見つけた [[!DNL Google Adwords]](../integrations/google-adwords.md)? 問題を特定するには、データを調査する必要があります。 これを行うには、 [!DNL Google Adwords] データをに `.csv` ファイル。

1. 無料のをダウンロードしてインストールします [[!DNL Google Adwords] 編集者](https://ads.google.com/home/tools/ads-editor/) アプリケーション。

1. インストールが完了したら、 `Add Count` が含まれる `Add/manage accounts` パネル。

1. を入力 [!DNL Google Adwords] アカウント情報。

1. アカウントの追加後 [!DNL Google Adwords] エディター、選択 **[!UICONTROL File** > **&#x200B;スプレッドシートの書き出し（CSV）**> **アカウント全体のエクスポート]**

これにより、 `.csv` 現在のに保存されているすべての情報を含むファイル [!DNL Google Adwords] アカウント。 この時点で、 [サポートチケット](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) （必ずこのファイルを添付してください。） したがって、データを詳しく見ることができます。 ファイルが大きすぎる場合は、 [!DNL Commerce Intelligence] 次を使用してチーム： [!DNL Dropbox] または [!DNL Google Drive].

詳しくは、 [!DNL Google Adwords] `.csv` ファイルのエクスポートについては、公式のを参照してください。 [[!DNL Google Adwords] 詳細を見る](https://support.google.com/google-ads/editor/answer/38657?hl=en).
