---
title: Mixpanel を接続
description: ユーザーが Web サイトやアプリをどのようにナビゲートし、使用しているかを分析する方法について説明します。
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# 接続 [!DNL Mixpanel]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

を使用 [!DNL Mixpanel]を使用すると、ユーザーが web サイトやアプリをどのようにナビゲートし、使用しているかを分析できます。 ユーザーの行動データを詳しく見ると、よりスマートな設計と開発の意思決定がおこなわれ、製品全体がより良くなります。 接続中 [!DNL Mixpanel] から [!DNL Commerce Intelligence] では、ユーザーの行動と、その行動が売上高にどのように影響するかを分析できます。

接続 [!DNL Mixpanel] データを [!DNL Commerce Intelligence] 簡単な 3 ステップのプロセス：

1. [を開きます。 [!DNL Mixpanel] 認証情報ページ [!DNL Commerce Intelligence]](#stepone)
1. [を取得する [!DNL Mixpanel] API 資格情報](#steptwo)
1. [を入力します。 [!DNL Mixpanel] での API 資格情報 [!DNL Commerce Intelligence]](#stepthree)

このプロセスを完了するには、2 つのブラウザーウィンドウまたはタブを開く必要があります (1 つは [!DNL Commerce Intelligence] そしてもう一つは君の [!DNL Mixpanel] アカウント。

## を開く [!DNL Mixpanel] 資格情報ページ {#stepone}

基本を学ぶ:

1. 次に移動： `Connections` 下のページ **[!DNL Manage Data** > **Connections]**.

1. クリック **[!UICONTROL Add a New Source]**( 画面の右側、上の `Data Sources` 表。

1. 次をクリック： [!DNL Mixpanel] アイコンと資格情報ページが開きます。

このページは開いたままにし、 [!DNL Mixpanel] アカウント。

## の取得 [!DNL Mixpanel] API 資格情報 {#steptwo}

ログインしていない場合は、 [!DNL Mixpanel] アカウントを作成し、次の手順を実行します。

1. クリック **[!UICONTROL Account]** をクリックします。

1. 表示されたダイアログで、 **[!UICONTROL Projects]**.

1. API 資格情報が表示されます。

![Mixpanel API 資格情報の取得](../../../assets/Mixpanel_API_creds.png)

これを開いたままにしておくと、これをまとめる必要があります。

## 次の項目に入ります： [!DNL Mixpanel] での API 資格情報 [!DNL Commerce Intelligence] {#stepthree}

1. をコピーします。 `API Key` および `Secret` に [!DNL Mixpanel] 認証情報ページ [!DNL Commerce Intelligence].
1. クリック **[!UICONTROL Connect to Mixpanel]** をクリックして設定を完了します。

接続に成功した場合、 _成功！_ メッセージがページの上部に表示されます。

### 関連

* [期待値 [!DNL Mixpanel] データ](../integrations/mixpanel-data.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
