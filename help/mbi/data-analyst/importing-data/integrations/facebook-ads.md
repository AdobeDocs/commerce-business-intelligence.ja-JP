---
title: Facebook広告を接続
description: 広告費データを分析し、そのお金が効果的に使われているかどうかを確認する方法を学びます。
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/6TR559YyeTHT3KWl3oA4Bdnpr-HCowTXTTkvmP0I0tg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 313
ht-degree: 0%

---

# [!DNL Facebook Ads]を接続

>[!NOTE]
>
>[管理者権限](../../../administrator/user-management/user-management.md)が必要です。

![Facebook広告のロゴ &#x200B;](../../../assets/facebook-ads-logo.png)

調査を行い、広告を作成し、[!DNL Facebook]にキャンペーンを開始しました。 広告費のデータを分析し、そのお金が効果的に使われているかどうかを確認する必要があります。 広告費データを使用すると、キャンペーンから獲得したユーザーの広告コストと顧客生涯価値（CLV） [を組み合わせることで、](../../../data-analyst/analysis/roi-ad-camp.md) キャンペーン ROIを測定できます。

[!DNL Facebook Ad] データを[!DNL Commerce Intelligence]に接続するには、次の簡単な3 ステップの手順を実行します。

1. [&#x200B; [!DNL Facebook] を [!DNL Commerce Intelligence]のデータソースとして追加](#stepone)
1. [&#x200B; [!DNL Commerce Intelligence]  データへの [!DNL Facebook Ads]  アクセスを許可する](#steptwo)
1. [データを引き出す [!DNL Facebook Ads]  アカウントを選択](#stepthree)

## [!DNL Facebook]を[!DNL Commerce Intelligence]のデータソースとして追加 {#stepone}

1. [!DNL Facebook]統合を[!DNL Commerce Intelligence] アカウントに追加するには、`Connections`の下の&#x200B;**[!UICONTROL Manage Data** > **Integrations]** ページに移動します。
1. 右側にある「**[!UICONTROL Add Integration]**」をクリックします。
1. [!DNL Facebook] アイコンをクリックします。 これにより、[!DNL Facebook]認証ページが表示されます。
1. **[!UICONTROL Authorize]**&#x200B;をクリックします。

## [!DNL Commerce Intelligence] データへの[!DNL Facebook Ads] アクセスを許可する {#steptwo}

**[!DNL Facebook Authorize]**&#x200B;をクリックすると、小さなポップアップウィンドウが表示されます。

Commerce Intelligence![の](../../../assets/Facebook_Access_Popup.png)Facebook アクセス権限ダイアログ

次の一連の手順に従って、[!DNL Commerce Intelligence]がパブリック プロファイル、[!DNL Facebook Ads]および関連する統計からデータにアクセスできるようにします。 続行するには、次の手順で&#x200B;**[!UICONTROL OK]**&#x200B;をクリックします。

## データを取得する[!DNL Facebook Ads] アカウントを選択 {#stepthree}

1. 認証が完了すると、データを取得する[!DNL Facebook Ads] アカウントを選択するように求められます。 `Connect`列のチェックボックスをクリックして、目的のアカウントを選択します。

   ![Facebook広告アカウント選択インターフェイス &#x200B;](../../../assets/Facebook_Ad_Accounts.png)

1. **[!UICONTROL Save Connections]**&#x200B;をクリックします。

   接続が成功した場合、*接続が成功しました。* メッセージがページの上部に表示されます。

## 次のステップ？ {#next}

[!DNL Facebook]で[!DNL Google Analytics]件のキャンペーンを追跡していることを確認してください。 これにより、`utm\_campaign`の[!DNL Google Analytics] フィールドが[!DNL Facebook] キャンペーン用に正しく入力されます。

## 関連

* [統合を再認証しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [&#x200B; [!DNL Google Adwords]  アカウントを接続](../integrations/google-ecommerce.md)
* [&#x200B; [!DNL Google eCommerce]経由で注文の紹介ソースを追跡](../integrations/google-ecommerce.md)
* [データベース内のユーザー紹介ソースの追跡](../../analysis/google-track-user-acq.md)
* [データベース内のユーザーデバイス、ブラウザー、OS データの追跡](../../analysis/track-usr-dev-browser.md)
* [最も価値のある獲得ソースとチャネルの発見](../../analysis/most-value-source-channel.md)
* [広告キャンペーンのROIを高める](../../analysis/roi-ad-camp.md)
* [&#x200B; [!DNL Google Analytics] UTM アトリビューションの仕組み](../../analysis/utm-attributes.md)
