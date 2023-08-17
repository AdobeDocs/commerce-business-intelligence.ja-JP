---
title: Google Adwords を接続
description: キャンペーンから取得したユーザーの広告コストと顧客のライフタイムバリュー (CLV) を結び付け、キャンペーンの ROI を測定する方法を説明します。
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 接続 [!DNL Google Adwords]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

あなたは研究を行い、広告を作り、あなたは [!DNL Google] キャンペーン。 次に、広告支出のデータを分析し、お金が効果的に使われているかどうかを確認する時間です。 広告費用データを使用すると、次のことができます。 [広告コストと顧客のライフタイムバリュー (CLV) を結び付けて、キャンペーンの ROI を測定します。](../../analysis/roi-ad-camp.md) キャンペーンから取得したユーザー数を格納できます。

まず、 [!DNL Google Adwords] ～への認証情報 [!DNL Commerce Intelligence].

1. 次に移動： `Connections` 下のページ **データを管理/統合**.
1. クリック **統合を追加**：画面の右上にあります。
1. 次をクリック： **[!DNL Google Adwords]** アイコン。 これにより、 [!DNL Google Adwords] 認証情報ページ。
1. を入力します。 [!DNL Google Analytics] 認証情報。 認証プロセスが完了すると、にリダイレクトされます。 [!DNL Commerce Intelligence].
1. プロファイル ID のリストが表示されます。 接続先のプロファイルを確認してください [!DNL Commerce Intelligence].

   ![](../../../assets/cnnct-profile.png)

1. 変更は自動的に保存されるので、「 **[!UICONTROL Back to Connections]** 終わったら

複数のプロファイルがあり、どちらを特定するかについて何らかの支援が必要な場合は、 `Connecting Multiple Google Analytics profiles` 」の節を参照してください。

## 複数の接続 [!DNL Google Analytics] プロファイル

1 つのに複数の Web サイトを接続している可能性があります [!DNL Google Analytics] 独自のアカウントで識別 [!DNL Google Analytics] プロファイル ID。 この場合、すべてのプロファイル ID を [!DNL Commerce Intelligence]. プロファイル選択手順で含めるプロファイル ID を確認します。

**特定の Web サイトのGoogle Analyticsプロファイル ID を識別するには：**

1. ログイン [!DNL Google Analytics]
1. 特定の Web サイトの [!DNL Google Analytics] dashboard
1. URL を見る — プロファイル ID は次の 8 つの数字に対応します `p` 行末：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## 切断中 [!DNL Google Adwords]

1. 次のサイトにアクセスします。 [!DNL Google] [アカウント設定](https://www.google.com/account/about/?hl=en) ページに貼り付けます。
1. の下 `Security` セクションで、 **[!UICONTROL edit]** 次の `Authorizing` アプリケーションとサイト。
1. クリック **[!UICONTROL revoke access]**.

## 関連

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [経由で注文のリファラルソースを追跡する [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [データベース内のユーザーのリファラルソースを追跡する](../../analysis/google-track-user-acq.md)
* [最も価値のある獲得ソースとチャネルを見つける](../../analysis/most-value-source-channel.md)
* [広告キャンペーンの ROI の向上](../../analysis/roi-ad-camp.md)
* [方法 [!DNL Google Analytics] UTM 属性は機能しますか？](../../analysis/utm-attributes.md)
