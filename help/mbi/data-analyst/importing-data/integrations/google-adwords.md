---
title: Google Adwords の接続
description: 広告コストと、キャンペーンから取得したユーザーの顧客生涯価値（CLV）を組み合わせて、キャンペーン ROI を測定する方法を説明します。
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Connect [!DNL Google Adwords]

>[!NOTE]
>
>[ 管理者権限 ](../../../administrator/user-management/user-management.md) が必要です。

![](../../../assets/Google_Adwords_logo.png)

調査を行い、広告を作成し、[!DNL Google] キャンペーンを開始しました。 次に、広告費用データを分析し、お金が効果的に費やされているかどうかを確認します。 広告費用データを使用すると、広告コストとキャンペーンから取得したユーザーの顧客生涯価値（CLV）を組み合わせて [ キャンペーン ROI を測定 ](../../analysis/roi-ad-camp.md) できます。

まず、[!DNL Google Adwords] 資格情報を [!DNL Commerce Intelligence] に入力します。

1. **データを管理/統合** の下の `Connections` ページに移動します。
1. 画面の右上にある「**統合を追加**」をクリックします。
1. **[!DNL Google Adwords]** アイコンをクリックします。 これにより、[!DNL Google Adwords] 資格情報ページが開きます。
1. [!DNL Google Analytics] 資格情報を入力します。 認証プロセスが完了すると、[!DNL Commerce Intelligence] にリダイレクトされます。
1. プロファイル ID のリストが表示されます。 [!DNL Commerce Intelligence] に接続するプロファイルを確認します。

   ![](../../../assets/cnnct-profile.png)

1. 変更は自動的に保存されるので、完了したら「**[!UICONTROL Back to Connections]**」をクリックします。

複数のプロファイルがあり、どれを識別するのかについてのヘルプが必要な場合は、以下の `Connecting Multiple Google Analytics profiles` の節を参照してください。

## 複数の [!DNL Google Analytics] プロファイルの接続

1 つの [!DNL Google Analytics] アカウントに接続された複数の web サイトがあり、独自の [!DNL Google Analytics] プロファイル ID で識別されている場合があります。 この場合、すべてのプロファイル ID を [!DNL Commerce Intelligence] に含めるオプションがあります。 プロファイル選択手順に含めるプロファイル ID を確認します。

**特定の web サイトのGoogle Analyticsプロファイル ID を識別するには：**

1. [!DNL Google Analytics] にログインします
1. 特定の web サイトの [!DNL Google Analytics] ダッシュボードに移動します
1. URL を見ます。プロファイル ID は、行の最後の `p` に続く 8 つの数値に対応しています。

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## [!DNL Google Adwords] の切断

1. [!DNL Google] の [ アカウント設定 ](https://www.google.com/account/about/?hl=en) ページにアクセスします。
1. [`Security`] セクションで、&lbrack; アプリケーションとサイト `Authorizing` 横にある [**[!UICONTROL edit]**] をクリックします。
1. 「**[!UICONTROL revoke access]**」をクリックします。

## 関連

* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
* [ [!DNL Google ECommerce] を介した注文リファラルソースの追跡](../integrations/google-ecommerce.md)
* [データベース内のユーザー紹介ソースを追跡](../../analysis/google-track-user-acq.md)
* [最も価値のある獲得ソースとチャネルを見つける](../../analysis/most-value-source-channel.md)
* [広告キャンペーンの ROI の向上](../../analysis/roi-ad-camp.md)
* [ [!DNL Google Analytics] UTM アトリビューションの仕組み](../../analysis/utm-attributes.md)
