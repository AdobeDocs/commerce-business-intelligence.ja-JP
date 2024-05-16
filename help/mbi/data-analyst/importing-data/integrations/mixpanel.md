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

# 接続 [!DNL Mixpanel]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

（を使用） [!DNL Mixpanel]を使用すると、ユーザーが web サイトやアプリをどのように移動および使用するかを分析できます。 ユーザー行動データを詳しく見ることで、設計と開発の意思決定がスマートになり、製品全体が向上します。 接続中 [!DNL Mixpanel] 対象： [!DNL Commerce Intelligence] では、ユーザーの行動とその行動が収益にどのように変換されるかを分析できます。

の接続 [!DNL Mixpanel] データ送信先 [!DNL Commerce Intelligence] シンプルな 3 ステップのプロセス：

1. [を開きます [!DNL Mixpanel] の資格情報ページ [!DNL Commerce Intelligence]](#stepone)
1. [を取得する [!DNL Mixpanel] API 資格情報](#steptwo)
1. [を入力 [!DNL Mixpanel] の API 資格情報 [!DNL Commerce Intelligence]](#stepthree)

このプロセスを完了するには、次の目的で 2 つのブラウザーウィンドウまたはタブを開く必要があります [!DNL Commerce Intelligence] もう 1 つは [!DNL Mixpanel] アカウント。

## を開く [!DNL Mixpanel] 資格情報ページ {#stepone}

はじめに：

1. に移動します `Connections` ページの下 **[!DNL Manage Data** > **Connections]**.

1. クリック **[!UICONTROL Add a New Source]**&#x200B;画面右側の上部にある `Data Sources` テーブル。

1. 「」をクリックします [!DNL Mixpanel] アイコンと資格情報ページが開きます。

このページは開いたままにして、ブラウザーウィンドウに切り替えます（ [!DNL Mixpanel] アカウント。

## の取得 [!DNL Mixpanel] API 資格情報 {#steptwo}

をまだログインしていない場合は、 [!DNL Mixpanel] その場合は、次の操作を行ってください。

1. クリック **[!UICONTROL Account]** 右上隅

1. 表示されたダイアログで、 **[!UICONTROL Projects]**.

1. API 資格情報の表示：

![Mixpanel API 資格情報の取得](../../../assets/Mixpanel_API_creds.png)

これを開いたままにしておきます。これを包み込む必要があります。

## の入力 [!DNL Mixpanel] の API 資格情報 [!DNL Commerce Intelligence] {#stepthree}

1. をコピーします `API Key` および `Secret` を、に追加します。 [!DNL Mixpanel] の資格情報ページ [!DNL Commerce Intelligence].
1. クリック **[!UICONTROL Connect to Mixpanel]** をクリックして設定を完了します。

接続に成功した場合、 _成功しました。_ メッセージがページの上部に表示されます。

### 関連

* [予測 [!DNL Mixpanel] データ](../integrations/mixpanel-data.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
