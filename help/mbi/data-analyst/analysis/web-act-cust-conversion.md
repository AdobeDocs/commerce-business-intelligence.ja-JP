---
title: Web サイトのアクティビティと顧客コンバージョン率の分析
description: ページビュー数、セッション数、ユーザー数など、Web サイトのアクティビティや、顧客のコンバージョン率を経時的に追跡するダッシュボードの設定方法について説明します。
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# ウェブサイトアクティビティの分析

[!DNL Adobe Commerce Intelligence] では、広告コストデータを他のデータと簡単に統合できます。 これにより、Web サイトでのアクティビティを理解できるだけでなく、Web サイトで登録ユーザーになった訪問者や購入をおこなった訪問者の割合を導き出すことができます。

このトピックでは、ページビュー数、セッション数、ユーザー数など、Web サイトのアクティビティや、顧客のコンバージョン率を経時的に追跡するダッシュボードの設定方法について説明します。

## 前提条件

**広告コストデータをインポート**  — 接続 [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) から [!DNL Adobe Commerce Intelligence]  — これにより、 [!DNL AdWords] は、コマースインテリジェンスで使用します。

**ユーザー獲得チャネルデータの追跡**  — 結ぶには [!DNL Google AdWords] データをデータベース内の特定の注文に対して、 [ユーザーの獲得を追跡する](../analysis/google-track-user-acq.md) 経由 [!DNL Google Analytics E-commerce]. これにより、各注文を UTM ソースとメディアに接続できます。

## ユーザー獲得キャンペーン

このレポートのコレクションは、次を使用して構築されます。

* 接続時に自動的に生成される指標 [!DNL Google AdWords] データ
* アカウントで既に使用可能にする必要がある基本指標（例： ） `Number of orders` および `New users`
* Dimensionを [!DNL Google Analytics Ecommerce] order の utm ソースや order の utm メディアなど、データベースに格納されるデータです。 これらのフィールドがお使いのアカウントで現在使用できない場合は、サポートチームにお問い合わせください

## レポートの作成

**最初に、ページビュー数、セッション数およびユーザー数の推移を示すレポートを作成します。**

1. レポートを作成します。
1. クリック **[!UICONTROL Add Metric]**&#x200B;次に、 [!DNL Google Analytics] セクションを選択し、 `Page Views`.
1. 別の指標を追加し、 [!DNL Google Analytics] セクションの選択 `Sessions`.
1. 3 つ目の指標を追加し、 [!DNL Google Analytics] セクションの選択 `Users`.
1. 期間を 31 日前から 1 日前の移動範囲に変更し、期間を `by day`.
1. レポートに名前を付けます ( 例： `Page views, sessions and users by day`) をクリックし、 **[!UICONTROL Save]**.

**2 番目のレポートでは、過去 1 年間のページビュー数を確認します。**

1. レポートを作成します。
1. クリック **[!UICONTROL Add Metric]**、 [!DNL Google Analytics] セクションを選択し、 _ページビュー数_.
1. 期間を 13 か月前から 1 か月前の移動範囲に変更し、期間を `by month`.
1. レポートに次のような名前を付けます。 `Page views by month,` をクリックし、 **[!UICONTROL Save]**.

**3 つ目のグラフでは、過去 1 年間のバウンス率を確認します。**

1. レポートを作成します。
1. クリック **[!UICONTROL Add Metric]**、 [!DNL Google Analytics] セクションを選択し、 _バウンス率_.
1. 期間を 13 か月前から 1 か月前の移動範囲に変更し、期間を `by month`.
1. レポートに次のような名前を付けます。 `Bounce rate by month`をクリックし、 **[!UICONTROL Save]**.

**再訪問者と比較した、新規訪問者のセッションの平均長さを見てみましょう。**

1. レポートを作成します。
1. クリック **UICONTROL 指標の追加**、 [!DNL Google Analytics] セクションを選択し、 `Average Session Length`.
1. 期間を 13 か月前から 1 か月前の移動範囲に変更し、期間を `by month`?
1. を追加します。 `Group by` を選択し、 `New or returning visitor`.  次を確認します。 `Show All` ボックス次に、 **[!UICONTROL Apply]**.
1. レポートに次のような名前を付けます。 `Average session length`をクリックし、 **[!UICONTROL Save]**.

**次に、過去 30 日間の上位の参照ドメインを確認します。**

1. レポートを作成します。
1. クリック **[!UICONTROL Add Metric]**、 [!DNL Google Analytics] セクションを選択し、 `Sessions`.
1. 期間を 31 日前から 1 日前の移動範囲に変更し、期間を次のように調整します。 `none`.
1. を追加します。 `Group by` を選択し、 `ga:source`.  次を確認します。 _すべて表示_ ボックス次に、 **[!UICONTROL Apply]**.
1. 別の `group by` を選択し、 `ga:medium`. 再度、 `Show All` ボックス次に、 **[!UICONTROL Apply]**.
1. レポートに次のような名前を付けます。 `Top 20 Referring Domains, 30 Days`をクリックし、 **[!UICONTROL Save]**.

**最後に、コンバージョンを見てみましょう。**

1. レポートを作成します。
1. 次の指標を追加します。

* `New users`
   * クリック **[!UICONTROL Hide]** 指標名の下に

* `Number of orders`
   * フィルターを追加 `Customer's order number` = 1 とクリックします。 **[!UICONTROL Apply]**
   * 指標名をクリックし、 `Number of first orders`を選択し、「 **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** 指標

* `Users`
   * **[!UICONTROL Hide]** 指標
   * 期間をに変更します。 `24 months ago to now`を使用し、 `by month`.
   * 次の数式を追加するには、 **[!UICONTROL Formula]**.
   * 「A/D」、「 **[!UICONTROL Apply]**
   * 数式の名前を変更 `Registration conversion`
   * 「B/D」、「 **[!UICONTROL Apply]**
   * 数式の名前を変更 `First order conversion`
   * C/D で、「 **[!UICONTROL Apply]**
   * 数式の名前を変更 `Any order conversion`

* 次のように、レポートに名前を付けます。 `Conversion by month`をクリックし、 **[!UICONTROL Save]**.

## 次の手順

これで、Web トラフィックとコンバージョン率のデータにアクセスできたので、これを掘り下げて、「サイトへのトラフィックを促進するのに最適なサイトはどれですか？」など、ビジネス上の意思決定を促すことができます。 または、ライフタイム値の高い顧客を獲得するのに最も効果的なキャンペーンはどれですか？

広告支出とマーケティング戦略を調整する際、 [!DNL Commerce Intelligence]を繰り返し実行して、会社の進化する優先度に合わせます。
