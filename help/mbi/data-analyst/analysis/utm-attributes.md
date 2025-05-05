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

# [!DNL Google Analytics] と UTM の属性

[ 最もパフォーマンスの高い広告キャンペーンを特定 ](../../data-analyst/analysis/google-track-user-acq.md) するために、[ ユーザー獲得ソースを追跡 ](../../data-analyst/analysis/most-value-source-channel.md) することが重要です。 このトピックでは、[!DNL Google Analytics] ソースアトリビューションプロセスについて説明します。 つまり、どの情報がいつ記録されるか。

## アトリビューションとは

`Attribution` れは、特定のアクティビティのリファラルソースを指定することです。 これらのアクティビティは通常、マクロコンバージョンまたはマイクロコンバージョン、マクロは **購入**、マイクロは **登録、メールのサインアップ、ブログコメント** などです。

理想的には、コンバージョンイベントが発生するたびに、リファラルソースが記録されます。 しかし、ソースはどのように決定されますか？

実際には、ユーザーは、マイクロコンバージョンやマクロコンバージョンをヒット/コミットする前に、多くのソースから来ることがよくあります。 例えば、オーガニック経由でサイトにアクセスしてから出発し、有料検索を使用して来て、出発してから、サイト自体に直接来る場合があります。 このソーストラッキング情報は、多くの場合、UTM パラメーターを介してサイトに提供されますが、より高度なシステムも存在します。 ここでは、[UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998) を重点的に説明します。

## UTM パラメーター [!DNL Google Analytics] 使用したリファラルソースの属性方法

UTM パラメーターが URL で指定されると、これらは解析されて、[!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie) に配置されます。 Web サイトに [!DNL Google Analytics] がない場合、UTM を使用しても意味はありません。 [!DNL Google Analytics] には、有効期間において UTM で複数の URL にヒットしたユーザーを処理する方法のルールがあります（詳しくは後で説明します）。 Web サイトが UTM パラメーターを外部データベースに取り込むように設定されている場合、ミクロまたはマクロの変換が発生すると、変換時の [!DNL Google Analytics] cookie 内の情報がデータベースにレプリケートされます。

## 最初のクリックと最後のクリック

### 最終クリック属性

ラストクリックアトリビューションは、[!DNL Google Analytics] で使用される最も一般的なアトリビューションモデルです。 この場合、[!DNL Google Analytics] Cookie は変換イベント前の最新のソースに対する UTM パラメーターを表し、これが [ データベースに記録 ](../../data-analyst/analysis/google-track-user-acq.md) されます。 [!DNL Google Analytics] cookie は、ユーザーが新しい UTM パラメーターのセットを含む新しい URL をクリックした場合にのみ、以前の UTM パラメーターを上書きします。

例えば、コンバージョンイベントの前に、最初に [!DNL Google Analytics]*有料検索* を使用して web サイトを訪問し、次に *オーガニック検索* を使用して戻り、最後に *web サイト* 直接または *メールリンク&#x200B;***UTM パラメーターなし** を使用して戻ってきたユーザーについて考えてみます。 この例では、[!DNL Google Analytics] Cookie はユーザーのソースがオーガニックであることを示しています。これは、変換前の最後のソースを表すからです。 その最終コンバージョンイベントの前のユーザーの *パス* は無視されます。 代わりに、ユーザーが UTM を使用したメールリンクから web サイトにアクセスした場合、[!DNL Google Analytics] Cookie はソースが「メール」であると言います。 そのため、Cookie に既存の UTM パラメーターがあり、ユーザーが direct を介して入ってきた場合、[!DNL Google Analytics] Cookie は「direct」ではなく UTM パラメーターを表示します。

>[!NOTE]
>
>特定のユーザーの [!DNL Google Analytics] 定の cookie パラメーターは、その cookie が [ 期限切れ ](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage) になったとき、またはユーザーがブラウザーで cookie をクリアしたときに消去されます。*

### ファーストクリック属性

一部の有料アトリビューションツールでは、ユーザーのパス内のソースの「パンケーキスタック」をキャプチャできます。 この場合、上記の例では、最初のクリック属性は有料検索を示します。 また、一部の web サイトでは、パンケーキスタックをキャプチャして最初のソースをデータベースに保存する独自の Cookie を実装しています。

## アトリビューションの分析方法

[!DNL Google Analytics] の web インターフェイスには、4 つの異なるアトリビューションモデルを実行できる堅牢な機能がいくつかあります。

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

* [E-Commerce経由  [!DNL Google Analytics]  注文リファラルソースを追跡](../importing-data/integrations/google-ecommerce.md)
* [データベース内のユーザー紹介ソースを追跡](../analysis/google-track-user-acq.md)
* [データベース内のユーザーデバイス、ブラウザー、OS データの追跡](../analysis/google-track-user-acq.md)
* [最も価値のある獲得ソースとチャネルを見つける](../analysis/most-value-source-channel.md)
* [アカウント  [!DNL Google Adwords]  接続](../importing-data/integrations/google-adwords.md)
* [広告キャンペーンの ROI の向上](../analysis/roi-ad-camp.md)
* [での UTM タグ付けの 5 つのベストプラクティス  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
