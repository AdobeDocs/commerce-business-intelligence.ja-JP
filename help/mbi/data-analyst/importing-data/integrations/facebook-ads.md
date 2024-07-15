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

# Connect [!DNL Facebook Ads]

>[!NOTE]
>
>[ 管理者権限 ](../../../administrator/user-management/user-management.md) が必要です。

![](../../../assets/facebook-ads-logo.png)

調査を行い、広告を作成し、[!DNL Facebook] でキャンペーンを開始しました。 次に、広告費用データを分析し、お金が効果的に費やされているかどうかを確認します。 広告費用データを使用すると、広告コストとキャンペーンから取得したユーザーの顧客生涯価値（CLV）を組み合わせて [ キャンペーン ROI を測定 ](../../../data-analyst/analysis/roi-ad-camp.md) できます。

[!DNL Facebook Ad] データを [!DNL Commerce Intelligence] に接続する手順は、次の 3 つです。

1. [ [!DNL Commerce Intelligence] [!DNL Facebook]  データソースとして追加](#stepone)
1. [デ  [!DNL Commerce Intelligence]  タへのアクセス  [!DNL Facebook Ads]  許可](#steptwo)
1. [データを取り込むための Select [!DNL Facebook Ads] Accounts](#stepthree)

## [!DNL Facebook] を [!DNL Commerce Intelligence] のデータソースとして追加する {#stepone}

1. [!DNL Facebook] 統合を [!DNL Commerce Intelligence] アカウントに追加するには、「**[!UICONTROL Manage Data** > **Integrations]**」の下の `Connections` ページに移動します。
1. 右側にある「**[!UICONTROL Add Integration]**」をクリックします。
1. [!DNL Facebook] アイコンをクリックします。 [!DNL Facebook] 認証ページが表示されます。
1. 「**[!UICONTROL Authorize]**」をクリックします。

## [!DNL Facebook Ads] データへの [!DNL Commerce Intelligence] アクセスを許可する {#steptwo}

**[!DNL Facebook Authorize]** をクリックすると、小さなポップアップウィンドウが表示されます。

![](../../../assets/Facebook_Access_Popup.png)

一連の手順に従って、[!DNL Commerce Intelligence] が公開プロファイル、[!DNL Facebook Ads] および関連する統計からデータにアクセスできるようにします。 続行するには、次の手順の **[!UICONTROL OK]** をクリックします。

## データを取り込む [!DNL Facebook Ads] アカウントを選択 {#stepthree}

1. 認証が完了すると、データを取り込む [!DNL Facebook Ads] アカウントを選択するように求められます。 `Connect` 列のチェックボックスをクリックして、目的のアカウントを選択します。

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. 「**[!UICONTROL Save Connections]**」をクリックします。

   接続に成功した場合、「接続に成功しました *メッセ* ジがページの上部に表示されます。

## 次の手順 {#next}

[!DNL Google Analytics] でキャンペーンをトラッキ [!DNL Facebook] グしていることを確認します。 これにより、[!DNL Google Analytics] の `utm\_campaign` フィールドが [!DNL Facebook] キャンペーン用に適切に設定されます。

## 関連

* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [アカウント  [!DNL Google Adwords]  接続](../integrations/google-ecommerce.md)
* [ [!DNL Google eCommerce] を介した注文リファラルソースの追跡](../integrations/google-ecommerce.md)
* [データベース内のユーザー紹介ソースを追跡](../../analysis/google-track-user-acq.md)
* [データベース内のユーザーデバイス、ブラウザー、OS データの追跡](../../analysis/track-usr-dev-browser.md)
* [最も価値のある獲得ソースとチャネルを見つける](../../analysis/most-value-source-channel.md)
* [広告キャンペーンの ROI の向上](../../analysis/roi-ad-camp.md)
* [ [!DNL Google Analytics] UTM アトリビューションの仕組み](../../analysis/utm-attributes.md)
