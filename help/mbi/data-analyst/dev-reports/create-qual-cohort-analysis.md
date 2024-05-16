---
title: 定性コホート分析の作成
description: 定性的コホートとは何か、この分析の構築に興味を持つ理由、Commerce Intelligence での分析作成方法について説明します。
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# を作成 `Qualitative Cohort Analysis`

あなたの方法を知っていますか [!DNL Google Adwords] – 獲得した顧客セグメントは、オーガニック検索で獲得した顧客と比較して LTV を伸ばしていますか？ ～を演じようと思ったことはありますか？ `cohort` 同じレポートで異なる顧客セグメントを並べて分析 もしそうなら、 `qualitative cohort analysis` これらの質問に答えるのに役立ちます。

このトピックでは、定性的コホートの概要、この分析の構築に興味を持つ理由、での作成方法について説明します [!DNL Commerce Intelligence].

## について `qualitative cohorts`とにかくね？ {#whatare}

`Cohort` 分析一般には、ライフサイクルを通じて類似した特性を共有するユーザーグループの分析と定義できます。 これにより、様々なユーザーグループにわたる行動のトレンドを特定できます。

参照： [コホート分析](https://www.cohortanalysis.com/).

Most `cohort` での分析 [!DNL Commerce Intelligence] 共通の日付（特定の月に最初の購入を行ったすべての顧客のセットなど）でユーザーをグループ化します。 A `qualitative cohort` 少し異なります。時間ベースではない特性によって定義されるユーザーグループです。 例を次に示します。

* 広告キャンペーンから取得したすべてのユーザーのセット
* 最初の購入にクーポンが含まれている（または含まれていない）すべてのユーザーのセット
* 特定の年齢のすべてのユーザーのセット

## それが通常とどう違うか `cohort` ビルダー？ {#different}

この [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) は、時間ベースの特性を使用してコホートをグループ化するために最適化されています。 これは、特定のユーザーのセグメント（有料検索キャンペーンで取得したすべてのユーザーなど）に焦点を当てた分析に最適です。 が含まれる `Cohort Analysis Builder`を使用すると、（1）その特定のユーザーグループにフォーカスすることができます。（2） `cohort` 日付（最初の注文日と同様に）に。

ただし、同じコホートレポートで複数のユーザーセグメントのコホート動作を分析する場合（`paid` 検索と `organic` 検索と直接トラフィックなど）、より高度な分析は、次の場所で構築できます。 `Report Builder`.

## 分析を設定するには、どのような情報をサポートに送信するとよいですか？ {#support}

の作成 `qualitative cohort` のレポート `Report Builder` は、Adobeアナリストチームが一部を作成する必要があります [高度な計算列](../data-warehouse-mgr/creating-calculated-columns.md) 必要なテーブルで。

これを作成するには、 [サポートチケット](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) （この記事を参照してください。 必要な知識を次に示します。

* この `metric` コホート分析に使用するテーブルと使用するテーブルを指定する（例： `Revenue`、にビルド `orders` テーブル）に保存します。

* この `user segments` その情報がデータベース内のどこにあるかを定義する場合（例：の異なる値） `User's referral source`、ネイティブ `users` テーブルを次の場所に移動 `orders`）に設定します。

* この `cohort date` 分析で使用する（例： `User's first order date` timestamp）を参照してください。 この例を使用すると、各セグメントを確認して尋ねることができます `How does a user's revenue grow in the months following their first order date?`.

* この `time interval` 分析を確認する場合（例： `weeks`, `months`、または `quarters` 後 `User's first order date`）に設定します。

Adobeアナリストチームが上記の手順に従ったら、新しい高度な計算列をいくつか用意して、レポートを作成できます。 次に、以下の手順に従ってこれを行うことができます。

## 定性コホート分析の作成 {#create}

まず、調整する指標を各 1 回ずつ追加します `cohort` 分析しています。 この例では、累積を表示します `Revenue` 顧客の初回注文後の数か月で行われ、によってセグメント化される `User's referral source`. つまり、セグメントごとに 1 つ追加します `Revenue` 特定のセグメントの指標とフィルター：

![](../../assets/qualcohort1.gif)

次に、レポートの時間オプションを 2 回変更する必要があります。

1. を `time interval` 対象： `None`. これは、通常の時間オプションを使用する代わりに、最終的にディメンションとして時間間隔でグループ化するためです。

1. を `time range` レポートの対象とする時間帯に追加します。

この例では、を確認します。 `all time` の表示 `Revenue`. この後、一連のドットで終わります。

![](../../assets/qualcohort2.gif)

3 番目に、 `cohorts`. に基づく `cohort date` および `time interval` Adobeアナリストチームに指定した場合、を実行するディメンションがアカウントに存在します `cohort` デート中。 この例では、そのカスタムディメンションはと呼ばれます `Months between this order and customer's first order date`. このディメンションを使用すると、次のことができます。

* `Group by` を含むディメンション `group by` オプション

* の値をすべて選択 `dimension` 関心のあるもの

* （を使用） `Show top/bottom option`を選択し、関心のある上位 X か月を選択して、で並べ替えます `Months between this order and customer's first order date` 寸法

これで、各行を 1 行ずつ表示できるようになります `cohort` を指定しました。 今すぐ例を確認してください。次が表示されます。 `Revenue` 各リファラルソースのユーザーが投稿、 `grouped by` 最初の注文から後続の注文までの月数。 この例では、も追加されています。 `Cumulative perspective` を表示するには `cohorts'` 集計値の増加：詳細については、結果の表を参照してください。

これは何を意味しますか？ ここでは、特定のリファラルソース `Paid search` は、顧客の購入有効期間の最初の 1 か月では価値がありますが、リピート収益があるにもかかわらず、顧客ベースを維持できません。 While `Direct Traffic` より少ない金額で開始し、その後の数か月の収益は実際には同様のペースで累積されます。

どんなに細かく言っても `cohort` analysis は、analysis ツールボックスの強力なツールです。 このタイプの分析は、従来のようなビジネスに関する興味深いインサイトを得ることができます `time-based cohorts` できない場合があり、データに基づいた意思決定を向上させることができます。
