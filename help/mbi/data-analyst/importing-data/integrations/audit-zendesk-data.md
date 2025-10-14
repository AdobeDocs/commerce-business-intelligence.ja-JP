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

[[!DNL Zendesk] data](../integrations/exp-zendesk-data.md) に何か奇妙なものが見つかりましたか？ 問題を特定するには、データを調査する必要があります。 これを行うには、[!DNL Zendesk] データをダウンロード可能なファイルに書き出します。

## データの書き出しの有効化

現在、すべての [!DNL Zendesk] アカウントでデータの書き出しが有効になっているわけではありません。 この機能を有効にするには、[&#x200B; のサブドメイン名を示す &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja) サポートチケットを送信 [!DNL Zendesk] します。

>[!NOTE]
>
>現在、この機能にアクセスできるのは `Enterprise` と `Plus` のプランのみです。

データの書き出しが有効になると、特定のメールドメインの管理者のみが [!DNL Zendesk] アカウントからデータを書き出すことができます。 通常、このメールドメインは、[!DNL Zendesk] ーザーと同じメールドメインです。 アカウント所有者のメールドメインがデフォルトで使用されますが、必要に応じてドメインを変更できます。

## ダウンロード可能ファイルへのエクスポート

1. サイドバーの管理者アイコン（歯車ロゴ）をクリックし、「**[!UICONTROL Manage** > **Reports]**」を選択します。
1. 「**[!UICONTROL Export]**」タブをクリックします。
1. 次の画像に示すように、「完全な XML 書き出し」の横にある「**[!UICONTROL Request file]**」をクリックします。

   この時点でビルドが開始され、完了するとメールで通知されます。
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. メール通知に含まれているリンクをクリックして、レポートを含む zip ファイルをダウンロードします。

   このダウンロードリンクは少なくとも 3 日間有効です。

このプロセスは、チケットデータ（コメント付き）、ユーザーデータ、アカウントデータなど、現在の [!DNL Zendesk] アカウントに保存されているすべての情報を含む XML ファイルを構築します。 この時点で、[&#x200B; サポートチケットを送信 &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja) （必ずこのファイルを添付してください）できるので、データを詳しく確認できます。 ファイルが大きすぎる場合は、[!DNL Commerce Intelligence] または [!DNL Dropbox] を使用して [!DNL Google Drive] チームと共有します。

ファイルの書き出しについて詳 [!DNL Zendesk] くは、公式の [[!DNL Zendesk]  書き出しドキュメント &#x200B;](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file) を参照してください。
