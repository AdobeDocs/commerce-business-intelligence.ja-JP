---
title: Mixpanel の接続
description: ユーザーが web サイトやアプリをどのように移動および使用するかを分析する方法について説明します。
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Connect [!DNL Mixpanel]

>[!NOTE]
>
>[ 管理者権限 ](../../../administrator/user-management/user-management.md) が必要です。

![](../../../assets/Mixpanel_logo.png)

[!DNL Mixpanel] を使用すると、ユーザーが web サイトやアプリをどのように移動および使用するかを分析できます。 ユーザー行動データを詳しく見ることで、設計と開発の意思決定がスマートになり、製品全体が向上します。 [!DNL Mixpanel] を [!DNL Commerce Intelligence] に接続すると、ユーザーの行動とその行動が収益にどのように変換されるかを分析できます。

[!DNL Mixpanel] データをに接続する [!DNL Commerce Intelligence]、簡単な 3 ステップのプロセスです。

1. [ [!DNL Commerce Intelligence] の場所で  [!DNL Mixpanel] credentials ページを開きます。](#stepone)
1. [API 資格情報  [!DNL Mixpanel]  取得](#steptwo)
1. [API 資格情報  [!DNL Mixpanel]  入力  [!DNL Commerce Intelligence]](#stepthree)

このプロセスを完了するには、2 つのブラウザーウィンドウまたはタブを開く必要があります。1 つは [!DNL Commerce Intelligence] 用で、もう 1 つは [!DNL Mixpanel] アカウント用です。

## [!DNL Mixpanel] 資格情報ページを開く {#stepone}

はじめに：

1. **[!DNL Manage Data** > **Connections]** の下の `Connections` ページに移動します。

1. `Data Sources` テーブルの上の画面の右側にある [**[!UICONTROL Add a New Source]**] をクリックします。

1. [!DNL Mixpanel] アイコンをクリックし、資格情報ページを開きます。

このページは開いたままにして、[!DNL Mixpanel] アカウントでブラウザーウィンドウに切り替えます。

## [!DNL Mixpanel] API 資格情報の取得 {#steptwo}

[!DNL Mixpanel] アカウントにまだログインしていない場合は、ログインしてから次の操作をおこないます。

1. 右上隅の「**[!UICONTROL Account]**」をクリックします。

1. 表示されたダイアログで、「**[!UICONTROL Projects]**」をクリックします。

1. API 資格情報の表示：

![Mixpanel API 資格情報の取得 ](../../../assets/Mixpanel_API_creds.png)

これを開いたままにしておきます。これを包み込む必要があります。

## [!DNL Commerce Intelligence] での [!DNL Mixpanel] API 資格情報の入力 {#stepthree}

1. `API Key` と `Secret` を [!DNL Commerce Intelligence] の [!DNL Mixpanel] 資格情報ページにコピーします。
1. 「**[!UICONTROL Connect to Mixpanel]**」をクリックして設定を完了します。

接続に成功した場合、_成功！メッセ_ ジがページの上部に表示されます。

### 関連

* [Expected [!DNL Mixpanel] data](../integrations/mixpanel-data.md)
* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
