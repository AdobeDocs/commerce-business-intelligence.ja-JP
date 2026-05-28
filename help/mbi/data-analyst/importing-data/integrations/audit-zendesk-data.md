---
title: Zendesk データの監査
description: Zendesk データを書き出す手順について説明します。
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/EQmiSbzzvOONQ8-F1U9uMVpgXUKd2PEjcLXLVSgQSm8
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 306
ht-degree: 0%

---

# Zendesk データの監査

[[!DNL Zendesk]  データ &#x200B;](../integrations/exp-zendesk-data.md)で何か変なものを見つけましたか？ 課題を特定するには、データを分析する必要があります。 これは、[!DNL Zendesk] データをダウンロード可能なファイルに書き出すことによって実行できます。

## データ書き出しの有効化

データの書き出しは、現在[!DNL Zendesk] アカウントすべてに対して有効になっていません。 この機能を有効にするには、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)を送信し、[!DNL Zendesk] サブドメイン名を指定します。

>[!NOTE]
>
>現在、`Enterprise`と`Plus`のプランのみがこの機能にアクセスできます。

データの書き出しが有効になると、特定の電子メールドメインの管理者のみが[!DNL Zendesk] アカウントからデータを書き出すことができます。 この電子メールドメインは、通常、[!DNL Zendesk]と同じ電子メールドメインです。 アカウント所有者のメールドメインがデフォルトとして使用されますが、必要に応じてドメインを変更できます。

## ダウンロード可能なファイルへのエクスポート

1. サイドバーの管理アイコン （歯車のロゴ）をクリックし、**[!UICONTROL Manage** > **Reports]**&#x200B;を選択します。
1. 「**[!UICONTROL Export]**」タブをクリックします。
1. 次の画像に示すように、「**[!UICONTROL Request file]**」をクリックして、完全XML書き出しをクリックします。

   この時点でビルドが開始され、完了するとメールで通知されます。
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. メール通知のリンクをクリックして、レポートを含むzip ファイルをダウンロードします。

   このダウンロードリンクは少なくとも3日間有効です。

このプロセスでは、現在の[!DNL Zendesk] アカウントに保存されているすべての情報（コメント付き）、ユーザーデータ、アカウントデータを含むXML ファイルを作成します。 この時点で、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)を送信できます（このファイルを添付してください）。 そのため、データを詳しく見てみましょう。 ファイルが大きすぎる場合は、[!DNL Dropbox]または[!DNL Google Drive]を介して[!DNL Commerce Intelligence] チームと共有します。

[!DNL Zendesk] ファイルの書き出しについて詳しくは、公式の[[!DNL Zendesk] 書き出しドキュメント &#x200B;](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file)を参照してください。
