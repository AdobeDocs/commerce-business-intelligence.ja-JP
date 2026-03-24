---
title: Google Analytics - ユーザー獲得の追跡Source データの概要
description: ユーザー獲得ソース別にデータをセグメンテーションする方法について説明します。
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/nqiC-AsuhdcOrxqFsW9ZqRZvlL8Ndu9xmNrTi-pvgv8
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 751
ht-degree: 1%

---

# ユーザー獲得ソース別セグメンテーション

>[!NOTE]
>
>以下のプロセスは[!DNL Google Universal Analytics]をサポートしていません。

ユーザー獲得ソースごとにデータをセグメンテーションできることは、マーケティングプランを効果的に管理するために不可欠です。 新規ユーザーの獲得ソースを把握することで、どのチャネルが最も高いリターンを生み出すのかを把握し、マーケティング予算を確実に配分することができます。

データベース内のユーザー獲得ソースをまだ追跡していない場合は、[!DNL Adobe Commerce Intelligence]を使用して開始できます。

## ユーザー獲得ソースのトラッキング

[!DNL Adobe]では、設定に基づいてリファラルソースデータを追跡する2つの方法をお勧めします。

### （オプション 1） [!DNL Google Analytics E-Commerce]経由で注文の参照元データを追跡する

[!DNL Google Analytics E-Commerce]を使用して注文と販売データを追跡する場合は、[!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md)を使用して、各注文の参照元データを同期できます。 これにより、収益と注文を参照元（`utm_source`または`utm_medium`など）別にセグメント化できます。 [!DNL Commerce Intelligence]などの`User's first order source`個のカスタムディメンションを使用して、顧客獲得ソースを確認することもできます。

### （オプション 2）取得ソースデータをデータベースに保存する[!DNL Google Analytics]

このトピックでは、[!DNL Google Analytics]獲得チャネル情報を独自のデータベースに保存する方法について説明します。つまり、`source`、`medium`、`term`、`content`、`campaign`、および`gclid` パラメーターは、ユーザーのweb サイトへの初回訪問時に存在していました。 これらのパラメーターの説明については、[[!DNL Google Analytics]  ドキュメント ](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article)を参照してください。 次に、[!DNL Commerce Intelligence]でこの情報を使用して実行できる強力なマーケティング分析の一部について説明します。

#### なぜでしょうか？

デフォルトの[!DNL Google Analytics] コンバージョン指標と獲得指標だけを見ている場合は、全体像を把握しているわけではありません。 オーガニック検索と有料検索のコンバージョン数の違いは興味深いものですが、その情報をどのように活用すればよいでしょうか？ 検索連動型広告の予算を増やすには？ これは、Google Analyticsが提供するものではなく、そのチャネルから流入する顧客の価値によって決まります。

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce)は、トランザクションデータを[!DNL Google Analytics]に保存することによってこの問題を軽減しますが、このソリューションはe コマースサイト以外では機能しません。 また、コホート分析などの特定のツールは、[!DNL Google Analytics] インターフェイスでは実行が簡単ではありません。

特定の電子メールキャンペーンから取得したすべての顧客に、フォローアップの成約を電子メールで送信する場合はどうすればよいですか？ または、獲得データをCRM システムと統合するのか？ これは[!DNL Google Analytics]では不可能です。実際、[!DNL Google Analytics]が個人を特定するデータを保存することは、サービス利用規約に違反します。 しかし、このデータは自分で保存することができます。

#### メソッド

[!DNL Google Analytics]は、訪問者の参照情報を`__utmz`というCookieに保存します。 このCookieが（[!DNL Google Analytics] トラッキングコードによって）設定されると、そのコンテンツは、そのユーザーから後続のすべてのリクエストとともにドメインに送信されます。 例えば、PHPでは、`$_COOKIE['__utmz']`の内容をチェックアウトすると、次のような文字列が表示されます。

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

文字列にエンコードされた取得ソースデータがあることは明らかです。 このテストは、訪問者の最新の獲得ソースおよび関連するキャンペーンデータであることを確認するために実行されます。 データを抽出する方法を知る必要があります。

このコードは、github[でホストされている](https://github.com/RJMetrics/referral-grabber-php)PHP ライブラリに変換されました。 ライブラリを使用するには、`include`が`ReferralGrabber.php`への参照を呼び出してから

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

返された`$data`配列は、キー`source`、`medium`、`term`、`content`、`campaign`、`gclid`およびそれぞれの値のマップです。

Adobeでは、`user_referral`という名前のテーブルをデータベースに追加することをお勧めします。列は`id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`のようになります。 オーディエンスが登録するたびに、紹介情報を取得し、このテーブルに保存します。

#### このデータの活用方法

ユーザー獲得ソースを保存したら、どのように使用できますか？

SQL データベースを使用しており、次の構造を持つ`users` テーブルがあるとします。

| ID | メール | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | オーガニック |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | 直接 | - |
| 4 | jess@ghi.com | 2012-01-26 | リファラル | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | その他 | オーガニック |
| ... | ... | ... | ... | ... |

まず、データベースに対して次のクエリを実行することで、各紹介チャネルから来るユーザーの数を数えることができます。

`SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

結果は次のようになります。

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| 直接 | 156 |
| リファラル | 55 |
| その他 | 16 |

これは面白いですが、使い方が限られています。 本当に知りたいことは：

* これらの数値の長期的な成長率
* 各獲得ソースが生成した収益の量
* 各ソースからのユーザーの[ コホート分析](https://en.wikipedia.org/wiki/Cohort_analysis)
* これらのチャネルのいずれかに属するユーザーが、将来顧客として戻る可能性があります

これらの分析を行うために必要なクエリは複雑です。 この情報をもとに、最も収益性の高い獲得チャネルを特定し、それに応じてマーケティング時間と予算を投入できます。

### 関連

* **[最も価値のある獲得ソースとチャネルの発見](../analysis/most-value-source-channel.md)**
* **[アカウントを [!DNL Google Adwords] 接続](../importing-data/integrations/google-adwords.md)**
* **[広告キャンペーンのROIを向上](../analysis/roi-ad-camp.md)**
* **[UTM アトリビューションの仕組みは [!DNL Google Analytics] どのようになっていますか？](../analysis/utm-attributes.md)**
