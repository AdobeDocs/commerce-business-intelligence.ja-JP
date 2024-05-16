---
title: Google Analyticsを接続
description: Google Analyticsと AEM を連携させる方法を学ぶ [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# 接続 [!DNL Google Analytics]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] は、インターネット上で最も広く使用されている web 分析サービスです。 実装 [!DNL Google Analytics] web サイトでは、訪問者によるサイトの使用方法、魅力的なコンテンツ、訪問者が離脱する場所などを追跡できます。 でのこれらの指標の分析 [!DNL Commerce Intelligence]は、他のデータと共に、サイトの全体的な正常性と操作性を向上させます。

基本を学ぶには [!DNL Google Analytics] への認証情報 [!DNL Commerce Intelligence]:

1. に移動 **[!UICONTROL Manage Data** > **Integrations]**.

1. クリック **[!UICONTROL Add Integration]**&#x200B;画面の右側にあります。

1. 「」をクリックします [!DNL Google Analytics] アイコン。 これにより、 [!DNL Google Analytics] 資格情報ページ。

1. を入力 [!DNL Google Analytics] 資格情報。 認証プロセスが完了すると、にリダイレクトされます。 [!DNL Commerce Intelligence].

1. プロファイル ID のリストが表示されます。 接続先のプロファイルを確認する [!DNL Commerce Intelligence]. 複数のプロファイルがあり、どちらを識別するかのヘルプが必要な場合は、複数のプロファイルの接続を参照してください [!DNL Google Analytics] 以下の「プロファイル」セクション：

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. 変更は自動的に保存されるため、 **接続に戻る** 完了したら、

## 複数のの接続 [!DNL Google Analytics] プロファイル

複数の web サイトが 1 つのサイトに接続されている場合があります [!DNL Google Analytics] アカウント（独自に識別） [!DNL Google Analytics] プロファイル ID。 この場合、すべてのプロファイル ID をに含めるオプションがあります [!DNL Commerce Intelligence]. プロファイル選択手順に含めるプロファイル ID を確認します。

特定の web サイトを識別するには [!DNL Google Analytics] プロファイル ID:

1. にログインします [!DNL Google Analytics]
1. 特定の Web サイトに移動 [!DNL Google Analytics] dashboard
1. URL を見ます。プロファイル ID は、次の 8 つの数値に対応しています `p` ラインの最後に：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 切断中 [!DNL Google Analytics] から [!DNL Commerce Intelligence] {#disconnect}

1. にアクセス [!DNL Google Analytics] [アカウント設定](https://accounts.google.com/) ページ。
1. の下 `Security` セクションで、をクリックします。 **[!UICONTROL edit]** 次の `Authorizing` アプリケーションとサイト。
1. クリック **[!UICONTROL revoke access]** 次の [!DNL Commerce Intelligence].

## 関連：

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [接続中 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Web サイトのアクティビティと顧客コンバージョン率の分析](../../analysis/web-act-cust-conversion.md)
* [を使用したユーザー獲得データの追跡 [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
