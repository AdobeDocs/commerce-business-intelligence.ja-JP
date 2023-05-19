---
title: Zendesk を接続
description: ヘルプデスクのレポートをに統合する方法を説明します。 [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# 接続 [!DNL Zendesk]

>[!NOTE]
>
>必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

接続 [!DNL Zendesk] データを使用すると、ヘルプデスクのレポートを [!DNL Commerce Intelligence]. これにより、カスタマーサポートを最適化し、ヘルプデスクのパフォーマンスを収益と共に監視できます。

接続 [!DNL Zendesk] データは、次の 3 つの手順で構成される簡単なプロセスです。

1. [を開きます。 [!DNL Zendesk] 認証情報ページ [!DNL Commerce Intelligence]](#stepone)
1. [を [!DNL Zendesk] API トークン](#steptwo)
1. [を入力します。 [!DNL Zendesk] ログイン情報とトークン： [!DNL Commerce Intelligence]](#stepthree)

このプロセスを完了するには、2 つのブラウザーウィンドウまたはタブを開く必要があります。1 つは [!DNL Commerce Intelligence]、もう 1 つは [!DNL Zendesk] アカウント

## を開きます。 [!DNL Zendesk] 認証情報ページ [!DNL Commerce Intelligence] {#stepone}

1. 次に移動： `Integrations` 下のページ **[!UICONTROL Manage Data** > **&#x200B;データソース&#x200B;**/ **統合]**.
1. クリック **[!UICONTROL Add Integration]**：画面の右側にあります。
1. 次をクリック： [!DNL Zendesk] アイコン これにより、 [!DNL Zendesk] 認証情報ページ。

## を [!DNL Zendesk] API トークン {#steptwo}

1. ログインしているウィンドウ/タブ [!DNL Zendesk] アカウントで、画面の左下隅にある設定（歯車）アイコンをクリックします。
1. 次の場合に `Settings` メニュー表示、 `Channels` 」セクションに入力します。 クリック **[!UICONTROL API]** （この節を参照）。
1. 内 `Token Access` このページの「 」セクションで、「 」の横にあるチェックボックスをクリックします。 `Enabled`. アクティブな API トークンのリストが表示されます。
1. クリック **[!UICONTROL Add New Token]**.
1. プロンプトが表示されたら、トークンのラベルを入力します。 Adobeは、 `Commerce Intelligence`つまり、トークンを使用しているアプリケーションは一目でわかります。
1. クリック **[!UICONTROL Create]**.
1. API トークンが作成されます。 このトークンをコピーする。次の手順で使用します。

## 入力 [!DNL Zendesk] ログイン情報と API トークン： [!DNL Commerce Intelligence] {#stepthree}

1. を入力します。 [!DNL Zendesk] サイトのプレフィックスとログイン用の電子メール [!DNL Zendesk] 認証情報ページ [!DNL Commerce Intelligence].
1. API トークンを入力します。
1. クリック **[!UICONTROL Save & Connect]**. 接続に成功した場合、 *接続に成功しました。* メッセージが画面の上部に表示されます。

## 関連：

* [予測 [!DNL Zendesk] データ](../integrations/exp-zendesk-data.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
