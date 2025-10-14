---
title: 非日付ベース コホートのコホートReport Builder
description: 類似のアクティビティまたは属性でユーザーをグループ化する方法を説明します。
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 76c5329c3f55570fa4e46601e902dc5a09e319e7
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# 非日付ベースのコホートの [!DNL Cohort Report Builder]

この [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) は、マーチャントが時間の経過と共にユーザーの様々なサブセットの動作を研究するのに役立ちます。 以前は、共通の `Cohort Report Builder` でユーザーをグループ化するために `cohort date` が最適化されていました（例えば、特定の月に最初の購入を行ったすべての顧客のセット）。 `Non-Date Based Cohort` 機能を使用して、類似のアクティビティまたは属性でユーザーをグループ化できるようになりました。 この機能の使用例をいくつか見てみましょう。

## ユースケース

これは包括的なリストではありませんが、この機能を使用して実行できる潜在的な分析をいくつか示します。

* [!DNL Google] から獲得した顧客の売上高と [!DNL Facebook] の売上高の比較
* 米国とカナダで初回購入を行った顧客の分析
* 様々な広告キャンペーンで獲得した顧客の行動を見る

## 分析の作成方法

1. 左側のタブの「**[!UICONTROL Report Builder]**」または任意のダッシュボードの「**[!UICONTROL Add Report** > **Create Report]**」をクリックします。

1. `Report Builder Selection` 画面で、「**[!UICONTROL Create Report]**」オプションの横にある「`Visual Report Builder`」をクリックします。

### 指標の追加

`Report Builder` を開いたので、分析を実行する指標（例：`Revenue` または `Orders`）を追加します。

>[!NOTE]
>
>ネイティブの [!DNL Google Analytics] 指標は `Cohort Report Builder` と互換性がありません。 この例の目標は、様々な [!DNL Google Analytics] ソースから取得した初回顧客の売上高の推移を確認することです。

### `Metric View` を `Cohort` に切り替えます。

![1 – 指標ビューをコホートに切り替え &#x200B;](../../assets/1-toggle-metric-view-to-cohort.png)

これにより新しいウィンドウが開き、コホートレポートの詳細を設定できます。

コホートレポートを作成するには、次の 5 つの仕様が必要です。

1. コホートのグループ化方法
1. コホートの選択
1. アクションタイムスタンプ
1. コホートの初回アクションの時間範囲
1. コホート発生後の時間範囲

![&#x200B; コホートグループ &#x200B;](../../assets/2-cohort-groups.png)<!--{: width="200" height="224"}-->



#### &#x200B;1. グループ化 `cohorts`

`Cohorts` は、動作の特性によってグループ化されます。この例では `Customer's first order GA source` です。 ここで使用できるオプションは、指標の `groupable` として既に指定されている列です。

#### &#x200B;2. コホートの選択

指定した特性のすべての結果を表示できます。 これにより多くの `cohorts` が生じる可能性があるので、必要な特定の `cohorts` （`Customer's first order GA source` で使用可能な様々な値に対応）を選択できます。

![&#x200B; コホートグループ &#x200B;](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3.`Action timestamp`

これにより、指標を作成した列以外の日付ベースの列を選択できます。 以下では、指定された `action timestamp` に適用される時間範囲の選択について説明します。

#### 4.`Cohort first action time range`

ここでは、`cohorts action timestamp` を含む日付範囲（つまり、2017 年 11 月から 2018 年 10 月に最初の注文を行ったお客様）を選択します。 これは、移動日付範囲または固定日付範囲にすることができます。

#### 5.`Time range after cohort occurrence`

`cohorts` の推移を月別、週別または年別に表示しますか？ ここで、選択を行います。 そのセクションの下で、`time range` が発生した後の `cohort action timestamp` を選択します。 例えば、アクションの時間範囲内に最初の注文を行った顧客の 12 か月のデータが表示されます。

![&#x200B; コホート – first-action-time-range](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

>[!NOTE]
>
>[!UICONTROL Filters] ビューと `Standard` ビューを切り替えても、指標に適用される `Cohort` ータはそのまま維持されます。

### 関連

[`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md) を参照。
