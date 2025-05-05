---
title: Stripeを接続
description: ビジネスの支払いと請求データを管理およびトラッキングする方法を説明します。
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 0%

---

# Connect [!DNL Stripe]

>[!NOTE]
>
>[ 管理者権限 ](../../../administrator/user-management/user-management.md) が必要です。

![](../../../assets/stripe-logo.png)

[!DNL Stripe] を使用すると、ビジネスの支払いおよび請求書データを管理および追跡できます。 [!DNL Stripe] アカウントを [!DNL Commerce Intelligence] に接続する手順は、次のとおりです。

1. [ [!DNL Commerce Intelligence] [!DNL Stripe]  データソースとして追加](#stepone)
1. [データへ  [!DNL Commerce Intelligence]  アクセス  [!DNL Stripe]  許可](#steptwo)

## [!DNL Stripe] をデータソースとして追加する {#stepone}

1. **[!UICONTROL Admin** > **Connections]** の下の `Connections` ページに移動します。
1. `Data Sources` テーブルの上の画面の右側にある [**[!UICONTROL Add a Data Source]**] をクリックします。
1. [!DNL Stripe] アイコンをクリックします。 `[!DNL Stripe] authorization` ページが表示されます。
1. 「**[!UICONTROL Connect with Stripe]**」をクリックします。

## [!DNL Stripe] データへの [!DNL Commerce Intelligence] アクセスを許可する {#steptwo}

「**[!UICONTROL Connect with Stripe]**」をクリックすると、アクセス要求ページが表示されます。

1. 「**[!UICONTROL Sign in with Stripe to Continue]**」をクリックします。

1. 認証情報を入力し、「**[!UICONTROL Sign in to your account]**」をクリックします。

1. 資格情報が検証され、[!DNL Commerce Intelligence] に戻ります。

1. 接続に成功した場合、「接続に成功しました *メッセ* ジが画面の上部に表示されます。

## 関連：

[[!DNL Stripe] API ドキュメント ](https://stripe.com/docs/api) は、[!DNL Commerce Intelligence] との統合方法の詳細を学習する際に役立 [!DNL Stripe] リソースです。

* [Expected [!DNL Stripe] data](../integrations/stripe-data.md)
* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
