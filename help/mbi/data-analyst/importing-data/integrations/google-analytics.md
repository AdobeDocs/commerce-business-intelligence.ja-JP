---
title: Google Analyticsを接続
description: Google Analyticsと  [!DNL Commerce Intelligence] を接続する方法を説明します。
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Connect [!DNL Google Analytics]

>[!NOTE]
>
>[&#x200B; 管理者権限 &#x200B;](../../../administrator/user-management/user-management.md) が必要です。

![Google Analytics ロゴ &#x200B;](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] は、インターネット上で最も広く使用されている web 分析サービスです。 Web サイトに [!DNL Google Analytics] を実装すると、訪問者によるサイトの使用方法、魅力的なコンテンツ、訪問者が離脱する場所などを追跡できます。 これらの指標を [!DNL Commerce Intelligence] で分析すると、他のデータと共に、サイトの全体的な正常性と操作性が向上します。

まず、[!DNL Google Analytics] の資格情報を [!DNL Commerce Intelligence] に入力します。

1. **[!UICONTROL Manage Data** > **Integrations]** に移動します。

1. 画面の右側にある「**[!UICONTROL Add Integration]**」をクリックします。

1. [!DNL Google Analytics] アイコンをクリックします。 これにより、[!DNL Google Analytics] 資格情報ページが開きます。

1. [!DNL Google Analytics] 資格情報を入力します。 認証プロセスが完了すると、[!DNL Commerce Intelligence] にリダイレクトされます。

1. プロファイル ID のリストが表示されます。 [!DNL Commerce Intelligence] に接続するプロファイルを確認します。 複数のプロファイルがあり、どれを識別するのかについてのヘルプが必要な場合は、以下の複数の [!DNL Google Analytics] プロファイルの接続の節を参照してください。

   ![URL にプロファイル ID が表示されているGoogle Analytics管理ページ &#x200B;](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. 変更は自動的に保存されるので、完了したら「**接続に戻る**」をクリックします。

## 複数の [!DNL Google Analytics] プロファイルの接続

1 つの [!DNL Google Analytics] アカウントに接続された複数の web サイトがあり、独自の [!DNL Google Analytics] プロファイル ID で識別されている場合があります。 この場合、すべてのプロファイル ID を [!DNL Commerce Intelligence] に含めるオプションがあります。 プロファイル選択手順に含めるプロファイル ID を確認します。

特定の web サイトの [!DNL Google Analytics] プロファイル ID を識別するには：

1. [!DNL Google Analytics] にログインします
1. 特定の web サイトの [!DNL Google Analytics] ダッシュボードに移動します
1. URL を見ます。プロファイル ID は、行の最後の `p` に続く 8 つの数値に対応しています。

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## [!DNL Google Analytics] を [!DNL Commerce Intelligence] から切断しています {#disconnect}

1. [!DNL Google Analytics] の [&#x200B; アカウント設定 &#x200B;](https://accounts.google.com/) ページにアクセスします。
1. 「`Security`」セクションで、「アプリケーションとサイト」の横にある「**[!UICONTROL edit]**」 `Authorizing` クリックします。
1. 「**[!UICONTROL revoke access]**」の横にある「[!DNL Commerce Intelligence]」をクリックします。

## 関連：

* [&#x200B; 統合の再認証 &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
* [接続  [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Web サイトのアクティビティと顧客コンバージョン率の分析](../../analysis/web-act-cust-conversion.md)
* [cookie を使用したユーザー取得デ  [!DNL Google Analytics]  タの追跡](../../analysis/google-track-user-acq.md)
