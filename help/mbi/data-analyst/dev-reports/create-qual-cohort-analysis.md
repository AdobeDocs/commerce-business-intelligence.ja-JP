---
title: 定性コホート分析の作成
description: 定性コホートとは何か、この分析の構築に興味を持つ理由、およびでの作成方法を説明します。 [!DNL MBI].
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# の作成 `Qualitative Cohort Analysis`

あなたは、 [!DNL Adwords] — 獲得した顧客セグメントは、オーガニック検索から獲得した顧客と比べて、LTV が成長しているか。 今までに、 `cohort` 同じレポート内で異なる顧客セグメントを並べて分析した場合、 その場合、 `qualitative cohort analysis` は、これらの質問に答えるのに役立ちます。

この記事では、定性コホートとは何か、この分析の構築に興味を持つ理由と、での分析の作成方法について説明します。 [!DNL MBI].

## 説明 `qualitative cohorts`それでも？ {#whatare}

`Cohort` 一般的な分析は、ライフサイクルにわたって同じ特性を共有するユーザーグループの分析として広く定義できます。 異なるユーザーグループにわたる行動傾向を識別できます。

詳しくは、 [コホート分析](https://www.cohortanalysis.com/).

最も多い `cohort` 分析 [!DNL MBI] 共通の日付（特定の月に初めて購入したすべての顧客のセットなど）でユーザーをグループ化します。 A `qualitative cohort` は少し異なります。時間ベースではない特性によって定義されるユーザーグループです。 以下に例を示します。

* 広告キャンペーンから取得されたすべてのユーザーのセット
* 最初の購入にクーポンが含まれている（または含まれていない）すべてのユーザーのセット
* 特定の年齢に属するすべてのユーザーのセット

## それは通常とどのように違うのですか `cohort` ビルダー？ {#different}

この [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) は、時間ベースの特性を使用してコホートをグループ化するために最適化されています。 これは、特定のユーザーセグメント（例えば、有料検索キャンペーンで獲得したすべてのユーザー）に焦点を当てた分析に最適です。 内 `Cohort Analysis Builder`(1) 特定のユーザーグループに焦点を当て、(2) `cohort` 日付（初回注文日など）に設定している必要があります。

ただし、同じコホートレポート (`paid` 検索対象 `organic` 検索と直接トラフィック（おそらく？）の違いにより、このより高度な分析を `Report Builder`.

## 分析を設定するには、どのような情報をサポートに送信する必要がありますか？ {#support}

の作成 `qualitative cohort` レポート `Report Builder` Adobe・アナリスト・チームが [高度な計算列](../data-warehouse-mgr/creating-calculated-columns.md) を必要なテーブルに追加します。

これらを作成するには、 [サポートチケット](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) （およびこの記事を参照してください。） 次の情報が必要です。

* この `metric` コホート分析を、その分析で使用するテーブル ( 例： `Revenue`( `orders` 表 )。

* この `user segments` データベース内の情報と場所を定義する ( 例：異なる値 `User's referral source`（にネイティブ） `users` テーブルに移動し、 `orders`) をクリックします。

* この `cohort date` 分析で使用する ( 例：の `User's first order date` タイムスタンプ )。 この例では、各セグメントを確認して `How does a user's revenue grow in the months following their first order date?`.

* この `time interval` 分析を確認する必要がある場合 ( 例： `weeks`, `months`または `quarters` 後 `User's first order date`) をクリックします。

Adobeアナリストチームが上記に応答したら、レポートを作成するための新しい高度な計算列が 2 つ追加されます。 その後、以下の指示に従ってこれを行うことができます。

## 定性コホート分析の作成 {#create}

まず、コホートに使用する指標を追加します。各指標に対して 1 回ずつ追加します `cohort` 分析中です。 この例では、累積 `Revenue` 顧客の初回注文から数か月後に、 `User's referral source`. つまり、各セグメントに対して 1 つ追加します `Revenue` 指標とフィルターを指定します。

![](../../assets/qualcohort1.gif)

次に、レポートの時間オプションを 2 つ変更します。

1. を `time interval` から `None`. これは、通常の時間オプションを使用する代わりに、最終的に時間間隔でディメンションとしてグループ化するからです。

1. を `time range` を指定します。

この例では、 `all time` ～の見方 `Revenue`. その後、次の一連のドットが表示されます。

![](../../assets/qualcohort2.gif)

3 つ目は、 `cohorts`. 次に基づいて `cohort date` および `time interval` Adobe・アナリスト・チームに指定した場合、 `cohort` デート。 この例では、カスタムディメンションの名前はです。 `Months between this order and customer's first order date`. このディメンションを使用して、次の操作をおこなう必要があります。

* `Group by` 次元と `group by` オプション

* 次の項目のすべての値を選択 `dimension` あなたが興味を持っている

* を使用 `Show top/bottom option`、関心のある上位 X ヶ月を選択し、 `Months between this order and customer's first order date` ディメンション

これで、各 `cohort` 指定した値。 例を今すぐご覧ください — `Revenue` 各リファラルソースのユーザーによって投稿されました。 `grouped by` 最初の注文からそれ以降の注文までの月数。 また、 `Cumulative perspective` 見る `cohorts'` 集計の増加 — より精度の高い結果の表を見てみましょう。

これは何を意味するのでしょうか？ ここでは、特定のリファラルソースについて説明します。 `Paid search` は、顧客の購入期間の最初の 1 か月で役立ちますが、リピート売上高を伴う顧客ベースの維持に失敗します。 While `Direct Traffic` は、より少ない金額で開始し、後続の月の売上高は、実際には同じペースで累積します。

どんなにさいころをしても `cohort` 分析は、分析ツールボックスの強力なツールです。 このタイプの分析は、従来の `time-based cohorts` できず、より優れたデータ主導型の意思決定を可能にする可能性があります。
