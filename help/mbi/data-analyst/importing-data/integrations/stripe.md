---
title: Stripeとの連携
description: ビジネスの支払いと請求書データを管理および追跡する方法について説明します。
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/S6-otAlCeS8aKQ6K-xZH2ZaqEjZ-ZZ6fMWXtFFafu6c
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 151
ht-degree: 0%

---

# [!DNL Stripe]を接続

>[!NOTE]
>
>[管理者権限](../../../administrator/user-management/user-management.md)が必要です。

![Stripeのロゴ ](../../../assets/stripe-logo.png)

[!DNL Stripe]を使用すると、ビジネスの支払いと請求書のデータを管理および追跡できます。 [!DNL Stripe] アカウントを[!DNL Commerce Intelligence]に接続するには、次の簡単な2 ステップの手順を実行します。

1. [ [!DNL Stripe] を [!DNL Commerce Intelligence]のデータソースとして追加](#stepone)
1. [ [!DNL Commerce Intelligence]  データへの [!DNL Stripe]  アクセスを許可](#steptwo)

## [!DNL Stripe]をデータソースとして追加 {#stepone}

1. `Connections`の下の&#x200B;**[!UICONTROL Admin** > **Connections]** ページに移動します。
1. **[!UICONTROL Add a Data Source]** テーブルの上の画面の右側にある「`Data Sources`」をクリックします。
1. [!DNL Stripe] アイコンをクリックします。 `[!DNL Stripe] authorization` ページが表示されます。
1. **[!UICONTROL Connect with Stripe]**&#x200B;をクリックします。

## [!DNL Commerce Intelligence] データへの[!DNL Stripe] アクセスを許可する {#steptwo}

**[!UICONTROL Connect with Stripe]**&#x200B;をクリックすると、アクセス要求ページが表示されます。

1. **[!UICONTROL Sign in with Stripe to Continue]**&#x200B;をクリックします。

1. 資格情報を入力し、**[!UICONTROL Sign in to your account]**&#x200B;をクリックします。

1. 資格情報が検証され、[!DNL Commerce Intelligence]に戻されます。

1. 接続が成功した場合、*接続が成功しました。* メッセージが画面の上部に表示されます。

## 関連：

[[!DNL Stripe] API ドキュメント ](https://stripe.com/docs/api)は、[!DNL Stripe]と[!DNL Commerce Intelligence]の統合方法の詳細を学ぶのに役立つリソースです。

* [期待される [!DNL Stripe]  データ](../integrations/stripe-data.md)
* [統合を再認証しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
