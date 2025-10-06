---
title: Stripeを接続
description: ビジネスの支払いと請求データを管理およびトラッキングする方法を説明します。
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 0%

---

# Connect [!DNL Stripe]

>[!NOTE]
>
>[&#x200B; 管理者権限 &#x200B;](../../../administrator/user-management/user-management.md) が必要です。

![Stripe ロゴ &#x200B;](../../../assets/stripe-logo.png)

[!DNL Stripe] を使用すると、ビジネスの支払いおよび請求書データを管理および追跡できます。 [!DNL Stripe] アカウントを [!DNL Commerce Intelligence] に接続する手順は、次のとおりです。

1. [&#x200B; [!DNL Stripe]  [!DNL Commerce Intelligence] データソースとして追加](#stepone)
1. [データへ  [!DNL Commerce Intelligence]  アクセス  [!DNL Stripe]  許可](#steptwo)

## [!DNL Stripe] をデータソースとして追加する {#stepone}

1. `Connections` の下の **[!UICONTROL Admin** > **Connections]** ページに移動します。
1. **[!UICONTROL Add a Data Source]** テーブルの上の画面の右側にある [`Data Sources`] をクリックします。
1. [!DNL Stripe] アイコンをクリックします。 `[!DNL Stripe] authorization` ページが表示されます。
1. 「**[!UICONTROL Connect with Stripe]**」をクリックします。

## [!DNL Commerce Intelligence] データへの [!DNL Stripe] アクセスを許可する {#steptwo}

「**[!UICONTROL Connect with Stripe]**」をクリックすると、アクセス要求ページが表示されます。

1. 「**[!UICONTROL Sign in with Stripe to Continue]**」をクリックします。

1. 認証情報を入力し、「**[!UICONTROL Sign in to your account]**」をクリックします。

1. 資格情報が検証され、[!DNL Commerce Intelligence] に戻ります。

1. 接続に成功した場合、「接続に成功しました *メッセ* ジが画面の上部に表示されます。

## 関連：

[[!DNL Stripe] API ドキュメント &#x200B;](https://stripe.com/docs/api) は、[!DNL Stripe] との統合方法の詳細を学習する際に役立 [!DNL Commerce Intelligence] リソースです。

* [Expected [!DNL Stripe] data](../integrations/stripe-data.md)
* [&#x200B; 統合の再認証 &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
