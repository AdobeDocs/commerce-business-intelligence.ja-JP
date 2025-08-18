---
title: Zendesk に接続
description: ' [!DNL Commerce Intelligence] でヘルプデスクレポートを統合する方法を説明します。'
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Connect [!DNL Zendesk]

>[!NOTE]
>
>[ 管理者権限 ](../../../administrator/user-management/user-management.md) が必要です。

![](../../../assets/Zendesk_logo.png)

[!DNL Zendesk] データを接続すると、[!DNL Commerce Intelligence] でヘルプ デスク レポートを統合できます。 これにより、カスタマーサポートを最適化し、売上高と共にヘルプデスクのパフォーマンスを監視できます。

[!DNL Zendesk] データの接続は、簡単な 3 ステップのプロセスで行うことができます。

1. [ [!DNL Zendesk]  の場所で  [!DNL Commerce Intelligence]credentials ページを開きます。](#stepone)
1. [API トークン  [!DNL Zendesk]  取得](#steptwo)
1. [ログイン情報  [!DNL Zendesk]  トークンを  [!DNL Commerce Intelligence] に入力します。](#stepthree)

このプロセスを完了するには、2 つのブラウザーウィンドウまたはタブを開く必要があります。1 つは [!DNL Commerce Intelligence] 用、もう 1 つは [!DNL Zendesk] アカウント用です。

## [!DNL Zendesk] の [!DNL Commerce Intelligence] 資格情報ページを開きます。 {#stepone}

1. `Integrations` データソース **[!UICONTROL Manage Data** > **/**&#x200B;統合 **の下の]** ページに移動します。
1. 画面の右側にある「**[!UICONTROL Add Integration]**」をクリックします。
1. [!DNL Zendesk] アイコンをクリックします。 これにより、[!DNL Zendesk] 資格情報ページが開きます。

## [!DNL Zendesk] API トークンの取得 {#steptwo}

1. [!DNL Zendesk] アカウントにログインしているウィンドウ/タブで、画面の左下にある設定（歯車）アイコンをクリックします。
1. `Settings` メニューが表示されたら、`Channels` セクションを見つけます。 このセクションの「**[!UICONTROL API]**」をクリックします。
1. このページの「`Token Access`」セクションで、「`Enabled`」の横にあるチェックボックスをクリックします。 アクティブな API トークンのリストが表示されます。
1. 「**[!UICONTROL Add New Token]**」をクリックします。
1. プロンプトが表示されたら、トークンのラベルを入力します。 Adobeでは、トークンを使用しているアプリケーションを一目で把握できるように、`Commerce Intelligence` を使用することをお勧めします。
1. 「**[!UICONTROL Create]**」をクリックします。
1. API トークンが作成されます。 このトークンをコピーします。このトークンは、次の手順で使用します。

## ログイン情報 [!DNL Zendesk]API トークンを [!DNL Commerce Intelligence] に入力します。 {#stepthree}

1. [!DNL Zendesk] の [!DNL Zendesk] 資格情報ページに [!DNL Commerce Intelligence] サイトのプレフィックスとログインメールを入力します。
1. API トークンを入力します。
1. 「**[!UICONTROL Save & Connect]**」をクリックします。 接続に成功した場合、「接続に成功しました *メッセ* ジが画面の上部に表示されます。

## 関連：

* [Expected [!DNL Zendesk] data](../integrations/exp-zendesk-data.md)
* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
