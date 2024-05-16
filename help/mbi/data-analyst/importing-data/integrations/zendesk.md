---
title: Zendesk に接続
description: でヘルプデスクレポートを統合する方法を説明します [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# 接続 [!DNL Zendesk]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

の接続 [!DNL Zendesk] データを使用すると、でヘルプデスクレポートを統合できます [!DNL Commerce Intelligence]. これにより、カスタマーサポートを最適化し、売上高と共にヘルプデスクのパフォーマンスを監視できます。

の接続 [!DNL Zendesk] データは、次の 3 つの簡単な手順で構成されます。

1. [を開きます [!DNL Zendesk] の資格情報ページ [!DNL Commerce Intelligence]](#stepone)
1. [を取得する [!DNL Zendesk] API トークン](#steptwo)
1. [を入力 [!DNL Zendesk] のログイン情報とトークン [!DNL Commerce Intelligence]](#stepthree)

このプロセスを完了するには、ブラウザーウィンドウまたはタブを 2 つ開く必要があります。1 つは以下に対応します [!DNL Commerce Intelligence]、他に [!DNL Zendesk] アカウント。

## を開きます [!DNL Zendesk] の資格情報ページ [!DNL Commerce Intelligence] {#stepone}

1. に移動します `Integrations` ページの下 **[!UICONTROL Manage Data** > **&#x200B;データソース&#x200B;**> **統合]**.
1. クリック **[!UICONTROL Add Integration]**&#x200B;画面の右側にあります。
1. 「」をクリックします [!DNL Zendesk] アイコン。 これにより、 [!DNL Zendesk] 資格情報ページ。

## を取得する [!DNL Zendesk] API トークン {#steptwo}

1. ログインしているウィンドウ/タブで、 [!DNL Zendesk] アカウントで、画面の左下にある「設定」（歯車）アイコンをクリックします。
1. いつ `Settings` メニューが表示されたら、 `Channels` セクション。 クリック **[!UICONTROL API]** この節を参照してください。
1. が含まれる `Token Access` このページのセクションで、の横にあるチェックボックスをクリックします。 `Enabled`. アクティブな API トークンのリストが表示されます。
1. クリック **[!UICONTROL Add New Token]**.
1. プロンプトが表示されたら、トークンのラベルを入力します。 Adobeでは、を使用することをお勧めします。 `Commerce Intelligence`トークンを使用しているアプリケーションを一目で確認できます。
1. クリック **[!UICONTROL Create]**.
1. API トークンが作成されます。 このトークンをコピーします。このトークンは、次の手順で使用します。

## Enter [!DNL Zendesk] へのログイン情報と API トークン [!DNL Commerce Intelligence] {#stepthree}

1. を入力 [!DNL Zendesk] のサイトのプレフィックスとログインメール [!DNL Zendesk] の資格情報ページ [!DNL Commerce Intelligence].
1. API トークンを入力します。
1. クリック **[!UICONTROL Save & Connect]**. 接続に成功した場合、 *接続に成功しました。* メッセージが画面の上部に表示されます。

## 関連：

* [予測 [!DNL Zendesk] データ](../integrations/exp-zendesk-data.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
