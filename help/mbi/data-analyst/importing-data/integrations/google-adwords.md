---
title: Google Adwordsとの連携
description: 広告コストと、キャンペーンから取得したユーザーの顧客生涯価値（CLV）を組み合わせて、キャンペーンのROIを測定する方法を説明します。
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/mZ8R2vPyFy8pGpYi4KhqocVnP-OlgMPGU3KJ4C9vsTo
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 322
ht-degree: 0%

---

# [!DNL Google Adwords]を接続

>[!NOTE]
>
>[管理者権限](../../../administrator/user-management/user-management.md)が必要です。

![Google AdWords ロゴ &#x200B;](../../../assets/Google_Adwords_logo.png)

調査を行い、広告を作成し、[!DNL Google] キャンペーンを開始しました。 広告費のデータを分析し、そのお金が効果的に使われているかどうかを確認する必要があります。 広告費データを使用すると、キャンペーンから獲得したユーザーの広告コストと顧客生涯価値（CLV） [を組み合わせることで、](../../analysis/roi-ad-camp.md) キャンペーン ROIを測定できます。

[!DNL Google Adwords]資格情報を[!DNL Commerce Intelligence]に入力して開始します。

1. `Connections` データの管理/統合&#x200B;**の下の** ページに移動します。
1. 画面の右上にある「**統合を追加**」をクリックします。
1. **[!DNL Google Adwords]** アイコンをクリックします。 これにより、[!DNL Google Adwords]資格情報ページが開きます。
1. [!DNL Google Analytics]資格情報を入力してください。 認証プロセスが完了すると、次の場所にリダイレクトされます：[!DNL Commerce Intelligence]。
1. プロファイル IDのリストが表示されます。 [!DNL Commerce Intelligence]に接続するプロファイルを確認してください。

   プロファイルの選択内容を表示する![Google AdWords接続ダイアログ &#x200B;](../../../assets/cnnct-profile.png)

1. 変更は自動的に保存されるので、完了したら&#x200B;**[!UICONTROL Back to Connections]**&#x200B;をクリックします。

複数のプロファイルがあり、そのプロファイルを特定するヘルプが必要な場合は、以下の「`Connecting Multiple Google Analytics profiles`」セクションを参照してください。

## 複数の[!DNL Google Analytics] プロファイルを接続しています

1つの[!DNL Google Analytics] アカウントに複数のWeb サイトを接続している可能性があります。各Web サイトは、独自の[!DNL Google Analytics] プロファイル IDで識別されます。 この場合、すべてのプロファイル IDを[!DNL Commerce Intelligence]に含めるオプションがあります。 プロファイル選択手順に含めるプロファイル IDを確認します。

**特定のweb サイトのGoogle Analytics プロファイル IDを識別するには：**

1. [!DNL Google Analytics]にログイン
1. 特定のweb サイトの[!DNL Google Analytics] ダッシュボードに移動
1. URLを見てください – プロファイル IDは、行の末尾にある`p`に続く8つの数字に対応しています。

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## [!DNL Google Adwords]の接続を切断しています

1. [!DNL Google] [&#x200B; アカウント設定](https://www.google.com/account/about/?hl=en) ページにアクセスします。
1. `Security` セクションで、**[!UICONTROL edit]**&#x200B;個のアプリケーションとサイトの横にある`Authorizing`をクリックします。
1. **[!UICONTROL revoke access]**&#x200B;をクリックします。

## 関連

* [統合を再認証しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
* [&#x200B; [!DNL Google ECommerce]経由で注文の紹介ソースを追跡](../integrations/google-ecommerce.md)
* [データベース内のユーザー紹介ソースの追跡](../../analysis/google-track-user-acq.md)
* [最も価値のある獲得ソースとチャネルの発見](../../analysis/most-value-source-channel.md)
* [広告キャンペーンのROIを高める](../../analysis/roi-ad-camp.md)
* [&#x200B; [!DNL Google Analytics] UTM アトリビューションの仕組み](../../analysis/utm-attributes.md)
