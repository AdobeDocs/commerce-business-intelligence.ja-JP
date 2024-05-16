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

# 接続 [!DNL Google Adwords]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

調査を行い、広告を作成し、を起動しました [!DNL Google] キャンペーン。 次に、広告費用データを分析し、お金が効果的に費やされているかどうかを確認します。 広告費用データを使用すると、次のことができます [広告コストと顧客生涯価値（CLV）を組み合わせて、キャンペーン ROI を測定します](../../analysis/roi-ad-camp.md) キャンペーンから取得したユーザーの。

基本を学ぶには [!DNL Google Adwords] への認証情報 [!DNL Commerce Intelligence].

1. に移動します `Connections` ページの下 **データを管理/統合**.
1. クリック **統合を追加**&#x200B;画面の右上にあります。
1. 「」をクリックします **[!DNL Google Adwords]** アイコン。 これにより、 [!DNL Google Adwords] 資格情報ページ。
1. を入力 [!DNL Google Analytics] 資格情報。 認証プロセスが完了すると、にリダイレクトされます。 [!DNL Commerce Intelligence].
1. プロファイル ID のリストが表示されます。 接続先のプロファイルを確認する [!DNL Commerce Intelligence].

   ![](../../../assets/cnnct-profile.png)

1. 変更は自動的に保存されるため、 **[!UICONTROL Back to Connections]** 完了したら、

複数のプロファイルがあり、どちらを識別するのかについて不明な点がある場合は、を参照してください。 `Connecting Multiple Google Analytics profiles` セクションを下にします。

## 複数のの接続 [!DNL Google Analytics] プロファイル

複数の web サイトが 1 つのサイトに接続されている場合があります [!DNL Google Analytics] アカウント（独自に識別） [!DNL Google Analytics] プロファイル ID。 この場合、すべてのプロファイル ID をに含めるオプションがあります [!DNL Commerce Intelligence]. プロファイル選択手順に含めるプロファイル ID を確認します。

**特定の web サイトのGoogle Analyticsプロファイル ID を識別するには：**

1. にログインします [!DNL Google Analytics]
1. 特定の Web サイトに移動 [!DNL Google Analytics] dashboard
1. URL を見ます。プロファイル ID は、次の 8 つの数値に対応しています `p` ラインの最後に：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## 切断中 [!DNL Google Adwords]

1. にアクセス [!DNL Google] [アカウント設定](https://www.google.com/account/about/?hl=en) ページ。
1. の下 `Security` セクションで、をクリック **[!UICONTROL edit]** 次の `Authorizing` アプリケーションとサイト。
1. クリック **[!UICONTROL revoke access]**.

## 関連

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [以下を介した注文参照ソースの追跡 [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [データベース内のユーザー紹介ソースを追跡](../../analysis/google-track-user-acq.md)
* [最も価値のある獲得ソースとチャネルを見つける](../../analysis/most-value-source-channel.md)
* [広告キャンペーンの ROI の向上](../../analysis/roi-ad-camp.md)
* [方法 [!DNL Google Analytics] UTM アトリビューションの仕組み](../../analysis/utm-attributes.md)
