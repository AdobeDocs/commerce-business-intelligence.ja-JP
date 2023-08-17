---
title: Google E コマースを接続
description: 最も重要な参照チャネルについて学びます。
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 接続 [!DNL Google ECommerce]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

トラフィックと注文の流れは、顧客に効果的に連絡し、獲得していることを意味します。 しかし、あなたの最も価値のある紹介チャネルは何ですか？ あるソースから獲得した顧客と別のソースから獲得した顧客の平均ライフタイム値はどれくらいですか？ 次の注文のリファラルソースデータを接続する。 [!DNL Google ECommerce] から [!DNL Commerce Intelligence]を使用すると、 [最も価値の高いマーケティングチャネル](../../../data-analyst/analysis/most-value-source-channel.md).

まず、 [!DNL Google ECommerce] ～への認証情報 [!DNL Commerce Intelligence]:

1. 次に移動： `Connections` 下のページ **[!UICONTROL Admin** > **Connections]**.

1. クリック **[!UICONTROL Add a New Source]**( 画面の右側、上の `Data Sources` 表。

1. 次をクリック： [!DNL Google ECommerce] アイコン。 これにより、 [!DNL Google ECommerce] 認証情報ページ。

1. を入力します。 [!DNL Google Analytics] 認証情報。 認証プロセスの完了時に、次の場所にリダイレクトされます： [!DNL Commerce Intelligence].

1. プロファイル ID のリストが表示されます。 接続先のプロファイルを確認してください [!DNL Commerce Intelligence].

   複数のプロファイルがあり、どちらを識別するかについてのヘルプが必要な場合は、**複数の接続 [!DNL Google Analytics] 以下のプロファイルの節を参照してください。

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. 変更は自動的に保存されるので、「 **[!UICONTROL Back to Connections]** 完了したら、

## 複数の接続 [!DNL Google Analytics] 次のプロファイル： [!DNL Commerce Intelligence]

1 つのに複数の Web サイトを接続している可能性があります [!DNL Google Analytics] 独自のアカウントで識別 [!DNL Google Analytics] プロファイル ID。 この場合、すべてのプロファイル ID を [!DNL Commerce Intelligence]. プロファイル選択手順で含めるプロファイル ID を確認します。

特定の Web サイトの [!DNL Google Analytics] プロファイル ID :

1. ログイン [!DNL Google Analytics].
1. 特定の Web サイトの [!DNL Google Analytics] ダッシュボード。
1. URL を見る — プロファイル ID は次の 8 つの数字に対応します `p` 行の終わりに

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 切断中 [!DNL Google ECommerce] から [!DNL Commerce Intelligence] {#disconnect}

1. 次のサイトにアクセスします。 [!DNL Google Analytics] [アカウント設定](https://www.google.com/account/about/?hl=en) ページに貼り付けます。
1. の下 `Security` セクションで、 **[!UICONTROL edit]** 次の `Authorizing` アプリケーションとサイト。
1. クリック **[!UICONTROL revoke access]** 次の [!DNL Commerce Intelligence].

## 関連：

* [期待値 [!DNL Google ECommerce] データ](../integrations/google-ecommerce-data.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [設定 [!DNL Google ECommerce] tracking](https://support.google.com/analytics/answer/1009612?hl=en)
* [最も価値のある獲得ソースとチャネルを見つける](../../analysis/most-value-source-channel.md)
* [広告キャンペーンの ROI の向上](../../analysis/roi-ad-camp.md)
