---
title: Mixpanelを接続
description: ユーザーがweb サイトとアプリをどのように操作し、使用するかを分析する方法について説明します。
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/ap-nWiPVnPSpvUT4uiimZ7iC4fiuKvKH0ZMVkOTDcK8
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 246
ht-degree: 0%

---

# [!DNL Mixpanel]を接続

>[!NOTE]
>
>[管理者権限](../../../administrator/user-management/user-management.md)が必要です。

![Mixpanel ロゴ &#x200B;](../../../assets/Mixpanel_logo.png)

[!DNL Mixpanel]を使用すると、ユーザーがweb サイトとアプリをどのように移動して使用するかを分析できます。 利用者の行動データを詳細に分析することで、よりスマートな設計および開発の意思決定が可能になり、製品全体が向上します。 [!DNL Mixpanel]を[!DNL Commerce Intelligence]に接続すると、ユーザーの行動とその行動が収益にどのように変換されるかを分析できます。

簡単な3 ステップのプロセスで[!DNL Mixpanel] データを[!DNL Commerce Intelligence]に接続します：

1. [&#x200B; [!DNL Mixpanel] で [!DNL Commerce Intelligence]資格情報ページを開きます](#stepone)
1. [&#x200B; [!DNL Mixpanel] API資格情報の取得](#steptwo)
1. [&#x200B; [!DNL Mixpanel] に [!DNL Commerce Intelligence]API資格情報を入力してください](#stepthree)

このプロセスを完了するには、[!DNL Commerce Intelligence]用と[!DNL Mixpanel] アカウント用の2つのブラウザーウィンドウまたはタブを開く必要があります。

## [!DNL Mixpanel]資格情報ページを開いています {#stepone}

今すぐはじめる：

1. `Connections`の下の&#x200B;**[!DNL Manage Data** > **Connections]** ページに移動します。

1. **[!UICONTROL Add a New Source]** テーブルの上の画面の右側にある「`Data Sources`」をクリックします。

1. [!DNL Mixpanel] アイコンをクリックし、資格情報ページを開きます。

このページを開いたままにして、[!DNL Mixpanel] アカウントでブラウザーウィンドウに切り替えます。

## [!DNL Mixpanel] API資格情報を取得しています {#steptwo}

まだ[!DNL Mixpanel] アカウントにログインしていない場合は、次の操作を行います。

1. 右上隅の&#x200B;**[!UICONTROL Account]**&#x200B;をクリックします。

1. 表示されたダイアログで、**[!UICONTROL Projects]**&#x200B;をクリックします。

1. API資格情報は次のように表示されます。

![Mixpanel API資格情報の取得](../../../assets/Mixpanel_API_creds.png)

このプレゼンテーションを開いたままにしておきます。

## [!DNL Mixpanel]に[!DNL Commerce Intelligence] API資格情報を入力しています {#stepthree}

1. `API Key`と`Secret`を[!DNL Mixpanel]の[!DNL Commerce Intelligence]資格情報ページにコピーします。
1. **[!UICONTROL Connect to Mixpanel]**&#x200B;をクリックして設定を完了します。

接続が成功した場合、_成功です。_ メッセージがページの上部に表示されます。

### 関連

* [期待される [!DNL Mixpanel]  データ](../integrations/mixpanel-data.md)
* [統合を再認証しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
