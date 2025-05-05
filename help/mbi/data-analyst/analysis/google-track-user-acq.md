---
title: Google Analytics - ユーザー獲得の追跡Source データの概要
description: ユーザー獲得ソース別にデータをセグメント化する方法を説明します。
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 3098909fdccb726108c24f2424e4ba4c1db9d1c2
workflow-type: tm+mt
source-wordcount: '751'
ht-degree: 1%

---

# ユーザー獲得ソースによるセグメント化

>[!NOTE]
>
>以下のプロセスは [!DNL Google Universal Analytics] をサポートしていません。

マーケティングプランを効果的に管理するには、ユーザー獲得ソースでデータをセグメント化する機能が重要です。 新しいユーザーの獲得ソースを把握すると、どのチャネルが最も高いリターンを生み出すかを示し、チームが自信を持ってマーケティングドルを割り当てることができます。

データベース内のユーザー獲得ソースをまだトラッキングしていない場合は、[!DNL Adobe Commerce Intelligence] の方法を開始すると役立ちます。

## ユーザー獲得ソースのトラッキング

[!DNL Adobe] では、設定に基づいてリファラルソースデータを追跡する 2 つの方法をお勧めします。

### （オプション 1） [!DNL Google Analytics E-Commerce] を介した注文リファラルソースデータの追跡

[!DNL Google Analytics E-Commerce] を使用して注文および販売データを追跡する場合は、[[!DNL [Google Analytics E-Commerce Connector]]](../importing-data/integrations/google-ecommerce.md) を使用して各注文のリファラルソースデータを同期できます。 これにより、売上高と注文をリファラルソース（`utm_source` や `utm_medium` など）別にセグメント化できます。 また、`User's first order source` などのカスタムディメンションを使用して、顧客獲得ソース [!DNL Commerce Intelligence] 把握できます。

### （オプション 2） [!DNL Google Analytics] の取得元データをデータベースに保存する

このトピックでは [!DNL Google Analytics] ユーザーが初めて Web サイトを訪問した際に存在した `source`、`medium`、`term`、`content`、`campaign` および `gclid` のパラメーターなど、獲得チャネルの情報を独自のデータベースに保存する方法について説明します。 これらのパラメーターについて詳しくは、[[!DNL Google Analytics]  ドキュメント ](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article) を参照してください。 次に、この情報を使用して [!DNL Commerce Intelligence] で実行できる強力なマーケティング分析をいくつか見ていきます。

#### なぜでしょうか。

コンバージョンおよび獲得指標 [!DNL Google Analytics] デフォルト値を見ているだけでは、全体像を把握することはできません。 オーガニック検索と有料検索のコンバージョン数の比較は興味深いものですが、この情報で何ができますか？ 有料検索にもっと金を使うべきですか？ これは、そのチャネルから生じる顧客の価値によって異なり、Google Analyticsが提供するものではありません。

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) は、トランザクションデータを [!DNL Google Analytics] に保存することでこの問題を軽減しますが、このソリューションは e コマース以外のサイトには機能しません。 また、コホート分析などの特定のツールは、[!DNL Google Analytics] インターフェイスで簡単に実行できません。

特定のメールキャンペーンから取得したすべての顧客にフォローアップの契約をメールで送信する場合はどうすればよいですか？ または、獲得データを CRM システムと統合しますか？ これは [!DNL Google Analytics] では不可能です。実際、個人を識別するデータを保存することは、[!DNL Google Analytics] の利用規約に反します。 ただし、このデータは自分で保存できます。

#### メソッド

[!DNL Google Analytics] は、訪問者の参照情報を `__utmz` という cookie に格納します。 [!DNL Google Analytics] トラッキングコードによってこの cookie が設定された後は、そのユーザーからのドメインへの後続のリクエストのたびに、その内容が送信されます。 例えば PHP では、`$_COOKIE['__utmz']` の内容をチェックすると、次のような文字列が表示されます。

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

文字列にエンコードされた何らかの取得元データがあることは明らかです。 これは、訪問者の最新の獲得ソースおよび関連するキャンペーンデータであることを確認するためにテストされています。 次に、データの抽出方法を知る必要があります。

このコードは、github でホストされる [PHP ライブラリ ](https://github.com/RJMetrics/referral-grabber-php) に変換されました。 ライブラリを使用するには、`ReferralGrabber.php` への参照を `include` し、次にを呼び出します

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

返される `$data` 配列は、キー `source`、`medium`、`term`、`content`、`campaign`、`gclid` およびそれぞれの値のマップです。

Adobeでは、例えば `user_referral` というテーブルを、`id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)` のような列を使用して、データベースに追加することをお勧めします。 ユーザーがサインアップするたびに、参照情報を取得してこのテーブルに保存します。

#### このデータの使用方法

ユーザー獲得ソースを保存している今、どのように使用できますか？

SQL データベースを使用していて、次の構造の `users` テーブルがあるとします。

| ID | 電子メール | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | 器質性 |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | ダイレクト | - |
| 4 | jess@ghi.com | 2012-01-26 | リファラル | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | その他 | 器質性 |
| ... | ... | ... | ... | ... |

まず、データベースに対して次のクエリを実行して、各紹介チャネルからのユーザーの数をカウントできます。

`SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

結果は次のようになります。

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| ダイレクト | 156 |
| リファラル | 55 |
| その他 | 16 |

これは興味深いものですが、使用が制限されています。 実際に知りたいのは次のとおりです。

* これらの数値の経時的な成長率
* 各獲得ソースによって生成された収益の額
* 各ソースからのユーザーの [ コホート分析 ](https://en.wikipedia.org/wiki/Cohort_analysis)
* これらのチャネルのいずれかからのユーザーが将来、顧客として返される確率

これらの分析を行うために必要なクエリは複雑です。 この情報に基づいて、最も収益性の高い獲得チャネルを決定し、それに応じてマーケティング時間と費用を集中させることができます。

### 関連

* **[最も価値の高い獲得ソースとチャネルを見つける](../analysis/most-value-source-channel.md)**
* **[アカウント  [!DNL Google Adwords]  接続](../importing-data/integrations/google-adwords.md)**
* **[広告キャンペーンの ROI の向上](../analysis/roi-ad-camp.md)**
* **[UTM アトリビ  [!DNL Google Analytics]  ーションはどのように機能しますか？](../analysis/utm-attributes.md)**
