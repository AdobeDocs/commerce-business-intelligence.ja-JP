---
title: 獲得ソースを使用したGoogle Analyticsチャネルのレプリケーション
description: 獲得ソースを使用してGoogle Analyticsチャネルをレプリケートする方法を説明します。
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# [!DNL Google Analytics] 獲得ソースの使用

## チャネルとは {#channels}

カスタムセグメントを作成して、様々なトラフィックのパフォーマンスを確認しトレンドを監視することは、の最も強力な使用方法の 1 つです [!DNL Google Analytics]. デフォルトでに存在する 1 つのクラスのセグメント [!DNL Google Analytics] は `Channels`. チャネルは、ユーザーがサイトを訪れる一般的な方法をグループ化したものです。  [!DNL Google Analytics] ソーシャルメディア、クリック課金、メール、リファラルリンクなど、ユーザーを取得する様々な方法を自動的に並べ替え、それらをバケットまたはチャネルにバンドルします。

## なぜ私は私を見ない `channels` Commerce Intelligence で？ {#nochannels}

`Channels` は単純なデータの集合バケットです。 獲得したデータをチャネルグループに並べ替えるには： [!DNL Google] 特定のパラメーターを使用して個別のルールおよび定義を設定します：獲得の組み合わせ [ソース](https://support.google.com/analytics/answer/1033173?hl=en) （トラフィックの起源）と獲得 [中](https://support.google.com/analytics/answer/6099206?hl=en) （ソースの一般的なカテゴリ）。

これらのバケットがあると、トラフィックの発信元を把握するのに役立ちますが、このデータはチャネルではなく、ソースとメディアの組み合わせによってタグ付けされます。 なぜなら [!DNL Google] は、チャネル情報を 2 つの異なるデータポイントとして送信します。チャネルグループ化は、では自動的には表示されません [!DNL Commerce Intelligence].

## デフォルトのチャネルグループは何ですか？ どのように作成されるか。

デフォルトでは [!DNL Google] は 8 つの異なるチャネルを設定します。 チャネルの作成方法を決定するルールを以下に示します。

| **チャネル** | **それは何ですか。** | **どのように作成されますか？** |
|---|---|---|
| ダイレクト | サイトに直接入ったユーザー。 | ソース = `Direct`<br>とメディア = `(not set); OR Medium = (none)` |
| オーガニック検索 | 無給検索エンジンで有機的にランク付けされたトラフィック。 | 中= `organic` |
| リファラル | オーガニック検索以外の外部リンクや、ソーシャルネットワーク以外の web サイトから受信したトラフィック。 | 中= `referral` |
| ペイド検索 | メディアが「cpc」、「ppc」、または「paidsearch」のいずれかであり、「コンテンツ」に一致しない広告配信ネットワークである UTM トラッキングコードを持つトラフィック。 | 中= `^(cpc|ppc|paidsearch)$`<br>および広告配信ネットワーク ≠ `Content` |
| ソーシャル | およそ 1 つから送信されるリファラルトラフィック [400 のソーシャルネットワーク](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) およびは広告としてタグ付けされていません。 | ソーシャルソースのリファラル = `Yes`<br>または中= `^(social|social-network|social-media|sm|social network|social media)$` |
| 電子メール | 「メール」というメディアでタグ付けされたセッションからのトラフィック。 | メディアの UTM トラッキングコード = `email` |
| 表示 | メディアがディスプレイまたは cpm である UTM トラッキングコードを持つトラフィック。 また、広告配信ネットワークが「コンテンツ」と一致する AdWords インタラクションも含まれます | 中= `^(display|cpm|banner)$`<br>OR 広告配信ネットワーク = `Content`<br>および広告フォーマット≠ `Text` |
| その他 | 「cpc」、「ppc」、「cpm」、「cpv」、「cpa」、「cpp」、「アフィリエイト」という媒体でタグ付けされた他の広告チャネル（有料検索を除く）からのセッション。 | 中= `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## Data Warehouseでこれらのチャネルグループ化を再作成するにはどうすればよいですか？ {#recreate}

チャネルはソースとメディアの単なる組み合わせであることが理解できたので、Data Warehouseでこれらのグループ化を再作成するのは簡単な 3 ステップのプロセスです。

1. **を有効にする[!DNL Google ECommerce]統合**

   [有効な場合](../importing-data/integrations/google-ecommerce.md)必ずしてください [同期]（../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing） **中** および **ソース** Data Warehouseのフィールド。 これが完了すると、メディアおよびソースの獲得データがData Warehouseに取り込まれます。

1. **Googleのチャネルグループ化のマッピングのアップロード**

   Adobe Commerceは、デフォルトのグループを含むテーブルを、作成可能なファイルとしてマッピングします [download](../../assets/ga-channel-mapping.csv).

   次の場合： [!DNL Google Analytics] 独自のチャネルを作成し、固有のルールをマッピングテーブルに追加してから、ファイルをにアップロードします。 [!DNL Commerce Intelligence].

   をData Warehouseに取り込みます [ファイルのアップロード](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **A と B の間に関係を築く[!DNL Google ECommerce]およびマッピングファイルのアップロード**

   A と B の間の関係を確立するには[!DNL Google ECommerce] とマッピングテーブル [サポートリクエストを送信](../../guide-overview.md#Submitting-a-Support-Ticket) をデータアナリストチームに送信し、このトピックを参照します。 アナリストは、という新しい計算列を作成します **チャネル** E コマーステーブルで確認できます。 **完全更新サイクルの後**、この列はで使用できるようになります `Filter` または `Group by`.

次が揃いました [!DNL Google Analytics Channel] Data Warehouseのグループ化。つまり、新しい観点からデータを分析できます。

![注文数指標をチャネル別にセグメント化](../../assets/GA_Channel_Gif.gif)

この例では、をセグメント化してシンプルな構成から始めました **注文数** 指標の基準 **チャネル**. 新しい列をテストして、で特定できるトレンドを確認する [!DNL Google Analytics Channel] データ！

## 関連ドキュメント

* [Report Builderの使用](../../tutorials/using-visual-report-builder.md)
* [予測[!DNL Google ECommerce]データ](../importing-data/integrations/google-ecommerce-data.md)
* [ビルド[!DNL Google ECommerce]注文および顧客データを含むディメンション](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [最も価値の高い獲得ソースとチャネルは何ですか？](../analysis/most-value-source-channel.md)
