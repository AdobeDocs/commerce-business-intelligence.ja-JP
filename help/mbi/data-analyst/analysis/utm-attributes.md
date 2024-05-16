---
title: Google Analyticsと UTM 属性
description: Google Analyticsソースアトリビューションプロセスについて説明します。
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Google Analytics] および UTM アトリビューション

～することが極めて重要である [ユーザー獲得ソースの追跡](../../data-analyst/analysis/google-track-user-acq.md) 対象： [最もパフォーマンスの高い広告キャンペーンを特定する](../../data-analyst/analysis/most-value-source-channel.md). このトピックでは、について説明します [!DNL Google Analytics] ソース属性プロセス。 つまり、どの情報がいつ記録されるか。

## アトリビューションとは

`Attribution` は、特定のアクティビティのリファラルソースを指定することを目的としています。 これらのアクティビティは通常、マクロコンバージョンまたはマイクロコンバージョンで、マクロは次のようになります **購入**（ミクロは～のようなもの） **登録，メールのサインアップ，ブログコメント，** その他。

理想的には、コンバージョンイベントが発生するたびに、リファラルソースが記録されます。 しかし、ソースはどのように決定されますか？

実際には、ユーザーは、マイクロコンバージョンやマクロコンバージョンをヒット/コミットする前に、多くのソースから来ることがよくあります。 例えば、オーガニック経由でサイトにアクセスしてから出発し、有料検索を使用して来て、出発してから、サイト自体に直接来る場合があります。 このソーストラッキング情報は、多くの場合、UTM パラメーターを介してサイトに提供されますが、より高度なシステムも存在します。 目的に応じて、次を重視します [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## 方法 [!DNL Google Analytics] UTM パラメーターを使用したリファラルソースの属性

UTM パラメーターが URL で指定されると、これらは解析されて、に配置されます。 [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Web サイトに次の情報がない場合： [!DNL Google Analytics]、UTM を使用しても意味はありません。 [!DNL Google Analytics] には、有効期間中に UTM で複数の URL にヒットしたユーザーを処理する方法のルールがあります（詳しくは後で説明します）。 Web サイトが UTM パラメーターを外部データベースに取り込むように設定されている場合、ミクロまたはマクロの変換が発生すると、 [!DNL Google Analytics] 変換時の cookie がデータベースにレプリケートされます。

## 最初のクリックと最後のクリック

### 最終クリック属性

最終クリック数アトリビューションは、が採用する最も一般的なアトリビューションモデルです [!DNL Google Analytics]. この場合、 [!DNL Google Analytics] cookie は、コンバージョンイベントより前の最新のソースに対する UTM パラメーターを表します。これは [データベースに記録される](../../data-analyst/analysis/google-track-user-acq.md). この [!DNL Google Analytics] cookie は、ユーザーが新しい UTM パラメーターセットを含む新しい URL をクリックした場合にのみ、以前の UTM パラメーターを上書きします。

例えば、最初にを介して web サイトを訪問するユーザーについて考えてみます [!DNL Google Analytics] *有料検索*&#x200B;を選択すると、から次の経路で戻ります *オーガニック検索*&#x200B;最後に、に戻ります *web サイトを直接参照* または *メールリンク* **UTM パラメーターなし** コンバージョンイベントの前。 この例では、 [!DNL Google Analytics] cookie は、ユーザーのソースが変換前の最後のソースを表すため、ユーザーのソースがオーガニックであると言います。 この *パス* その最終コンバージョンイベントの前のユーザーのは無視されます。 代わりに、ユーザーが UTM を使用したメールリンクから web サイトにアクセスした場合は、 [!DNL Google Analytics] cookie はソースが「email」と言います。 そのため、Cookie に既存の UTM パラメーターがあり、ユーザーが直接経由でアクセスする場合、 [!DNL Google Analytics] cookie は、「直接」ではなく UTM パラメーターを表示します。

>[!NOTE]
>
>特定のユーザーの [!DNL Google Analytics] cookie のパラメーターは次の場合に消去されます [expires](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)または、ユーザーがブラウザーで Cookie をクリアした場合に発生します。*

### ファーストクリック属性

一部の有料アトリビューションツールでは、ユーザーのパス内のソースの「パンケーキスタック」をキャプチャできます。 この場合、上記の例では、最初のクリック属性は有料検索を示します。 また、一部の web サイトでは、パンケーキスタックをキャプチャして最初のソースをデータベースに保存する独自の Cookie を実装しています。

## アトリビューションの分析方法

[!DNL Google Analytics] には、4 つの異なるアトリビューションモデルを実行できる堅牢な機能が web インターフェイスに含まれています。

1. 最初のクリック
1. 前回のクリック
1. 線形（パス内のすべてのソースにわたって売上高を均等に分割）
1. 重み付け（カスタマイズされた属性）

マイクロコンバージョンまたはマクロコンバージョンごとのアトリビューションモデルを理解できたので、「ユーザーのコンバージョン全体はどうしますか？」という質問になります。  例えば、GA のラストクリックロジックに基づいて記録された UTM を見てみましょう。

* ユーザーはオーガニックに登録
* 有料検索でのユーザーの最初の購入$5.00
* ユーザーの 2 回目の電子メール購入$50.00
* オーガニック$10.00 未満でのユーザーの 3 回目の購入

「有料検索でどのくらいの売上高を得られましたか？ メールから？  オーガニックから？」 答えは 5、50、10 （最後のソースが何であれ）と言えます。または、すべての売上高を最初のソースに関連付ける（65 のすべてがオーガニックに分類される）と言うこともできます。 また、一部の重み付け解析を適用したり、線形モデル（つまり、それぞれ約 22 個）を適用することもできます。

## 関連ドキュメント

* [以下を介した注文参照ソースの追跡 [!DNL Google Analytics] 電子Commerce](../importing-data/integrations/google-ecommerce.md)
* [データベース内のユーザー紹介ソースを追跡](../analysis/google-track-user-acq.md)
* [データベース内のユーザーデバイス、ブラウザー、OS データの追跡](../analysis/google-track-user-acq.md)
* [最も価値のある獲得ソースとチャネルを見つける](../analysis/most-value-source-channel.md)
* [を接続 [!DNL Google Adwords] アカウント](../importing-data/integrations/google-adwords.md)
* [広告キャンペーンの ROI の向上](../analysis/roi-ad-camp.md)
* [での UTM タグ付けの 5 つのベストプラクティス [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
