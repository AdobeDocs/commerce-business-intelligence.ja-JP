---
title: Google Analytics - ユーザー獲得ソースデータのトラッキングの概要
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
>以下のプロセスはサポートしていません [!DNL Google Universal Analytics].

マーケティングプランを効果的に管理するには、ユーザー獲得ソースでデータをセグメント化する機能が重要です。 新しいユーザーの獲得ソースを把握すると、どのチャネルが最も高いリターンを生み出すかを示し、チームが自信を持ってマーケティングドルを割り当てることができます。

データベース内のユーザー獲得ソースをまだトラッキングしていない場合は、 [!DNL Adobe Commerce Intelligence] 作業を開始する際に役立ちます。

## ユーザー獲得ソースのトラッキング

[!DNL Adobe] では、設定に基づいてリファラルソースデータを追跡する 2 つの方法をお勧めします。

### （オプション 1）を介した注文リファラルソースデータのトラッキング [!DNL Google Analytics E-Commerce]

を使用する場合 [!DNL Google Analytics E-Commerce] 注文および販売データを追跡するには、を使用できます [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) 各注文の参照元データを同期します。 これにより、リファラルソース（など）別に売上高と注文をセグメント化できます。 `utm_source` または `utm_medium`）に設定します。 また、次のような方法で、顧客獲得ソースを把握できます [!DNL Commerce Intelligence] カスタムディメンション（例：） `User's first order source`.

### （オプション 2）保存 [!DNL Google Analytics]データベース内の獲得ソースデータ

このトピックでは、保存方法を説明します [!DNL Google Analytics] 獲得チャネル情報を独自のデータベースに –  `source`, `medium`, `term`, `content`, `campaign`、および `gclid` ユーザーの初めての web サイト訪問時に存在したパラメーター。 これらのパラメータの詳細については、 [[!DNL Google Analytics] 詳細を見る](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). 次に、この情報を使用して実行できる強力なマーケティング分析をいくつか見ていきます。 [!DNL Commerce Intelligence].

#### なぜでしょうか。

デフォルトの場合は、次のようになります [!DNL Google Analytics] コンバージョンと獲得の指標については、全体像を把握しているわけではありません。 オーガニック検索と有料検索のコンバージョン数の比較は興味深いものですが、この情報で何ができますか？ 有料検索にもっと金を使うべきですか？ これは、そのチャネルから生じる顧客の価値によって異なり、Google Analyticsが提供するものではありません。

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) トランザクションデータをに保存することでこの問題を軽減します [!DNL Google Analytics]ただし、このソリューションは e コマース以外のサイトには機能しません。 また、コホート分析などの特定のツールは、 [!DNL Google Analytics] インターフェイス。

特定のメールキャンペーンから取得したすべての顧客にフォローアップの契約をメールで送信する場合はどうすればよいですか？ または、獲得データを CRM システムと統合しますか？ では不可能です。 [!DNL Google Analytics]  – 実際、次のサービス利用規約に反します： [!DNL Google Analytics] 個人を識別するデータを格納する場合。 ただし、このデータは自分で保存できます。

#### メソッド

[!DNL Google Analytics] という cookie に訪問者の参照情報を格納します `__utmz`. この Cookie の設定後（ [!DNL Google Analytics] トラッキングコード）、そのコンテンツは、そのユーザーからドメインに後続のリクエストのたびに送信されます。 例えば PHP では、以下の内容を確認できます。 `$_COOKIE['__utmz']` 次のような文字列が表示されます。

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

文字列にエンコードされた何らかの取得元データがあることは明らかです。 これは、訪問者の最新の獲得ソースおよび関連するキャンペーンデータであることを確認するためにテストされています。 次に、データの抽出方法を知る必要があります。

このコードはに変換されました [github でホストされる PHP ライブラリ](https://github.com/RJMetrics/referral-grabber-php). ライブラリを使用するには、 `include` 対する参照 `ReferralGrabber.php` を呼び出します

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

返された `$data` 配列はキーのマップです `source`, `medium`, `term`, `content`, `campaign`, `gclid`、およびそれぞれの値。

Adobeでは、データベースにというテーブルを追加することをお勧めします。例： `user_referral`：次のような列を持ちます。 `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. ユーザーがサインアップするたびに、参照情報を取得してこのテーブルに保存します。

#### このデータの使用方法

ユーザー獲得ソースを保存している今、どのように使用できますか？

SQL データベースを使用していて、 `users` 次の構造を持つテーブル：

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
* A [コホート分析](https://en.wikipedia.org/wiki/Cohort_analysis) 各ソースからのユーザーの
* これらのチャネルのいずれかからのユーザーが将来、顧客として返される確率

これらの分析を行うために必要なクエリは複雑です。 この情報に基づいて、最も収益性の高い獲得チャネルを決定し、それに応じてマーケティング時間と費用を集中させることができます。

### 関連

* **[最も価値のある獲得ソースとチャネルを見つける](../analysis/most-value-source-channel.md)**
* **[を接続 [!DNL Google Adwords] アカウント](../importing-data/integrations/google-adwords.md)**
* **[広告キャンペーンの ROI の向上](../analysis/roi-ad-camp.md)**
* **[方法 [!DNL Google Analytics] UTM アトリビューションの仕組み](../analysis/utm-attributes.md)**
