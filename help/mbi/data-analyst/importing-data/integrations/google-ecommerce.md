---
title: Google E コマースに接続
description: 最も価値の高いリファラルチャネルについて説明します。
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# 接続 [!DNL Google ECommerce]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

トラフィックと注文の着実な流れがあります。つまり、顧客に効果的に到達し、獲得しています。 しかし、最も価値のある紹介チャネルは何ですか？ あるソースから取得した顧客の平均生涯価値は、別のソースから取得した顧客の平均生涯価値はどれくらいですか？ ご注文のリファラルソースデータを次の場所から接続する [!DNL Google ECommerce] 対象： [!DNL Commerce Intelligence]を使用すると、の識別に役立つ分析を構築できます [最も価値のあるマーケティングチャネル](../../../data-analyst/analysis/most-value-source-channel.md).

基本を学ぶには [!DNL Google ECommerce] への認証情報 [!DNL Commerce Intelligence]:

1. に移動します `Connections` ページの下 **[!UICONTROL Admin** > **Connections]**.

1. クリック **[!UICONTROL Add a New Source]**&#x200B;画面右側の上部にある `Data Sources` テーブル。

1. 「」をクリックします [!DNL Google ECommerce] アイコン。 これにより、 [!DNL Google ECommerce] 資格情報ページ。

1. を入力 [!DNL Google Analytics] 資格情報。 認証プロセスが完了すると、にリダイレクトされます。 [!DNL Commerce Intelligence].

1. プロファイル ID のリストが表示されます。 接続先のプロファイルを確認する [!DNL Commerce Intelligence].

   複数のプロファイルがあり、どちらを識別するのかについて不明な点がある場合は、**複数のプロファイルの接続」を参照してください [!DNL Google Analytics] 以下の「プロファイル」セクション：

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. 変更は自動的に保存されるため、 **[!UICONTROL Back to Connections]** 完了したら、

## 複数のの接続 [!DNL Google Analytics] プロファイル先 [!DNL Commerce Intelligence]

複数の web サイトが 1 つのサイトに接続されている場合があります [!DNL Google Analytics] アカウント（独自に識別） [!DNL Google Analytics] プロファイル ID。 この場合、すべてのプロファイル ID をに含めるオプションがあります [!DNL Commerce Intelligence]. プロファイル選択手順に含めるプロファイル ID を確認します。

特定の web サイトを識別するには [!DNL Google Analytics] プロファイル ID:

1. にログインします [!DNL Google Analytics].
1. 特定の Web サイトに移動 [!DNL Google Analytics] ダッシュボード。
1. URL を見ます。プロファイル ID は、次の 8 つの数値に対応しています `p` ラインの最後に。

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 切断中 [!DNL Google ECommerce] から [!DNL Commerce Intelligence] {#disconnect}

1. にアクセス [!DNL Google Analytics] [アカウント設定](https://www.google.com/account/about/?hl=en) ページ。
1. の下 `Security` セクションで、をクリック **[!UICONTROL edit]** 次の `Authorizing` アプリケーションとサイト。
1. クリック **[!UICONTROL revoke access]** 次の [!DNL Commerce Intelligence].

## 関連：

* [予測 [!DNL Google ECommerce] データ](../integrations/google-ecommerce-data.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [設定 [!DNL Google ECommerce] トラッキング](https://support.google.com/analytics/answer/1009612?hl=en)
* [最も価値のある獲得ソースとチャネルを見つける](../../analysis/most-value-source-channel.md)
* [広告キャンペーンの ROI の向上](../../analysis/roi-ad-camp.md)
