---
title: 接続Stripe
description: ビジネスの支払いと請求書データを管理および追跡する方法を説明します。
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 1%

---

# 接続 [!DNL Stripe]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

[!DNL Stripe] では、ビジネスの支払いと請求書データを管理および追跡できます。 接続 [!DNL Stripe] アカウント [!DNL Commerce Intelligence] は、簡単な 2 段階のプロセスです。

1. [追加 [!DNL Stripe] を [!DNL Commerce Intelligence]](#stepone)
1. [許可 [!DNL Commerce Intelligence] 次にアクセス： [!DNL Stripe] データ](#steptwo)

## 追加 [!DNL Stripe] データソースとして {#stepone}

1. 次に移動： `Connections` 下のページ **[!UICONTROL Admin** > **Connections]**.
1. クリック **[!UICONTROL Add a Data Source]**( 画面の右側、上の `Data Sources` 表。
1. 次をクリック： [!DNL Stripe] アイコン。 これにより、 `[!DNL Stripe] authorization` ページに貼り付けます。
1. クリック **[!UICONTROL Connect with Stripe]**.

## 許可 [!DNL Commerce Intelligence] 次にアクセス： [!DNL Stripe] データ {#steptwo}

クリック後 **[!UICONTROL Connect with Stripe]**&#x200B;に設定すると、アクセスリクエストページが表示されます。

1. クリック **[!UICONTROL Sign in with Stripe to Continue]**.

1. 資格情報を入力し、「 **[!UICONTROL Sign in to your account]**.

1. 資格情報が検証され、に戻ります。 [!DNL Commerce Intelligence].

1. 接続に成功した場合、 *接続に成功しました。* メッセージが画面の上部に表示されます。

## 関連：

The [[!DNL Stripe] API ドキュメント](https://stripe.com/docs/api) は、 [!DNL Stripe] は、 [!DNL Commerce Intelligence].

* [期待値 [!DNL Stripe] データ](../integrations/stripe-data.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
