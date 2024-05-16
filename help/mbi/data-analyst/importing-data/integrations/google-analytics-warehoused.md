---
title: Google Analyticsが倉庫に保管されているを接続
description: 訪問者によるサイトの使用方法、魅力的なコンテンツ、訪問者が離脱する場所などをトラッキングする方法を説明します。
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# 接続 [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] は、インターネット上で最も広く使用されている web 分析サービスです。 実装 [!DNL Google Analytics] web サイトでは、訪問者によるサイトの使用方法、魅力的なコンテンツ、訪問者が離脱する場所などを追跡できます。 [!DNL Google Analytics Warehoused] は、既存のとは別の統合です [!DNL Google Analytics] 統合。 以下の条件を満たすことで、より良い分析が可能になります [!DNL Google Analytics] Data Warehouse内のデータ（既存ののライブフィードとは異なる） [!DNL Google Analytics] 統合。 でのこれらの指標の分析 [!DNL Commerce Intelligence]は、他のデータと共に、サイトの全体的な正常性と操作性を向上させます。

## GA ウェアハウスとライブ統合の違い

主な差別化要因は、1 つの統合が格納されるということです（[!DNL Google Analytics Warehoused]）、もう 1 つは（[!DNL Google Analytics Live]）に設定します。 の場合 [!DNL Google Analytics Warehoused]を使用すると、の操作が可能です [!DNL Google Analytics] を使用すると、との結合が可能です。 [!DNL Google Analytics] インサイトに満ちたレポートを作成するためのその他のデータソース。

を見る [!DNL Google Analytics] 操作の観点からできることの例として、広告キャンペーンを使用します。 第 4 四半期に、異なる名前の複数の広告キャンペーンがあったとします。 キャンペーンは、特定のマーケティング施策の成果でした。 保管されたデータを使用すると、問題のキャンペーン名を見つけて、第 4 四半期のイニシアチブ名を返す列を作成できます。 `Operation Dumbo`.

組み合わせ側面では、 [!DNL Google Analytics] 分析を行うために他のデータに結合されるデータ。 例： `Total Time On Site By Ad Campaign` からのデータ [!DNL Google Analytics] そして、それに加わる `Total Spent Per Campaign` からのデータ [!DNL Facebook Ads] エンゲージメントにかかる費用の全体像を把握する

（を使用） [!DNL Google Analytics Live] 一方、の統合では、 [!DNL Google Analytics] グラフは、Data Warehouseに保存されていない小さなサイロのようなものです。

## 接続中 [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] が `Premium` 統合。 [サポートに連絡する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) この統合をサブスクリプションに追加することに関心がある場合。

1. に移動します `Connections` ページの下 **[!UICONTROL Admin** > **Integrations]**.
1. クリック **[!UICONTROL Add an Integration]**&#x200B;右側にあります。
1. 「」をクリックします [!DNL Google Analytics Warehoused] アイコン。 これにより、 [!DNL Google Analytics] 資格情報ページ。
1. を入力 [!DNL Google Analytics] 資格情報。 認証プロセスが完了すると、にリダイレクトされます。 [!DNL Commerce Intelligence].
1. プロファイル ID のリストが表示されます。 接続先のプロファイルを確認する [!DNL Commerce Intelligence]. 複数のプロファイルがあり、どちらを識別するかのヘルプが必要な場合は、複数のプロファイルの接続を参照してください [!DNL Google Analytics] 以下の「プロファイル」セクション：

## 複数のの接続 [!DNL Google Analytics] プロファイル

複数の web サイトが 1 つのサイトに接続されている場合があります [!DNL Google Analytics] アカウント（独自に識別） [!DNL Google Analytics] プロファイル ID。 この場合、すべてのプロファイル ID をに含めるオプションがあります [!DNL Commerce Intelligence]. プロファイル選択手順に含めるプロファイル ID を確認します。

特定の web サイトを識別するには [!DNL Google Analytics] プロファイル ID:

1. にログインします [!DNL Google Analytics]
1. 特定の Web サイトに移動 [!DNL Google Analytics] dashboard
1. URL を見ます。プロファイル ID は、次の 8 つの数値に対応しています `p` 列の最後に

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 切断中 [!DNL Google Analytics Warehoused] から [!DNL Commerce Intelligence] {#disconnect}

1. にアクセス [!DNL Google Analytics] [アカウント設定](https://myaccount.google.com/intro) ページ。
1. の下 `Security` セクションで、をクリックします。 **[!UICONTROL edit]** 次の `Authorizing` アプリケーションとサイト。
1. クリック **[!UICONTROL revoke access]** 次の [!DNL Commerce Intelligence].

## 関連ドキュメント

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [接続中 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Web サイトのアクティビティと顧客コンバージョン率の分析](../../analysis/web-act-cust-conversion.md)
* [を使用したユーザー獲得データの追跡 [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
