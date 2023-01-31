---
title: Google Analyticsと UTM 属性
description: Google Analyticsソースの属性設定プロセスについて説明します。
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Google Analyticsと UTM 属性

～することが極めて重要である。 [ユーザー獲得ソースの追跡](../../data-analyst/analysis/google-track-user-acq.md) から [最も効果の高い広告キャンペーンの特定](../../data-analyst/analysis/most-value-source-channel.md). このチュートリアルでは、Google Analyticsソースのアトリビューションプロセスを調べます。 つまり、どの情報が記録されたときか。

## 属性とは

`Attribution` は、特定のアクティビティの参照元を指定することを目的としています。 これらのアクティビティは、通常、マクロ変換またはマイクロ変換です。マクロは、次のようになります。 **purchases**&#x200B;といったミクロなもの **登録，電子メールのサインアップ，ブログコメント，** など。

理想的には、コンバージョンイベントが発生するたびに、参照元が記録されます。 しかし、その原因はどのように決まるのでしょうか。

実際、ユーザーは、多くの場合、マイクロコンバージョンやマクロコンバージョンをヒット/コミットする前に、多くのソースから来ます（例えば、オーガニックからサイトに来て、離れ、有料検索から来て、サイトに直接来る）。 このソーストラッキング情報は、多くの場合、UTM パラメーターを介してサイトに提供されますが、より高度なシステムも存在します。 我々は、我々の目的のために、焦点を当てる [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## 方法 [!DNL Google Analytics] UTM パラメータを介した属性の参照元は？

UTM パラメーターが URL で指定されると、それらは解析され、 [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Web サイトが [!DNL Google Analytics]を使用する場合、UTM を使用する意味はありません。 [!DNL Google Analytics] には、有効期間内に UTM で複数の URL をヒットしたユーザーに対して、どのように対処するかのルールがあります（詳しくは、後で説明します）。 Web サイトで UTM パラメーターを外部データベースに取り込むように設定されている場合、マイクロコンバージョンやマクロコンバージョンが発生したとき ( [!DNL Google Analytics] 変換時に cookie がデータベースにレプリケートされる問題を修正しました。

## 最初のクリックと最後のクリック

### 最後のクリック属性

最後のクリックのアトリビューションは、 [!DNL Google Analytics]. この場合、 [!DNL Google Analytics] cookie は、コンバージョンイベントの前の最後または最新のソースの UTM パラメーターを表し、これがその意味 [データベースに記録される](../../data-analyst/analysis/google-track-user-acq.md). なお、 [!DNL Google Analytics] ユーザーが新しい UTM パラメーターのセットを含む新しい URL をクリックすると、cookie は以前の UTM パラメーターのみを上書きします。

例えば、ユーザーがを通じて最初に Web サイトにアクセスしたとします。 [!DNL Google Analytics][!DNL Google Analytics][!DNL Google Analytics] *有料検索*&#x200B;を返し、 *オーガニック検索*&#x200B;最後に、に戻ります。 *web サイトを直接* または経由 *電子メールリンク* **UTM パラメーターなし** コンバージョンイベントの前に配置されます。 この例では、 [!DNL Google Analytics] cookie には、ユーザーのソースが「オーガニック」と表示されます。これは、変換前の最後のソースを表すからです。 この *パス* が無視されます。 ユーザーが UTM を含む電子メールリンクから Web サイトに訪問した場合、 [!DNL Google Analytics] Cookie の場合、ソースは「email」となります。 したがって、cookie に既存の UTM パラメーターが存在し、ユーザーが直接アクセスする場合、 [!DNL Google Analytics] cookie には、「直接」ではなく、常に UTM パラメーターが表示されます。

>[!NOTE]
>
>特定のユーザーの [!DNL Google Analytics] cookie パラメーターは、cookie が [有効期限](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)または、ユーザーがブラウザーで Cookie を消去したとき。*)

### 最初のクリック属性

一部の有料アトリビューションツールでは、ユーザーのパスでソースの「パンケーキスタック」をキャプチャできます。 この状況では、上の例で、最初のクリックアトリビューションは有料検索を示します。 また、少数の Web サイトでは、パンケーキスタックをキャプチャし、最初のソースをデータベースに保存する独自の cookie を実装しています。

## アトリビューションの分析方法は？

[!DNL Google Analytics] には、Web インターフェイスに 4 つの異なるアトリビューションモデルを実行できる、いくつかの堅牢な機能があります。最初のクリック、最後のクリック、線形（売上高をパス内のすべてのソースに均等に配分）、重み付け（カスタマイズされたアトリビューション）がおこなわれます。

これで、各マイクロコンバージョンまたはマクロコンバージョンのアトリビューションモデルを理解したので、質問は、ユーザーのコンバージョンの全体性をどのように処理するかということになります。  例えば、GA のラストクリックロジックに基づいて記録される UTM を見てみましょう。

* ユーザーがオーガニックに登録する
* 有料検索でのユーザーの最初の購入$5.00
* メール$50.00 でのユーザーの 2 回目の購入
* オーガニック$10.00 でのユーザーの 3 回目の購入

ここで質問します。有料検索から得た売上高はどれくらいですか？  メールから？  オーガニックから？  答えは 5、50、10（つまり、最後のソースが何であったか）と言うことも、すべての売上高を最初のソース（つまり、65 がすべてオーガニックになる）に属性付けすることもできます。 また、重み付け分析を適用したり、線形モデルを適用したりすることもできます（つまり、それぞれ約 22 個）。

## 関連ドキュメント

* [経由で注文のリファラルソースを追跡 [!DNL Google Analytics] E コマース](../importing-data/integrations/google-ecommerce.md)
* [データベース内のユーザー参照元を追跡する](../analysis/google-track-user-acq.md)
* [データベース内のユーザーデバイス、ブラウザー、OS データを追跡する](../analysis/google-track-user-acq.md)
* [最も価値のある獲得ソースとチャネルを見つける](../analysis/most-value-source-channel.md)
* [接続 [!DNL Google Adwords] アカウント](../importing-data/integrations/google-adwords.md)
* [広告キャンペーンの ROI の向上](../analysis/roi-ad-camp.md)
* [での UTM タグ付けの 5 つのベストプラクティス [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
