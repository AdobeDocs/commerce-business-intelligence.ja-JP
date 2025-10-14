---
title: Web サイトのアクティビティと顧客コンバージョン率の分析
description: ページビュー、セッション、ユーザーを含む web サイトのアクティビティおよび顧客コンバージョン率を経時的に追跡する、ダッシュボードの設定方法を説明します。
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Web サイトアクティビティの分析

[!DNL Adobe Commerce Intelligence] を使用すると、広告コストデータを他のデータと簡単に統合できます。 これにより、web サイトのアクティビティを理解できるだけでなく、web サイト上で、登録ユーザーになったり購入したりする訪問者の割合を導き出すことができます。

このトピックでは、ページビュー数、セッション数、ユーザー数などの web サイトアクティビティと、時間の経過に伴う顧客コンバージョン率を追跡する、ダッシュボードの設定方法について説明します。

## 前提条件

**広告コストデータのインポート** - [[!DNL [Google AdWords]]](../importing-data/integrations/google-adwords.md) を [!DNL Adobe Commerce Intelligence] に接続すると、Commerce Intelligenceでの [!DNL AdWords] 広告の支出が自動的に同期されます。

**ユーザー獲得チャネルデータの追跡** - [!DNL Google AdWords] データをデータベース内の特定の注文に関連付けるには、[&#x200B; を介して &#x200B;](../analysis/google-track-user-acq.md) ユーザー獲得を追跡 [!DNL Google Analytics E-commerce] する必要があります。 これにより、各注文を utm ソースとメディアに接続できます。

## ユーザー獲得キャンペーン

このレポートコレクションは、次を使用して構築されています。

* [!DNL Google AdWords] データの接続時に自動的に生成される指標
* `Number of orders` や `New users` など、アカウントで既に使用可能になっている基本指標
* 注文の utm ソースや注文の utm メディアなど、[!DNL Google Analytics Ecommerce] データをデータベースに結合する際に作成されるディメンション。 お使いのアカウントでこれらのフィールドが現在使用できない場合は、サポートチームにお問い合わせください

## レポートの作成

**まず、ページビュー数、セッション数およびユーザー数の推移を示すレポートを作成します。**

1. レポートを作成します。
1. 「**[!UICONTROL Add Metric]**」をクリックして、ドロップダウンの下部にある「[!DNL Google Analytics]」セクションにマウスを移動し、「`Page Views`」を選択します。
1. 別の指標を追加し、再び「[!DNL Google Analytics]」セクションにマウスポインターを置いて、今度は「`Sessions`」を選択します。
1. 3 つ目の指標を追加し、再び「[!DNL Google Analytics]」セクションにマウスポインターを置き、今回は「`Users`」を選択します。
1. 次に、期間を 31 日前から 1 日前までの移動範囲に変更し、時間間隔を `by day` に調整します。
1. レポートに名前（例：`Page views, sessions and users by day`）を付け、「**[!UICONTROL Save]**」をクリックします。

**2 番目のレポートは、過去 1 年間のページビュー数を示しています**。

1. レポートを作成します。
1. 「**[!UICONTROL Add Metric]**」をクリックし、ドロップダウンの下部にある「[!DNL Google Analytics]」セクションにマウスを移動して、「_ページビュー_」を選択します。
1. 期間を 13 か月前から 1 か月前の移動範囲に変更し、時間間隔を `by month` に調整します。
1. レポートに `Page views by month,` などの名前を付け、「**[!UICONTROL Save]**」をクリックします。

**3 つ目のグラフは、過去 1 年間のバウンス率を示しています**

1. レポートを作成します。
1. 「**[!UICONTROL Add Metric]**」をクリックし、ドロップダウンの下部にある「[!DNL Google Analytics]」セクションにマウスポインターを置いて、「_バウンス率_」を選択します。
1. 期間を 13 か月前から 1 か月前の移動範囲に変更し、時間間隔を `by month` に調整します。
1. レポートに `Bounce rate by month` のような名前を付け、「**[!UICONTROL Save]**」をクリックします。

**次に、再訪問者と比較した、新規訪問者のセッションの平均長さを見てみましょう。**

1. レポートを作成します。
1. **UICONTROL 指標を追加** をクリックし、ドロップダウンの下部にある「[!DNL Google Analytics]」セクションにマウスポインターを置いて、「`Average Session Length`」を選択します。
1. 期間を 13 か月前から 1 か月前の移動範囲に変更し、時間間隔を `by month` に調整しますか？
1. `Group by` を追加し、「`New or returning visitor`」を選択します。  「`Show All`」ボックスを選択し、「**[!UICONTROL Apply]**」をクリックします。
1. レポートに `Average session length` のような名前を付け、「**[!UICONTROL Save]**」をクリックします。

**次に、過去 30 日間に上位の参照ドメインを確認します。**

1. レポートを作成します。
1. 「**[!UICONTROL Add Metric]**」をクリックし、ドロップダウンの下部にある「[!DNL Google Analytics]」セクションにマウスを移動して「`Sessions`」を選択します。
1. 期間を 31 日前から 1 日前の移動範囲に変更し、時間間隔を `none` に調整します。
1. `Group by` を追加し、「`ga:source`」を選択します。  _すべて表示_ ボックスをオンにし、**[!UICONTROL Apply]** をクリックします。
1. 別の `group by` を追加し、`ga:medium` を選択します。 再度、「`Show All`」チェックボックスをオンにし、「**[!UICONTROL Apply]**」をクリックします。
1. レポートに `Top 20 Referring Domains, 30 Days` のような名前を付け、「**[!UICONTROL Save]**」をクリックします。

**最後に、コンバージョンを見てみましょう。**

1. レポートを作成します。
1. 次の指標を追加します。

* `New users`
   * 指標名の下にある「**[!UICONTROL Hide]**」をクリックします

* `Number of orders`
   * `Customer's order number` = 1 のフィルターを追加して、「**[!UICONTROL Apply]**」をクリックします。
   * 指標名をクリックして `Number of first orders` 呼び出すことにより、指標の名前を変更し、「**[!UICONTROL Hide]**」をクリックします

* `Number of orders`
   * 指標の **[!UICONTROL Hide]**

* `Users`
   * 指標の **[!UICONTROL Hide]**
   * 期間を `24 months ago to now` に変更し、時間間隔を `by month` に調整します。
   * 「**[!UICONTROL Formula]**」をクリックして、次の式を追加します。
   * A/D をクリックしてから **[!UICONTROL Apply]** をクリック
   * 式の名前を `Registration conversion` に変更
   * B/D をクリックしてから「**[!UICONTROL Apply]**」をクリック
   * 式の名前を `First order conversion` に変更
   * C/D をクリックしてから **[!UICONTROL Apply]**
   * 式の名前を `Any order conversion` に変更

* 次に、レポートに `Conversion by month` のような名前を付け、[**[!UICONTROL Save]**] をクリックします。

## 次の手順

Web トラフィックおよびコンバージョン率に関するデータにアクセスできるようになったので、これをマイニングして、サイトへのトラフィックを促進するのに最適なサイトはどれかなど、ビジネス上の意思決定を促進できます。 または、生涯価値の高い顧客を獲得する上で最も効果的なキャンペーンはどれですか？

広告費用とマーケティング戦略を調整しながら、[!DNL Commerce Intelligence] で結果を追跡し続け、このダッシュボードを繰り返して、会社の進化する優先度に合わせることができます。
