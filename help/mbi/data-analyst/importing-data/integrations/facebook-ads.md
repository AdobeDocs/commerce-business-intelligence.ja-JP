---
title: facebook Ads の接続
description: 広告費用データを分析し、お金が効果的に費やされているかどうかを確認する方法を説明します。
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# 接続 [!DNL Facebook Ads]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/facebook-ads-logo.png)

調査を行い、広告を作成し、キャンペーンを次の日に開始しました [!DNL Facebook]. 次に、広告費用データを分析し、お金が効果的に費やされているかどうかを確認します。 広告費用データを使用すると、次のことができます [広告コストと顧客生涯価値（CLV）を組み合わせて、キャンペーン ROI を測定します](../../../data-analyst/analysis/roi-ad-camp.md) キャンペーンから取得したユーザーの。

の接続 [!DNL Facebook Ad] データ送信先 [!DNL Commerce Intelligence] は、簡単な 3 ステップのプロセスです。

1. [追加 [!DNL Facebook] におけるデータソースとして [!DNL Commerce Intelligence]](#stepone)
1. [許可 [!DNL Commerce Intelligence] アクセス権限 [!DNL Facebook Ads] データ](#steptwo)
1. [を選択 [!DNL Facebook Ads] データを取り込むためのアカウント](#stepthree)

## 追加 [!DNL Facebook] におけるデータソースとして [!DNL Commerce Intelligence] {#stepone}

1. を追加します [!DNL Facebook] との統合 [!DNL Commerce Intelligence]アカウントで、に移動します `Connections` ページの下 **[!UICONTROL Manage Data** > **Integrations]**.
1. クリック **[!UICONTROL Add Integration]**&#x200B;右側にあります。
1. 「」をクリックします [!DNL Facebook] アイコン。 次が表示されます [!DNL Facebook] 認証ページ。
1. クリック **[!UICONTROL Authorize]**.

## 許可 [!DNL Commerce Intelligence] アクセス権限 [!DNL Facebook Ads] データ {#steptwo}

クリック後 **[!DNL Facebook Authorize]**&#x200B;小さなポップアップウィンドウが表示されます。

![](../../../assets/Facebook_Access_Popup.png)

次の一連の手順に従って、 [!DNL Commerce Intelligence] パブリック プロファイルのデータにアクセスするには [!DNL Facebook Ads] と、関連する統計です。 クリック **[!UICONTROL OK]** この手順を繰り返します。

## を選択 [!DNL Facebook Ads] データを取り込むためのアカウント {#stepthree}

1. 認証が完了すると、 [!DNL Facebook Ads] データの取り込み元のアカウント。 のチェックボックスをクリックして、目的のアカウントを選択します。 `Connect` 列。

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. クリック **[!UICONTROL Save Connections]**.

   接続に成功した場合、 *接続に成功しました。* メッセージがページの上部に表示されます。

## 次の手順 {#next}

を追跡していることを確認します [!DNL Facebook] のキャンペーン [!DNL Google Analytics]. これにより、 `utm\_campaign` のフィールド [!DNL Google Analytics] がユーザーに対して適切に設定されている [!DNL Facebook] キャンペーン。

## 関連

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [を接続 [!DNL Google Adwords] アカウント](../integrations/google-ecommerce.md)
* [以下を介した注文参照ソースの追跡 [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [データベース内のユーザー紹介ソースを追跡](../../analysis/google-track-user-acq.md)
* [データベース内のユーザーデバイス、ブラウザー、OS データの追跡](../../analysis/track-usr-dev-browser.md)
* [最も価値のある獲得ソースとチャネルを見つける](../../analysis/most-value-source-channel.md)
* [広告キャンペーンの ROI の向上](../../analysis/roi-ad-camp.md)
* [方法 [!DNL Google Analytics] UTM アトリビューションの仕組み](../../analysis/utm-attributes.md)
