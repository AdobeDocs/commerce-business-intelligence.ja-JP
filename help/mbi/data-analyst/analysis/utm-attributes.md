---
title: Google AnalyticsとUTM アトリビューション
description: Google Analyticsのソースアトリビューションプロセスについてご確認ください。
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Developer, User
feature: Reports
TQID: https://experienceleague.adobe.com/DIg4HPkxaY4eCXZvTS8j4eO8C-d-yqPgBkrvFD5L0ms
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 781
ht-degree: 0%

---

# [!DNL Google Analytics]とUTM アトリビューション

ユーザー獲得ソースを[追跡](../../data-analyst/analysis/google-track-user-acq.md)して[最もパフォーマンスの高い広告キャンペーンを特定](../../data-analyst/analysis/most-value-source-channel.md)することが重要です。 このトピックでは、[!DNL Google Analytics] ソースのアトリビューションプロセスについて説明します。 つまり、どの時点で情報が記録されるのか。

## アトリビューションとは？

`Attribution`は、特定のアクティビティのリファラルソースを指定することです。 これらのアクティビティは、通常、マクロコンバージョンまたはマイクロコンバージョンです。マクロには、**購入**&#x200B;や、**登録、電子メール登録、ブログコメント、**&#x200B;などがあります。

コンバージョンイベントが発生するたびに、参照元が記録されることが望ましいです。 しかし、その源泉はどのように決まるのでしょうか。

実際には、多くのユーザーは、マイクロコンバージョンやマクロコンバージョンに達する前に、多くのソースからもたらされます。 例えば、オーディエンスはオーガニック広告を通じてサイトにアクセスし、そのままサイトを離れたあと、有料検索を通じてサイトを離れたあと、サイト自体に直接移動しました。 このソース追跡情報は、UTM パラメーターを介してサイトに提供されることが多いものの、より高度なシステムも存在します。 目的に応じて、[UTM](https://support.google.com/analytics/answer/1033867?hl=en&ref_topic=1032998)に焦点を当てます。

## [!DNL Google Analytics]は、UTM パラメーターを使用してリファラルソースをどのように属性しますか？

UTM パラメーターをURLで指定すると、これらは解析され、[!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie)に配置されます。 Web サイトに[!DNL Google Analytics]がない場合、UTMを使用しても意味がありません。 [!DNL Google Analytics]には、有効期間の間にUTMで複数のURLをヒットしたユーザーを扱うルールがあります（後で詳しく説明します）。 Web サイトがUTM パラメーターを外部データベースに取り込むように設定されていると仮定すると、マイクロ変換またはマクロ変換が発生すると、変換時に[!DNL Google Analytics] Cookie内にあるものは何でもデータベースにレプリケートされます。

## ファーストクリックとラストクリックの比較

### ラストクリックアトリビューション

ラストクリックアトリビューションは、[!DNL Google Analytics]が使用する最も一般的なアトリビューションモデルです。 この場合、[!DNL Google Analytics] Cookieは、コンバージョンイベントの前の最新のソースのUTM パラメーターを表し、これは[&#x200B; データベース &#x200B;](../../data-analyst/analysis/google-track-user-acq.md)に記録されます。 ユーザーが新しいUTM パラメーターのセットを含む新しいURLをクリックした場合にのみ、[!DNL Google Analytics] Cookieは以前のUTM パラメーターを上書きします。

例えば、コンバージョンイベントの前に[!DNL Google Analytics] *有料検索*&#x200B;を介して初めてweb サイトにアクセスし、*オーガニック検索*&#x200B;を介して戻り、最終的に&#x200B;*web サイトに直接*&#x200B;または&#x200B;*電子メールリンク&#x200B;***経由で戻り、UTM パラメーターを使用せずに**&#x200B;というユーザーを考えてみましょう。 この例では、[!DNL Google Analytics] Cookieは、ユーザーのソースがオーガニックであると示します。これは、コンバージョンの前の最後のソースを表すためです。 最終変換イベントの前のユーザーの&#x200B;*パス*&#x200B;は無視されます。 代わりに、ユーザーがUTMを使用した電子メールリンクからweb サイトにアクセスした場合、[!DNL Google Analytics] Cookieは、ソースが「電子メール」であると示します。 したがって、cookieに既存のUTM パラメーターがあり、ユーザーが直接経由でアクセスした場合、[!DNL Google Analytics] cookieには「direct」ではなくUTM パラメーターが表示されます。

>[!NOTE]
>
>特定のユーザーの[!DNL Google Analytics] cookie パラメーターは、cookie [の有効期限](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)が切れるか、ユーザーがブラウザーでCookieをクリアすると消去されます*。

### ファーストクリックアトリビューション

一部の有料アトリビューションツールでは、ユーザーのパス内のソースの「パンケーキスタック」をキャプチャできます。 上記の例では、ファーストクリックアトリビューションで有料検索が可能です。 あるいは、一部のweb サイトでは、パンケーキスタックをキャプチャし、最初のソースをデータベースに保存する独自のCookieを実装しています。

## アトリビューションの分析方法？

[!DNL Google Analytics]には、4つの異なるアトリビューションモデルを実行できる堅牢な機能がweb インターフェイスにあります。

1. ファーストクリック
1. 最後のクリック
1. 線形（経路のすべてのソースにわたって収益を均等に分割）
1. 重み付け（カスタマイズされた属性）

マイクロコンバージョンやマクロコンバージョンごとのアトリビューションモデルを理解したところで、「ユーザーのコンバージョンの全体をどうするか」という質問になります。  例えば、GAのラストクリックロジックに基づいて記録されたUTMを確認します。

* オーガニックでユーザー登録
* 有料検索でのユーザーの最初の購入$5.00
* ユーザーの電子メールでの2回目の購入$50.00
* オーガニック $10.00の下でのユーザーの3回目の購入

ここでは、「検索連動型広告からどの程度の収益を得たか？」という質問があります。 メールから？  オーガニックから？」 答えは5、50、10 （最後のソースが何であれ）と言うこともできますし、すべての売上を最初のソースに帰することもできます（65はすべてオーガニックに行きます）。 重み付け分析を適用したり、線形モデル（各約22）を適用したりすることもできます。

## 関連ドキュメント

* [&#x200B; [!DNL Google Analytics] E-Commerce経由で注文の紹介ソースを追跡](../importing-data/integrations/google-ecommerce.md)
* [データベース内のユーザー紹介ソースの追跡](../analysis/google-track-user-acq.md)
* [データベース内のユーザーデバイス、ブラウザー、OS データの追跡](../analysis/google-track-user-acq.md)
* [最も価値のある獲得ソースとチャネルの発見](../analysis/most-value-source-channel.md)
* [&#x200B; [!DNL Google Adwords]  アカウントを接続](../importing-data/integrations/google-adwords.md)
* [広告キャンペーンのROIを高める](../analysis/roi-ad-camp.md)
* [&#x200B; [!DNL Google Analytics]でのUTM タグ付けに関する5つのベストプラクティス](../../best-practices/utm-tagging-google.md)
