---
title: 獲得ソースを使用したGoogle Analytics チャネルのレプリケーション
description: 獲得ソースを使用してGoogle Analytics チャネルをレプリケートする方法を説明します。
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 736dbdc3ea6bc8b7c852f06110705765f040c31f
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# 獲得ソースを使用した [!DNL Google Analytics]

## チャネルとは {#channels}

カスタムセグメントを作成して、様々なトラフィックのパフォーマンスを確認しトレンドを監視することは、[!DNL Google Analytics] の最も強力な使用方法の 1 つです。 [!DNL Google Analytics] にデフォルトで存在するセグメントの 1 つのクラスは `Channels` です。 チャネルは、ユーザーがサイトを訪れる一般的な方法をグループ化したものです。  [!DNL Google Analytics] では、ユーザーを取得する様々な方法（ソーシャルメディア、クリック課金、メール、リファラルリンクなど）を自動的に並べ替えて、バケットまたはチャネルにバンドルします。

## Commerce Intelligenceに `channels` が表示されないのはなぜですか。 {#nochannels}

`Channels` は、単純なデータの集合バケットです。 [!DNL Google] では、獲得をチャネルバケットに並べ替えるために、獲得 [Source](https://support.google.com/analytics/answer/1033173?hl=en) （トラフィックの接触チャネル）と獲得 [Medium](https://support.google.com/analytics/answer/6099206?hl=en) （ソースの一般カテゴリ）の組み合わせという、特定のパラメーターを使用した個別のルールと定義を設定します。

これらのバケットがあると、トラフィックの発信元を理解するのに役立ちますが、このデータはチャネルではなく、SourceとMediumの組み合わせによってタグ付けされます。 [!DNL Google] はチャネル情報を 2 つの異なるデータポイントとして送信するので、チャネルグループ化は [!DNL Commerce Intelligence] に自動的には表示されません。

## デフォルトのチャネルグループは何ですか？ どのように作成されるか。

デフォルトでは、[!DNL Google] は 8 つの異なるチャネルを設定します。 チャネルの作成方法を決定するルールを以下に示します。

| **チャネル** | **何ですか？** | **どのように作成されますか？** |
|---|---|---|
| ダイレクト | サイトに直接入ったユーザー。 | Source = `Direct`<br> およびMedium = `(not set); OR Medium = (none)` |
| オーガニック検索 | 無給検索エンジンで有機的にランク付けされたトラフィック。 | Medium= `organic` |
| リファラル | オーガニック検索以外の外部リンクや、ソーシャルネットワーク以外の web サイトから受信したトラフィック。 | Medium= `referral` |
| ペイド検索 | メディアが「cpc」、「ppc」、または「paidsearch」のいずれかであり、「コンテンツ」に一致しない広告配信ネットワークである UTM トラッキングコードを持つトラフィック。 | Medium = `^(cpc|ppc|paidsearch)$`<br> および Ad Distribution Network ≠ `Content` |
| ソーシャル | 約 400 のソーシャルネットワークのいずれかから発生し、広告としてタグ付けされていないリファラルトラフィック。 | ソーシャルSource参照元= `Yes`<br> またはMedium = `^(social|social-network|social-media|sm|social network|social media)$` |
| 電子メール | 「メール」というメディアでタグ付けされたセッションからのトラフィック。 | Mediumの UTM トラッキングコード = `email` |
| 表示 | メディアがディスプレイまたは cpm である UTM トラッキングコードを持つトラフィック。 また、広告配信ネットワークが「コンテンツ」と一致する AdWords インタラクションも含まれます | Medium = `^(display|cpm|banner)$`<br> または Ad Distribution Network = `Content`<br> および Ad Format ≠ `Text` |
| その他 | 「cpc」、「ppc」、「cpm」、「cpv」、「cpa」、「cpp」、「アフィリエイト」という媒体でタグ付けされた他の広告チャネル（有料検索を除く）からのセッション。 | Medium= `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## これらのチャネルグループをData Warehouseで再作成するにはどうすればよいですか？ {#recreate}

チャネルはソースとメディアの単なる組み合わせだとわかったので、これらのグループ化をData Warehouseで再作成するには、簡単な 3 つの手順のプロセスです。

1. **統合を有効 [!DNL Google ECommerce] する**

   [ 有効 ](../importing-data/integrations/google-ecommerce.md) にした場合、Data Warehouseで [sync](tour-dwm.md#syncing) **medium** および **source** フィールドが設定されていることを確認します。 これが完了すると、中程度のデータやソースの獲得データがData Warehouseに取り込まれます。

1. **Googleのチャネルグループ化のマッピングをアップロードする**

   Adobe Commerceが、[ ダウンロード ](../../assets/ga-channel-mapping.csv) 可能なファイルとしてマッピングされた、デフォルトのグループを含むテーブルを作成します。

   [!DNL Google Analytics] pro で独自のチャネルを作成した場合は、ファイルを [!DNL Commerce Intelligence] にアップロードする前に、特定のルールをマッピングテーブルに追加する必要があります。

   ファイルをData Warehouse as a[ ファイルのアップロード ](../importing-data/connecting-data/using-file-uploader.md) に取り込みます。

   ![ プライマリキーの設定を示すData Warehouse Manager インターフェイス ](../../assets/Setting_Primary_Keys.png)

1. **とマッピングファイルのアップロード間 [!DNL Google ECommerce] 関係の確立**

   [!DNL Google ECommerce] とマッピングテーブルの間の関係を確立するには、データアナリストチームに [ サポート依頼を送信 ](../../guide-overview.md#Submitting-a-Support-Ticket) して、このトピックを参照してください。 アナリストが、E コマーステーブルに **チャネル** という新しい計算列を作成します。 **完全な更新サイクルの後**、この列は、`Filter` または `Group by` で使用できるようになります。

これで、Data Warehouseに [!DNL Google Analytics Channel] のグループ化が作成されました。これにより、新しい視点からデータを分析できます。

![ 注文数指標のチャネル別のセグメント化 ](../../assets/GA_Channel_Gif.gif)

この例では、**注文数** 指標を **チャネル** でセグメント化して単純な作業を開始しました。 新しい列をテストし、[!DNL Google Analytics Channel] データで特定できるトレンドを確認します。

## 関連ドキュメント

* [Report Builderの使用](../../tutorials/using-visual-report-builder.md)
* [Expected[!DNL Google ECommerce]data](../importing-data/integrations/google-ecommerce-data.md)
* [注文お [!DNL Google ECommerce] び顧客データを使用したディメンションの作成](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [最も価値の高い獲得ソースとチャネルは何ですか？](../analysis/most-value-source-channel.md)
