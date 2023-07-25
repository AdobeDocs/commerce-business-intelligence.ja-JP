---
title: Google Analyticsと UTM 属性
description: Google Analyticsソースの属性設定プロセスについて説明します。
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# [!DNL Google Analytics] および UTM 属性

～することが極めて重要である。 [ユーザー獲得ソースの追跡](../../data-analyst/analysis/google-track-user-acq.md) から [最も効果の高い広告キャンペーンの特定](../../data-analyst/analysis/most-value-source-channel.md). このトピックでは、 [!DNL Google Analytics] ソース属性プロセス。 つまり、どの情報が記録されたときか。

## 属性とは

`Attribution` は、特定のアクティビティの参照元を指定することを目的としています。 これらのアクティビティは、通常、マクロ変換またはマイクロ変換です。マクロは、次のようになります。 **purchases**&#x200B;といったミクロなもの **登録，電子メールのサインアップ，ブログコメント，** など。

理想的には、コンバージョンイベントが発生するたびに、参照元が記録されます。 しかし、その原因はどのように決まるのでしょうか。

実際には、ユーザーは多くのソースから来て、マイクロやマクロの変換をヒット/コミットする前に来ることが多いのです。 例えば、オーガニック経由でサイトに来て、その後、有料検索から来て、その後サイトを離れて、サイト自体に直接来る場合があります。 このソーストラッキング情報は、多くの場合、UTM パラメーターを介してサイトに提供されますが、より高度なシステムも存在します。 目的に合わせて、 [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## 方法 [!DNL Google Analytics] UTM パラメータを介した属性の参照元は？

UTM パラメーターが URL で指定されると、それらは解析され、 [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Web サイトが [!DNL Google Analytics]を使用する場合、UTM を使用する意味はありません。 [!DNL Google Analytics] には、有効期間中に UTM で複数の URL をヒットしたユーザーを扱う方法のルールがあります（詳しくは、後で説明します）。 Web サイトで、UTM パラメーターを外部データベースに取り込むように設定されていると仮定します。このとき、マイクロコンバージョンまたはマクロコンバージョンが発生したとき、 [!DNL Google Analytics] 変換時に cookie がデータベースにレプリケートされる。

## 最初のクリックと最後のクリック

### 最後のクリック属性

最後のクリックのアトリビューションは、 [!DNL Google Analytics]. この場合、 [!DNL Google Analytics] cookie は、コンバージョンイベントの前の最新のソースの UTM パラメーターを表し、これは [データベースに記録される](../../data-analyst/analysis/google-track-user-acq.md). この [!DNL Google Analytics] ユーザーが新しい UTM パラメーターのセットを含む新しい URL をクリックすると、cookie は以前の UTM パラメーターのみを上書きします。

例えば、ユーザーがを通じて最初に Web サイトにアクセスしたとします。 [!DNL Google Analytics] *有料検索*&#x200B;を返し、 *オーガニック検索*&#x200B;最後に、に戻ります。 *web サイトを直接* または経由 *電子メールリンク* **UTM パラメーターなし** コンバージョンイベントの前に配置されます。 この例では、 [!DNL Google Analytics] cookie には、ユーザーのソースが「オーガニック」と表示されます。これは、変換前の最後のソースを表すからです。 この *パス* の値は、その最終的なコンバージョンイベントの前のユーザーに対しては無視されます。 ユーザーが UTM を含む電子メールリンクから Web サイトに訪問した場合、 [!DNL Google Analytics] Cookie の場合、ソースは「email」となります。 したがって、cookie に既存の UTM パラメーターが存在し、ユーザーが直接アクセスする場合、 [!DNL Google Analytics] cookie には、「直接」ではなく UTM パラメーターが表示されます。

>[!NOTE]
>
>特定のユーザーの [!DNL Google Analytics] cookie のパラメーターは、cookie の作成時に消去されます [有効期限](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)、またはユーザーがブラウザーで Cookie をクリアした場合に発生します。*

### 最初のクリック属性

一部の有料アトリビューションツールでは、ユーザーのパスでソースの「パンケーキスタック」をキャプチャすることができます。 この場合、上の例では、最初にクリックしたアトリビューションによって有料検索が示されます。 また、一部の Web サイトでは、パンケーキスタックをキャプチャし、最初のソースをデータベースに保存する独自の Cookie を実装しています。

## アトリビューションの分析方法は？

[!DNL Google Analytics] には、Web インターフェイスに 4 つの異なるアトリビューションモデルを実行できるいくつかの堅牢な機能があります。

1. 最初のクリック
1. 最後のクリック
1. 線形（売上高をパスのすべてのソースに均等に配分）
1. 重み付け（カスタマイズされたアトリビューション）

これで、各マイクロコンバージョンまたはマクロコンバージョンのアトリビューションモデルを理解したので、質問は「ユーザーのコンバージョンの全体をどのように扱うのか」になります。  例えば、GA のラストクリックロジックに基づいて記録される UTM を見てみましょう。

* ユーザーがオーガニックに登録する
* 有料検索でのユーザーの最初の購入$5.00
* メール$50.00 でのユーザーの 2 回目の購入
* オーガニック$10.00 でのユーザーの 3 回目の購入

ここでは「有料検索で得た売上高はどれくらいですか？ メールから？  オーガニックから？」 回答が 5、50、10（最後のソースが何であったか）と言うことも、すべての売上高を最初のソースに属性付けする（65 はすべてオーガニックになります）と言うこともできます。 また、重み付け分析を適用したり、線形モデルを適用したりすることもできます（つまり、それぞれ約 22 個）。

## 関連ドキュメント

* [経由で注文のリファラルソースを追跡 [!DNL Google Analytics] E コマース](../importing-data/integrations/google-ecommerce.md)
* [データベース内のユーザー参照元を追跡する](../analysis/google-track-user-acq.md)
* [データベース内のユーザーデバイス、ブラウザー、OS データを追跡する](../analysis/google-track-user-acq.md)
* [最も価値のある獲得ソースとチャネルを見つける](../analysis/most-value-source-channel.md)
* [接続 [!DNL Google Adwords] アカウント](../importing-data/integrations/google-adwords.md)
* [広告キャンペーンの ROI の向上](../analysis/roi-ad-camp.md)
* [での UTM タグ付けの 5 つのベストプラクティス [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
