---
title: 非日付ベースのコホートのコホートReport Builder
description: 類似のアクティビティまたは属性でユーザーをグループ化する方法を説明します。
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# `Cohort Report Builder for Non-Date-Based Cohorts`

この [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) は、時間の経過と共に様々なユーザーサブセットがどのように動作するかを商人が調べるのに役立ちました。 以前は、 `Cohort Report Builder` は、共通のユーザーのグループ化用に最適化されています `cohort date` （例えば、特定の月に初めて購入したすべての顧客のセット）。 この `Non-Date Based Cohort` 機能を使用すると、類似のアクティビティや属性でユーザーをグループ化できます。 この機能の使用例をいくつか見てみましょう。

## 使用例

これは包括的なリストではありませんが、この機能で実行できる潜在的な分析を次に示します。

* ～から得た顧客の収益の調査 [!DNL Google] 対比 [!DNL Facebook]
* 米国とカナダで初めて購入した顧客の分析
* 様々な広告キャンペーンから獲得した顧客の行動を調べる

## 分析の作成方法

1. クリック **[!UICONTROL Report Builder]** ( 左側のタブまたは **[!UICONTROL Add Report** > **Create Report]** （任意のダッシュボード）

1. 内 `Report Builder Selection` 画面、クリック **[!UICONTROL Create Report]** の横 `Visual Report Builder` オプション。

### 指標の追加

これで、 `Report Builder`に値を入力する場合は、分析を実行する指標を追加します ( 例： `Revenue` または `Orders`) をクリックします。

>[!NOTE]
>
>ネイティブ [!DNL Google Analytics] 指標は `Cohort Report Builder`. この例の目標は、様々な GA ソースから獲得したファーストオーダー顧客の売上高の推移を見ることです。

### 切り替え `Metric View` から `Cohort`

![指標表示をコホートに 1 切り替え](../../assets/1-toggle-metric-view-to-cohort.png)

新しいウィンドウが開き、コホートレポートの詳細を設定できます。

コホートレポートを作成するには、次の 5 つの仕様が必要です。

1. コホートのグループ化方法
1. コホートの選択
1. アクションタイムスタンプ
1. コホートの最初のアクションの時間範囲
1. コホート発生後の時間範囲

![コホートグループ](../../assets/2-cohort-groups.png){:width=&quot;200&quot; height=&quot;224&quot;}

![コホート — 最初のアクション — 時間範囲](../../assets/3-cohort-first-action-time-range.png){:width=&quot;400&quot; height=&quot;554&quot;}

#### 1.グループ化 `cohorts`

`Cohorts` は、動作特性別にグループ化されています ( この例では `Customer's first order GA source`. ここで使用できるオプションは、既に `groupable` を参照してください。

#### 2.コホートの選択

指定した特性のすべての結果を表示できます。 これは多くの結果を招く可能性があるので `cohorts`を選択すると、特定の `cohorts` ( これは、 `Customer's first order GA source`) をクリックします。

![コホートグループ](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

これにより、指標が作成される列以外の日付ベースの列を選択できます。 以下では、特定の `action timestamp`.

#### 4. `Cohort first action time range`

ここで、 `cohorts action timestamp` （2017 年 11 月～ 2018 年 10 月の最初のご注文をお持ちのお客様の場合）。 日付範囲は、移動日付範囲または固定日付範囲で指定できます。

#### 5. `Time range after cohort occurrence`

次の項目を表示しますか： `cohorts` 月別、週別、年別に ここで選択を行います。 このセクションの下で、 `time range` 後 `cohort action timestamp` が発生しました。 例えば、この例では、アクション期間内に最初の注文をした顧客の 12 ヶ月分のデータが表示されます。

![コホート — 最初のアクション — 時間範囲](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

### その他のメモ

* [!UICONTROL Filters]:を切り替えても、指標はそのまま残ります。 `Standard` および `Cohort` ビュー
* 詳しくは、 [`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md).
