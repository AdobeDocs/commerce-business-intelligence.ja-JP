---
title: Google Analyticsをウェアハウジングに接続
description: 訪問者によるサイトの使用方法、魅力的なコンテンツ、訪問者が離脱する場所などをトラッキングする方法を説明します。
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Connect [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>[ 管理者権限 ](../../../administrator/user-management/user-management.md) が必要です。

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] は、インターネット上で最も広く使用されている web 分析サービスです。 Web サイトに [!DNL Google Analytics] を実装すると、訪問者によるサイトの使用方法、魅力的なコンテンツ、訪問者が離脱する場所などを追跡できます。 [!DNL Google Analytics Warehoused] は、既存の [!DNL Google Analytics] 統合とは別の統合です。 これにより、既存の [!DNL Google Analytics] 統合のライブフィードとは異なり、Data Warehouseに [!DNL Google Analytics] のデータが含まれるので、分析の精度が向上します。 これらの指標を [!DNL Commerce Intelligence] で分析すると、他のデータと共に、サイトの全体的な正常性と操作性が向上します。

## GA ウェアハウスとライブ統合の違い

主な違いは、1 つの統合が保存され（[!DNL Google Analytics Warehoused]）、もう 1 つは保存されない（[!DNL Google Analytics Live]）ことです。 [!DNL Google Analytics Warehoused] の場合は、[!DNL Google Analytics] データを操作でき、[!DNL Google Analytics] と他のデータソースを組み合わせて、インサイトに満ちたレポートを作成できます。

操作の観点から実行できる操作の例については、[!DNL Google Analytics] の広告キャンペーンを参照してください。 第 4 四半期に、異なる名前の複数の広告キャンペーンがあったとします。 キャンペーンは、特定のマーケティング施策の成果でした。 ウェアハウスに格納されたデータを使用すると、問題のキャンペーン名を見つけて、第 4 四半期のイニシアチブ名 `Operation Dumbo` を返す列を作成できます。

組み合わせ側面 [!DNL Google Analytics] 使用すると、分析を行うためにデータを他のデータに結合できます。 例えば、`Total Time On Site By Ad Campaign` のデータ [!DNL Google Analytics] 取り、`Total Spent Per Campaign` の [!DNL Facebook Ads] データと結合して、エンゲージメントにかかる費用の全体像を把握できます。

一方、[!DNL Google Analytics Live] の統合では、すべての [!DNL Google Analytics] グラフはData Warehouseに保存されない小さなサイロのようになります。

## [!DNL Google Analytics Warehoused] の接続

>[!INFO]
>
>[!DNL Google Analytics Warehoused] は `Premium` 統合です。 この統合をサブスクリプションに追加することに関心がある場合は、[ サポートにお問い合わせください ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)。

1. `Connections` の下の **[!UICONTROL Admin** > **Integrations]** ページに移動します。
1. 右側にある「**[!UICONTROL Add an Integration]**」をクリックします。
1. [!DNL Google Analytics Warehoused] アイコンをクリックします。 これにより、[!DNL Google Analytics] 資格情報ページが開きます。
1. [!DNL Google Analytics] 資格情報を入力します。 認証プロセスが完了すると、[!DNL Commerce Intelligence] にリダイレクトされます。
1. プロファイル ID のリストが表示されます。 [!DNL Commerce Intelligence] に接続するプロファイルを確認します。 複数のプロファイルがあり、どれを識別するのかについてのヘルプが必要な場合は、以下の複数の [!DNL Google Analytics] プロファイルの接続の節を参照してください。

## 複数の [!DNL Google Analytics] プロファイルの接続

1 つの [!DNL Google Analytics] アカウントに接続された複数の web サイトがあり、独自の [!DNL Google Analytics] プロファイル ID で識別されている場合があります。 この場合、すべてのプロファイル ID を [!DNL Commerce Intelligence] に含めるオプションがあります。 プロファイル選択手順に含めるプロファイル ID を確認します。

特定の web サイトの [!DNL Google Analytics] プロファイル ID を識別するには：

1. [!DNL Google Analytics] にログインします
1. 特定の web サイトの [!DNL Google Analytics] ダッシュボードに移動します
1. URL を見ます。プロファイル ID は、行の最後の `p` に続く 8 つの数値に対応しています

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## [!DNL Google Analytics Warehoused] を [!DNL Commerce Intelligence] から切断しています {#disconnect}

1. [!DNL Google Analytics] の [ アカウント設定 ](https://myaccount.google.com/intro) ページにアクセスします。
1. 「`Security`」セクションで、「アプリケーションとサイト」の横にある「**[!UICONTROL edit]**」 `Authorizing` クリックします。
1. 「**[!UICONTROL revoke access]**」の横にある「[!DNL Commerce Intelligence]」をクリックします。

## 関連ドキュメント

* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
* [接続  [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Web サイトのアクティビティと顧客コンバージョン率の分析](../../analysis/web-act-cust-conversion.md)
* [cookie を使用したユーザー取得デ  [!DNL Google Analytics]  タの追跡](../../analysis/google-track-user-acq.md)
