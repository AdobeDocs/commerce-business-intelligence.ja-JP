---
title: Google Analyticsとの連携
description: Google Analyticsと [!DNL Commerce Intelligence]の連携について説明します。
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/wSR5SWYSfmNZkzp5QxTUwv6QSsynXYofmRkKbvMsohs
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080bid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 283
ht-degree: 0%

---

# [!DNL Google Analytics]を接続

>[!NOTE]
>
>[管理者権限](../../../administrator/user-management/user-management.md)が必要です。

![Google Analyticsのロゴ ](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics]は、インターネット上で最も広く使用されているWeb分析サービスです。 Web サイトに[!DNL Google Analytics]を実装すると、訪問者によるサイトの利用状況、魅力的なコンテンツ、訪問者の離脱などを追跡できます。 [!DNL Commerce Intelligence]でこれらの指標を他のデータと一緒に分析することで、サイトの全体的な健全性と使いやすさが向上します。

[!DNL Google Analytics]資格情報を[!DNL Commerce Intelligence]に入力して開始します。

1. **[!UICONTROL Manage Data** > **Integrations]**&#x200B;に移動します。

1. 画面の右側にある「**[!UICONTROL Add Integration]**」をクリックします。

1. [!DNL Google Analytics] アイコンをクリックします。 これにより、[!DNL Google Analytics]資格情報ページが開きます。

1. [!DNL Google Analytics]資格情報を入力してください。 認証プロセスが完了すると、次の場所にリダイレクトされます：[!DNL Commerce Intelligence]。

1. プロファイル IDのリストが表示されます。 [!DNL Commerce Intelligence]に接続するプロファイルを確認してください。 複数のプロファイルがあり、そのプロファイルを特定するヘルプが必要な場合は、以下の「複数の[!DNL Google Analytics] プロファイルの接続」セクションを参照してください。

   ![URL](../../../assets/list-profile-id.png)<!--{: width="600px"}-->にプロファイル IDが表示されているGoogle Analytics管理ページ

1. 変更は自動的に保存されるので、完了したら「**接続に戻る**」をクリックします。

## 複数の[!DNL Google Analytics] プロファイルを接続しています

1つの[!DNL Google Analytics] アカウントに複数のWeb サイトを接続している可能性があります。各Web サイトは、独自の[!DNL Google Analytics] プロファイル IDで識別されます。 この場合、すべてのプロファイル IDを[!DNL Commerce Intelligence]に含めるオプションがあります。 プロファイル選択手順に含めるプロファイル IDを確認します。

特定のweb サイトの[!DNL Google Analytics] プロファイル IDを識別するには：

1. [!DNL Google Analytics]にログイン
1. 特定のweb サイトの[!DNL Google Analytics] ダッシュボードに移動
1. URLを見てください – プロファイル IDは、行の末尾にある`p`に続く8つの数字に対応しています。

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## [!DNL Google Analytics]を[!DNL Commerce Intelligence]から切断しています {#disconnect}

1. [!DNL Google Analytics] [ アカウント設定](https://accounts.google.com/) ページにアクセスします。
1. 「`Security`」セクションで、**[!UICONTROL edit]** アプリケーションとサイトの横にある「`Authorizing`」をクリックします。
1. **[!UICONTROL revoke access]**&#x200B;の横にある[!DNL Commerce Intelligence]をクリックします。

## 関連：

* [統合を再認証しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [接続中 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [web サイトのアクティビティと顧客のコンバージョン率の分析](../../analysis/web-act-cust-conversion.md)
* [ [!DNL Google Analytics] Cookieを使用したユーザー獲得データの追跡](../../analysis/google-track-user-acq.md)
