---
title: Google Analytics — ユーザー獲得ソースデータの追跡の概要
description: ユーザーの獲得ソース別にデータをセグメント化する方法を説明します。
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 3098909fdccb726108c24f2424e4ba4c1db9d1c2
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 1%

---

# ユーザーの獲得ソース別のセグメント化

>[!NOTE]
>
>以下のプロセスはをサポートしていません [!DNL Google Universal Analytics].

マーケティングプランを効果的に管理するには、ユーザーの獲得ソースごとにデータをセグメント化する機能が重要です。 新しいユーザーの獲得ソースを把握することで、どのチャネルが最も高い収益率をもたらすかを示し、チームが自信を持ってマーケティングドルを割り当てることができます。

データベース内のユーザー獲得ソースをまだ追跡していない場合は、 [!DNL Adobe Commerce Intelligence] では、以下の作業を開始できます。

## ユーザーの獲得ソースの追跡

[!DNL Adobe] では、の設定に基づいてリファラルソースデータを追跡する 2 つの方法を推奨しています。

### （オプション 1）を介して注文の紹介元データを追跡する [!DNL Google Analytics E-Commerce]

次を使用する場合、 [!DNL Google Analytics E-Commerce] 注文と販売のデータを追跡するには、 [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) 各注文のリファラルソースデータを同期する。 これにより、紹介ソース ( 例えば、 `utm_source` または `utm_medium`) をクリックします。 また、 [!DNL Commerce Intelligence] カスタムディメンション： `User's first order source`.

### （オプション 2）保存 [!DNL Google Analytics]データベース内の&#39;獲得ソースデータ

このトピックでは、保存方法を説明します。 [!DNL Google Analytics] 獲得チャネル情報を独自のデータベース ( つまり、 `source`, `medium`, `term`, `content`, `campaign`、および `gclid` ユーザーが Web サイトに初めてアクセスする際に使用したパラメーター。 これらのパラメーターの説明については、 [[!DNL Google Analytics] ドキュメント](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). 次に、この情報を使用して実行できる、強力なマーケティング分析をいくつか調べます ( [!DNL Commerce Intelligence].

#### なぜ？

デフォルトの [!DNL Google Analytics] コンバージョン指標と獲得指標の両方を使用している場合、画像全体が取得されるわけではありません。 オーガニック検索と有料検索のコンバージョン数は興味深いものですが、その情報を使用して何ができるのでしょうか。 有料検索にもっとお金を使うべきですか？ これは、Google Analyticsが提供するものではない、そのチャネルからの顧客の価値に依存します。

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) トランザクションデータを次の場所に保存することで、この問題を軽減します。 [!DNL Google Analytics]ですが、このソリューションは e コマース以外のサイトでは機能しません。 また、コホート分析などの特定のツールは、 [!DNL Google Analytics] インターフェイス。

特定のメールキャンペーンから取得したすべての顧客にフォローアップ契約をメールで送信する場合はどうすればよいですか。 または、獲得データを CRM システムと統合しますか？ これは～では不可能だ [!DNL Google Analytics]  — 実際、これは、のサービス利用規約に反しています [!DNL Google Analytics] 個人を識別するデータを保存する。 しかし、このデータは自分で保存できます。

#### メソッド

[!DNL Google Analytics] 訪問者のリファラル情報を `__utmz`. この cookie が設定された後 ( [!DNL Google Analytics] トラッキングコード ) の場合、そのコンテンツは以降そのユーザーからのドメインへのリクエストが発生するたびに送信されます。 PHP では、例えば、 `$_COOKIE['__utmz']` 次のような文字列が表示されます。

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

文字列にエンコードされた獲得ソースデータが明らかに一部存在します。 これが訪問者の最新の獲得ソースおよび関連するキャンペーンデータであることを確認するためにテストされます。 次に、データの抽出方法を知っておく必要があります。

このコードは、 [github でホストされる PHP ライブラリ](https://github.com/RJMetrics/referral-grabber-php). ライブラリを使用するには、 `include` ～への言及 `ReferralGrabber.php` その後、

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

返された `$data` 配列はキーのマップです `source`, `medium`, `term`, `content`, `campaign`, `gclid`、およびそれぞれの値。

Adobeでは、という名前のテーブルをデータベースに追加することをお勧めします。例： `user_referral`を作成し、次のような列を含めます。 `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. ユーザーがサインアップするたびに、紹介情報を取得してこのテーブルに保存します。

#### このデータの使用方法

ユーザーの獲得ソースを保存したので、どのように使用できますか？

SQL データベースを使用していて、 `users` 次の構造を持つテーブル：

| ID | 電子メール | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | 有機 |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | 直接 | - |
| 4 | jess@ghi.com | 2012-01-26 | リファラル | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | その他 | 有機 |
| ... | ... | ... | ... | ... |

まず、データベースに対して次のクエリを実行して、各リファラルチャネルからのユーザー数をカウントできます。

`SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

結果は次のようになります。

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| 直接 | 156 |
| リファラル | 55 |
| その他 | 16 |

これは面白いが、限られた使い方だ。 実際に知りたいことは次のとおりです。

* 時間の経過に伴うこれらの数の増加率
* 各獲得ソースで生み出された売上高
* A [コホート分析](https://en.wikipedia.org/wiki/Cohort_analysis) 各ソースから来るユーザーの数
* これらのチャネルの 1 つからのユーザーが将来顧客として返される確率

これらの分析の実行に必要なクエリは複雑です。 この情報を活用すると、最も収益性の高い獲得チャネルを特定し、それに応じてマーケティングの時間とお金に焦点を当てることができます。

### 関連

* **[最も価値のある獲得ソースとチャネルを見つける](../analysis/most-value-source-channel.md)**
* **[接続する [!DNL Google Adwords] アカウント](../importing-data/integrations/google-adwords.md)**
* **[広告キャンペーンの ROI の向上](../analysis/roi-ad-camp.md)**
* **[方法 [!DNL Google Analytics] UTM 属性は機能しますか？](../analysis/utm-attributes.md)**
