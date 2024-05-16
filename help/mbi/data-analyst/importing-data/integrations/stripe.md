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

# 接続 [!DNL Stripe]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

[!DNL Stripe] を使用すると、ビジネスの支払いおよび請求書データを管理および追跡できます。 の接続 [!DNL Stripe] 移動先の口座 [!DNL Commerce Intelligence] は、簡単な 2 段階のプロセスです。

1. [追加 [!DNL Stripe] におけるデータソースとして [!DNL Commerce Intelligence]](#stepone)
1. [許可 [!DNL Commerce Intelligence] アクセス権限 [!DNL Stripe] データ](#steptwo)

## 追加 [!DNL Stripe] as a データソース {#stepone}

1. に移動します `Connections` ページの下 **[!UICONTROL Admin** > **Connections]**.
1. クリック **[!UICONTROL Add a Data Source]**&#x200B;画面右側の上部にある `Data Sources` テーブル。
1. 「」をクリックします [!DNL Stripe] アイコン。 次が表示されます `[!DNL Stripe] authorization` ページ。
1. クリック **[!UICONTROL Connect with Stripe]**.

## 許可 [!DNL Commerce Intelligence] アクセス権限 [!DNL Stripe] データ {#steptwo}

クリック後 **[!UICONTROL Connect with Stripe]**&#x200B;にアクセスをリクエストするページが表示されます。

1. クリック **[!UICONTROL Sign in with Stripe to Continue]**.

1. 認証情報を入力し、をクリックします **[!UICONTROL Sign in to your account]**.

1. 資格情報が検証され、に戻ります。 [!DNL Commerce Intelligence].

1. 接続に成功した場合、 *接続に成功しました。* メッセージが画面の上部に表示されます。

## 関連：

この [[!DNL Stripe] API ドキュメント](https://stripe.com/docs/api) は、方法の詳細を学習する際に役立つリソースです [!DNL Stripe] との統合 [!DNL Commerce Intelligence].

* [予測 [!DNL Stripe] データ](../integrations/stripe-data.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
