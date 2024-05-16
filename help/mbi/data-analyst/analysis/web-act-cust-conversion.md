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

**広告コストデータの読み込み**  – 接続 [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) 対象： [!DNL Adobe Commerce Intelligence]  – これは自動的に [!DNL AdWords] Commerce Intelligence でお過ごしください。

**ユーザー獲得チャネルデータの追跡**  – を結び付ける [!DNL Google AdWords] データをデータベース内の特定の順序に変換するには、次の操作を行う必要があります [ユーザー獲得の追跡](../analysis/google-track-user-acq.md) 経由 [!DNL Google Analytics E-commerce]. これにより、各注文を utm ソースとメディアに接続できます。

## ユーザー獲得キャンペーン

このレポートコレクションは、次を使用して構築されています。

* を接続すると自動的に生成される指標 [!DNL Google AdWords] データ
* お使いのアカウントで既に使用可能になっている基本的な指標（など） `Number of orders` および `New users`
* に参加する際に作成されたDimension [!DNL Google Analytics Ecommerce] 注文の utm ソースや注文の utm メディアなどのデータをデータベースに送信します。 お使いのアカウントでこれらのフィールドが現在使用できない場合は、サポートチームにお問い合わせください

## レポートの作成

**まず、ページビュー数、セッション数およびユーザー数の推移を示すレポートを作成します。**

1. レポートを作成します。
1. クリック **[!UICONTROL Add Metric]**&#x200B;その後、上にマウスを移動 [!DNL Google Analytics] ドロップダウンの下部にあるセクションを選択し、 `Page Views`.
1. 別の指標を追加し、再び上にマウスポインターを置きます [!DNL Google Analytics] セクション、今回は選択 `Sessions`.
1. 3 番目の指標を追加し、再び上にマウスポインターを置きます [!DNL Google Analytics] セクション、今回は選択 `Users`.
1. 次に、期間を 31 日前から 1 日前までの移動範囲に変更し、時間間隔を次のように調整します `by day`.
1. レポートに名前を付けます（例： `Page views, sessions and users by day`）を選択し、をクリックします **[!UICONTROL Save]**.

**2 つ目のレポートは、過去 1 年間のページビュー数を示しています。**

1. レポートを作成します。
1. クリック **[!UICONTROL Add Metric]**、マウスで囲む [!DNL Google Analytics] ドロップダウンの下部にあるセクションを選択し、 _ページビュー_.
1. 期間を 13 か月前から 1 か月前の移動範囲に変更し、時間間隔を次のように調整します `by month`.
1. レポートに次のような名前を付けます `Page views by month,` をクリックして、 **[!UICONTROL Save]**.

**3 つ目のグラフは、過去 1 年間のバウンス率を示しています。**

1. レポートを作成します。
1. クリック **[!UICONTROL Add Metric]**、マウスで囲む [!DNL Google Analytics] ドロップダウンの下部にあるセクションを選択し、 _バウンス率_.
1. 期間を 13 か月前から 1 か月前の移動範囲に変更し、時間間隔を次のように調整します `by month`.
1. レポートに次のような名前を付けます `Bounce rate by month`を選択し、 **[!UICONTROL Save]**.

**次に、再訪問者と比較した、新規訪問者のセッションの平均長さを見てみましょう。**

1. レポートを作成します。
1. クリック **UICONTROL 指標の追加**、マウスで囲む [!DNL Google Analytics] ドロップダウンの下部にあるセクションを選択し、 `Average Session Length`.
1. 期間を 13 か月前から 1 か月前の移動範囲に変更し、時間間隔を次のように調整します `by month`?
1. を追加 `Group by` を選択して、 `New or returning visitor`.  を確認します `Show All` ボックス、次に **[!UICONTROL Apply]**.
1. レポートに次のような名前を付けます `Average session length`を選択し、 **[!UICONTROL Save]**.

**次に、過去 30 日間の上位の参照ドメインを確認します。**

1. レポートを作成します。
1. クリック **[!UICONTROL Add Metric]**、マウスで囲む [!DNL Google Analytics] ドロップダウンの下部にあるセクションを選択し、 `Sessions`.
1. 期間を 31 日前から 1 日前までの移動範囲に変更し、時間間隔を次のように調整します `none`.
1. を追加 `Group by` を選択して、 `ga:source`.  を確認します _すべてを表示_ ボックス、次に **[!UICONTROL Apply]**.
1. さらに追加 `group by` を選択して、 `ga:medium`. もう一度確認します `Show All` ボックス、次に **[!UICONTROL Apply]**.
1. レポートに次のような名前を付けます `Top 20 Referring Domains, 30 Days`を選択し、 **[!UICONTROL Save]**.

**最後に、コンバージョンについて説明します。**

1. レポートを作成します。
1. 次の指標を追加します。

* `New users`
   * クリック **[!UICONTROL Hide]** 指標名の下

* `Number of orders`
   * のフィルターを追加 `Customer's order number` = 1 で、をクリックします **[!UICONTROL Apply]**
   * 指標名をクリックして呼び出すことにより、指標の名前を変更します `Number of first orders`を選択し、 **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** 指標

* `Users`
   * **[!UICONTROL Hide]** 指標
   * 期間をに変更します。 `24 months ago to now`、および時間間隔を次のように調整します `by month`.
   * をクリックして、次の式を追加します。 **[!UICONTROL Formula]**.
   * A/D をクリックしてから、 **[!UICONTROL Apply]**
   * 式の名前の変更 `Registration conversion`
   * B/D 次にクリック **[!UICONTROL Apply]**
   * 式の名前の変更 `First order conversion`
   * C/D をクリックしてから、 **[!UICONTROL Apply]**
   * 式の名前の変更 `Any order conversion`

* 次のように、レポートに名前を付けます `Conversion by month`を選択し、 **[!UICONTROL Save]**.

## 次の手順

Web トラフィックおよびコンバージョン率に関するデータにアクセスできるようになったので、これをマイニングして、サイトへのトラフィックを促進するのに最適なサイトはどれかなど、ビジネス上の意思決定を促進できます。 または、生涯価値の高い顧客を獲得する上で最も効果的なキャンペーンはどれですか？

広告費用とマーケティング戦略を調整する際に、結果を次の場所で引き続き追跡できます [!DNL Commerce Intelligence]。会社の進化する優先度に合わせて、このダッシュボードを繰り返し処理します。
