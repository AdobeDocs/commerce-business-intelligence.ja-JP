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

# Connect [!DNL Google ECommerce]

>[!NOTE]
>
>[ 管理者権限 ](../../../administrator/user-management/user-management.md) が必要です。

![](../../../assets/google-ecommerce-logo.png)

トラフィックと注文の着実な流れがあります。つまり、顧客に効果的に到達し、獲得しています。 しかし、最も価値のある紹介チャネルは何ですか？ あるソースから取得した顧客の平均生涯価値は、別のソースから取得した顧客の平均生涯価値はどれくらいですか？ 注文参照ソースデータを [!DNL Google ECommerce] から [!DNL Commerce Intelligence] に接続することで、[ 最も価値のあるマーケティングチャネル ](../../../data-analyst/analysis/most-value-source-channel.md) を特定するのに役立つ分析を構築できます。

まず、[!DNL Google ECommerce] の資格情報を [!DNL Commerce Intelligence] に入力します。

1. **[!UICONTROL Admin** > **Connections]** の下の `Connections` ページに移動します。

1. `Data Sources` テーブルの上の画面の右側にある [**[!UICONTROL Add a New Source]**] をクリックします。

1. [!DNL Google ECommerce] アイコンをクリックします。 これにより、[!DNL Google ECommerce] 資格情報ページが開きます。

1. [!DNL Google Analytics] 資格情報を入力します。 認証プロセスが完了すると、[!DNL Commerce Intelligence] にリダイレクトされます。

1. プロファイル ID のリストが表示されます。 [!DNL Commerce Intelligence] に接続するプロファイルを確認します。

   複数のプロファイルがあり、どれを識別するのかについてのヘルプが必要な場合は、以下の**複数の [!DNL Google Analytics] プロファイルの接続」の節を参照してください。

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. 変更は自動的に保存されるので、完了したら「**[!UICONTROL Back to Connections]**」をクリックします。

## [!DNL Commerce Intelligence] への複数の [!DNL Google Analytics] プロファイルの接続

1 つの [!DNL Google Analytics] アカウントに接続された複数の web サイトがあり、独自の [!DNL Google Analytics] プロファイル ID で識別されている場合があります。 この場合、すべてのプロファイル ID を [!DNL Commerce Intelligence] に含めるオプションがあります。 プロファイル選択手順に含めるプロファイル ID を確認します。

特定の web サイトの [!DNL Google Analytics] プロファイル ID を識別するには：

1. [!DNL Google Analytics] にログインします。
1. 特定の web サイトの [!DNL Google Analytics] ダッシュボードに移動します。
1. URL を見ます。プロファイル ID は、行の最後の `p` に続く 8 つの数値に対応しています。

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## [!DNL Google ECommerce] を [!DNL Commerce Intelligence] から切断しています {#disconnect}

1. [!DNL Google Analytics] の [ アカウント設定 ](https://www.google.com/account/about/?hl=en) ページにアクセスします。
1. [`Security`] セクションで、[ アプリケーションとサイト `Authorizing` 横にある [**[!UICONTROL edit]**] をクリックします。
1. 「[!DNL Commerce Intelligence]」の横にある「**[!UICONTROL revoke access]**」をクリックします。

## 関連：

* [Expected [!DNL Google ECommerce] data](../integrations/google-ecommerce-data.md)
* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [ 設定  [!DNL Google ECommerce]  トラッキング ](https://support.google.com/analytics/answer/1009612?hl=en)
* [最も価値のある獲得ソースとチャネルを見つける](../../analysis/most-value-source-channel.md)
* [広告キャンペーンの ROI の向上](../../analysis/roi-ad-camp.md)
