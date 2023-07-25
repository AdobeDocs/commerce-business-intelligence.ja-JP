---
title: facebook Ads の接続
description: 広告費用のデータを分析し、お金が効果的に使われているかどうかを確認する方法を説明します。
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# 接続 [!DNL Facebook Ads]

>[!NOTE]
>
>必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/facebook-ads-logo.png)

あなたは調査を行い、広告を作成し、キャンペーンを開始しました [!DNL Facebook]. 次に、広告支出のデータを分析し、お金が効果的に使われているかどうかを確認する時間です。 広告費用データを使用すると、次のことができます。 [広告コストと顧客のライフタイムバリュー (CLV) を結び付けて、キャンペーンの ROI を測定します。](../../../data-analyst/analysis/roi-ad-camp.md) キャンペーンから取得したユーザー数を格納できます。

接続 [!DNL Facebook Ad] データを [!DNL Commerce Intelligence] は、次の 3 つの手順で構成される簡単なプロセスです。

1. [追加 [!DNL Facebook] を [!DNL Commerce Intelligence]](#stepone)
1. [許可 [!DNL Commerce Intelligence] の [!DNL Facebook Ads] データ](#steptwo)
1. [選択 [!DNL Facebook Ads] データを取り込むためのアカウント](#stepthree)

## 追加 [!DNL Facebook] を [!DNL Commerce Intelligence] {#stepone}

1. 次の手順で [!DNL Facebook] の [!DNL Commerce Intelligence]アカウントで、 `Connections` 下のページ **[!UICONTROL Manage Data** > **Integrations]**.
1. クリック **[!UICONTROL Add Integration]**（右側）
1. 次をクリック： [!DNL Facebook] アイコン これにより、 [!DNL Facebook] 認証ページ。
1. クリック **[!UICONTROL Authorize]**.

## 許可 [!DNL Commerce Intelligence] の [!DNL Facebook Ads] データ {#steptwo}

クリック後 **[!DNL Facebook Authorize]**&#x200B;を指定した場合、小さなポップアップウィンドウが表示されます。

![](../../../assets/Facebook_Access_Popup.png)

一連の手順に従って、 [!DNL Commerce Intelligence] 公開プロファイルからデータにアクセスするには [!DNL Facebook Ads] および、関連する統計。 クリック **[!UICONTROL OK]** をクリックして続行します。

## 選択 [!DNL Facebook Ads] データを取り込むためのアカウント {#stepthree}

1. 認証が完了すると、 [!DNL Facebook Ads] データを取り込むアカウント。 目的のアカウントを選択するには、 `Connect` 列。

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. クリック **[!UICONTROL Save Connections]**.

   接続に成功した場合、 *接続に成功しました。* メッセージがページの上部に表示されます。

## 次の手順 {#next}

追跡していることを確認します。 [!DNL Facebook] キャンペーン [!DNL Google Analytics]. これにより、 `utm\_campaign` ～に入る [!DNL Google Analytics] が [!DNL Facebook] キャンペーン。

## 関連

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [接続 [!DNL Google Adwords] アカウント](../integrations/google-ecommerce.md)
* [経由で注文のリファラルソースを追跡 [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [データベース内のユーザー参照元を追跡する](../../analysis/google-track-user-acq.md)
* [データベース内のユーザーデバイス、ブラウザー、OS データを追跡する](../../analysis/track-usr-dev-browser.md)
* [最も価値のある獲得ソースとチャネルを見つける](../../analysis/most-value-source-channel.md)
* [広告キャンペーンの ROI の向上](../../analysis/roi-ad-camp.md)
* [方法 [!DNL Google Analytics] UTM 属性は機能しますか？](../../analysis/utm-attributes.md)
