---
title: Zendeskへの接続
description: ' [!DNL Commerce Intelligence]でヘルプデスクのレポートを統合する方法について説明します。'
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KBUuqTDD9s3qXDktcV3RzLx4zxtAFwAkKPbsQE2YGtI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 270
ht-degree: 0%

---

# [!DNL Zendesk]を接続

>[!NOTE]
>
>[管理者権限](../../../administrator/user-management/user-management.md)が必要です。

![Zendesk ロゴ &#x200B;](../../../assets/Zendesk_logo.png)

[!DNL Zendesk] データを接続すると、[!DNL Commerce Intelligence]でヘルプデスクのレポートを統合できます。 これにより、カスタマーサポートを最適化し、売上とともにヘルプデスクのパフォーマンスを監視することができます。

[!DNL Zendesk] データの接続は、シンプルな3段階のプロセスです。

1. [&#x200B; [!DNL Commerce Intelligence]で [!DNL Zendesk] 資格情報ページを開きます](#stepone)
1. [&#x200B; [!DNL Zendesk] API トークンを取得](#steptwo)
1. [&#x200B; [!DNL Commerce Intelligence]に [!DNL Zendesk]  ログイン情報とトークンを入力してください](#stepthree)

このプロセスを完了するには、2つのブラウザーウィンドウまたはタブを開く必要があります（[!DNL Commerce Intelligence]用と[!DNL Zendesk] アカウント用のどちらか一方）。

## [!DNL Commerce Intelligence]で[!DNL Zendesk]資格情報ページを開く {#stepone}

1. **[!UICONTROL Manage Data** > **&#x200B; データソース &#x200B;**/**統合]**&#x200B;の下の`Integrations` ページに移動します。
1. 画面の右側にある「**[!UICONTROL Add Integration]**」をクリックします。
1. [!DNL Zendesk] アイコンをクリックします。 これにより、[!DNL Zendesk]資格情報ページが開きます。

## [!DNL Zendesk] API トークンを取得します {#steptwo}

1. [!DNL Zendesk] アカウントにログインしているウィンドウ/タブで、画面の左下隅にある設定（歯車）アイコンをクリックします。
1. `Settings` メニューが表示されたら、`Channels` セクションを見つけます。 このセクションの&#x200B;**[!UICONTROL API]**&#x200B;をクリックします。
1. このページの`Token Access` セクションで、`Enabled`の横にあるチェックボックスをクリックします。 アクティブなAPI トークンのリストが表示されます。
1. **[!UICONTROL Add New Token]**&#x200B;をクリックします。
1. プロンプトが表示されたら、トークンのラベルを入力します。 Adobeでは、`Commerce Intelligence`の使用を推奨しています。一目でどのアプリケーションがトークンを使用しているかがわかります。
1. **[!UICONTROL Create]**&#x200B;をクリックします。
1. API トークンが作成されます。 このトークンをコピーします。次のステップで使用します。

## [!DNL Zendesk]のログイン情報とAPI トークンを[!DNL Commerce Intelligence]に入力します {#stepthree}

1. [!DNL Commerce Intelligence]の[!DNL Zendesk]資格情報ページに[!DNL Zendesk] サイトのプレフィックスとログイン用メールを入力します。
1. API トークンを入力します。
1. **[!UICONTROL Save & Connect]**&#x200B;をクリックします。 接続が成功した場合、*接続が成功しました！* メッセージが画面の上部に表示されます。

## 関連：

* [期待される [!DNL Zendesk]  データ](../integrations/exp-zendesk-data.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
