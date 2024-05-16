---
title: Zendesk データの監査
description: Zendesk データを書き出す手順を説明します。
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Zendesk データの監査

あなたの中に何か奇妙なものを見つけました [[!DNL Zendesk] データ](../integrations/exp-zendesk-data.md)? 問題を特定するには、データを調査する必要があります。 これを行うには、 [!DNL Zendesk] データをダウンロード可能なファイルに追加します。

## データの書き出しの有効化

データの書き出しは現在、一部ので有効になっていません [!DNL Zendesk] アカウント。 この機能を有効にするには、 [サポートチケットを送信](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)、に言及しています [!DNL Zendesk] サブドメイン名。

>[!NOTE]
>
>のみ `Enterprise` および `Plus` 現在、計画はこの機能にアクセスできます。

データの書き出しが有効になると、特定のメールドメインの管理者のみがユーザーの [!DNL Zendesk] アカウント。 通常、このメールドメインは、と同じメールドメインです。 [!DNL Zendesk]. アカウント所有者のメールドメインがデフォルトで使用されますが、必要に応じてドメインを変更できます。

## ダウンロード可能ファイルへのエクスポート

1. サイドバーの管理者アイコン（歯車ロゴ）をクリックし、次を選択します **[!UICONTROL Manage** > **Reports]**.
1. 「」をクリックします **[!UICONTROL Export]** タブ。
1. クリック **[!UICONTROL Request file]** 以下の画像に示すように、完全な XML 書き出しの横にあります。

   この時点でビルドが開始され、完了するとメールで通知されます。
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. メール通知に含まれているリンクをクリックして、レポートを含む zip ファイルをダウンロードします。

   このダウンロードリンクは少なくとも 3 日間有効です。

このプロセスは、現在の [!DNL Zendesk] アカウント（チケットデータ（コメント付き）、ユーザーデータ、アカウントデータを含む）。 この時点で、次のことができます [サポートチケットを送信](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) （必ずこのファイルを添付してください。） したがって、データを詳しく見ることができます。 ファイルが大きすぎる場合は、 [!DNL Commerce Intelligence] 次を使用してチーム： [!DNL Dropbox] または [!DNL Google Drive].

詳しくは、 [!DNL Zendesk] ファイルのエクスポートについては、公式のを参照してください。 [[!DNL Zendesk] ドキュメントを書き出し](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
