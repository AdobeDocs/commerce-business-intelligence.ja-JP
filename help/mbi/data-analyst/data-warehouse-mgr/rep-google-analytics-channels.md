---
title: 獲得ソースを使用したGoogle Analyticsチャネルのレプリケーション
description: 獲得ソースを使用してGoogle Analyticsチャネルをレプリケートする方法について説明します。
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# 獲得ソースを使用したGoogle Analytics

## チャネルとは {#channels}

様々なトラフィックのパフォーマンスを確認し、トレンドを観察するためのカスタムセグメントを作成することは、  [!DNL Google Analytics ]. デフォルトでに存在するセグメントの 1 つのクラス [!DNL Google Analytics ] が `Channels`. チャネルは、訪問者がサイトに来訪する一般的な方法のグループです。  [!DNL Google Analytics ] ユーザーを取得した様々な方法（ソーシャルメディア、クリック課金、電子メール、紹介リンクなど）を自動的に並べ替え、バケットまたはチャネルにまとめます。

## 表示されない理由 `channels` MBI で？ {#nochannels}

`Channels` は単純で、データの集計グループです。 獲得をチャネルグループに分類するために、Googleでは、特定のパラメーターを使用して個別のルールと定義を設定しています。獲得の組み合わせ [ソース](https://support.google.com/analytics/answer/1033173?hl=en) （トラフィックの発生元）と獲得 [中](https://support.google.com/analytics/answer/6099206?hl=en) （ソースの一般的なカテゴリ）。

これらのバケットを使用すると、トラフィックの発生元を把握できますが、このデータはチャネルでタグ付けされるのではなく、ソースとメディアを組み合わせてタグ付けされます。 Googleはチャネル情報を 2 つの異なるデータポイントとして送信するので、チャネルのグループ化が [!DNL MBI].

## デフォルトのチャネルグループ化とは何ですか？ 作成方法

デフォルトでは、Googleは 8 つの異なるチャネルを使用して設定します。 作成方法を決定するルールを確認します。

| チャネル | 何だ？ | 作成方法 |
|---|---|---|
| 直接 | サイトに直接アクセスするユーザー。 | ソース= `Direct`<br>AND 中= `(not set); OR Medium = (none)` |
| オーガニック検索 | 未払いの検索エンジンでオーガニックランク付けされたトラフィック。 | 中= `organic` |
| 参照元 | オーガニック検索ではない外部リンク、またはソーシャルネットワーク以外の Web サイトから入ってくるトラフィック。 | 中= `referral` |
| 有料検索 | メディアが「cpc」、「ppc」、または「paidsearch」の UTM トラッキングコードを持つトラフィックで、「Content」に一致しない広告配信ネットワークです。 | 中= `^(cpc|ppc|paidsearch)$`<br>AND 広告配信ネットワーク≠ `Content` |
| Social | ほぼいずれかの [400 のソーシャルネットワーク](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) およびは、広告としてタグ付けされていません。 | ソーシャルソースの参照元= `Yes`<br>OR 中= `^(social|social-network|social-media|sm|social network|social media)$` |
| 電子メール | 「E メール」のメディアでタグ付けされたセッションからのトラフィック。 | メディアの UTM トラッキングコード= `email` |
| 表示 | メディアが表示または cpm の UTM トラッキングコードを持つトラフィック。 また、広告配信ネットワークが「コンテンツ」に一致する AdWords インタラクションも含まれます | 中= `^(display|cpm|banner)$`<br>OR 広告配信ネットワーク= `Content`<br>AND 広告形式≠ `Text` |
| その他 | 「cpc」、「ppc」、「cpv」、「cpa」、「cpp」、「cpp」、「cpp」、「アフィリエイト」のメディアでタグ付けされた他の広告チャネル（有料検索を除く）からのセッション。 | 中= `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## これらのチャネルのグループ化をData Warehouseで再作成する方法 {#recreate}

チャネルは単にソースとメディアの組み合わせであることがわかっているので、Data Warehouseでこれらのグループを再作成する簡単な 3 段階のプロセスです。

1. **を有効にします。[!DNL Google ECommerce]統合**

   [有効化後](../importing-data/integrations/google-ecommerce.md)、必ず [同期](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) **中** および **ソース** フィールドをData Warehouseに追加します。 この作業が完了すると、中規模およびソースの獲得データがData Warehouseに取り込まれます。

1. **Googleチャネルグループ化のマッピングをアップロード**

   時間を節約するために、Commerce は既にデフォルトのグループをファイルとしてマッピングしたテーブルを作成しています。このテーブルは、 [ダウンロード](../../assets/ga-channel-mapping.csv).

   Google Analyticsプロが独自のチャネルを作成した場合は、にファイルをアップロードする前に、特定のルールをマッピングテーブルに追加する必要があります。 [!DNL MBI].

   Adobe Campaign を、 [ファイルのアップロード](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **A と B の間に関係を築く[!DNL Google ECommerce]およびマッピングファイルのアップロード**

   次の間に関係を確立するには[!DNL Google ECommerce]マッピング・テーブル [サポートリクエストを送信](../../guide-overview.md) を Data Analyst チームに連絡し、この記事を参照します。 アナリストが、「 **チャネル** （e コマーステーブル） **完全な更新サイクルの後**&#x200B;の場合、この列は、フィルターまたはグループ化基準で使用する準備が整います。

おめでとうございます。 Data WarehouseにGoogle Analyticsチャネルのグループ化が追加されました。つまり、新しい視点でデータを分析できます。

![チャネル別の注文件数指標のセグメント化](../../assets/GA_Channel_Gif.gif)

この例では、単純なセグメント化を開始しました。 **注文数** 指標別 **チャネル**. 今度は、あなたのターンです — 新しい列をテストし、Google Analyticsチャネルデータで特定できるトレンドを確認してください。

## 関連ドキュメント

* [Report Builderの使用](../../tutorials/using-visual-report-builder.md)
* [予測[!DNL Google ECommerce]データ](../importing-data/integrations/google-ecommerce-data.md)
* [建物[!DNL Google ECommerce]注文と顧客データを含むディメンション](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [最も価値のある獲得ソースとチャネルは何ですか？](../analysis/most-value-source-channel.md)
