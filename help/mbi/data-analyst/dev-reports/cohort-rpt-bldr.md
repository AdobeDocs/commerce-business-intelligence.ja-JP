---
title: コホートReport Builder
description: ライフサイクルで類似した特性を共有するユーザーグループの分析について説明します。
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# コホートReport Builder

時間の経過と共にユーザーの様々なサブセットがどのように動作するかを研究したいと思ったことはありますか？ 例えば、プロモ期間中に登録したユーザーの平均生涯売上高が、そうでないユーザーの平均生涯売上高よりも高いかどうか疑問に思ったことはありませんか。 答えが `Yes` い場合は、`Cohort Report Builder` が最適なツールです。 [!DNL Adobe Commerce Intelligence] は、この分析を実行し、ビジネスに関連づけるために最適化されています。

## コホート分析とは {#what}

分析 `Cohort`、ライフサイクル全体で類似した特性を共有するユーザーグループの分析として広く定義できます。 これにより、様々なユーザーグループにわたる行動のトレンドを特定できます。

分析に関する詳細な入門 `cohort` ついては、[ このページ ](https://www.cohortanalysis.com/) を参照してください。

[!DNL Commerce Intelligence] ダッシュボードでは、`cohort` 定の日付とアカウントの指標に基づいて、ユーザー `cohorts` を簡単に作成できます。

## コホート分析はなぜ重要なのでしょうか？ {#important}

前述のように、分析 `cohort` 使用すると、様々なユーザーグループ間の行動のトレンドを特定できます。 特定のグループの行動をしっかりと理解することで、決定と支出を調整して売上を最大化できます。 例えば、生涯売上高 `cohort` 分析を取り上げます。この種の分析は多くの理由で有益ですが、すぐに行う方が、顧客の獲得に関する意思決定を向上させることができます。

## 独自の `cohort` 分析を作成するにはどうすればよいですか？

### 新しいアーキテクチャ

[ 新しいアーキテクチャ ](../../administrator/account-management/new-architecture.md) の `Cohort Report Builder` を使用する手順を以下に示します。

1. 左側のタブの「**[!UICONTROL Report Builder]**」または任意のダッシュボードの「**[!UICONTROL Add Report** > **Create Report]**」をクリックします。

1. `Report Builder` 選択画面で、「`Visual Report Builder`」オプションの横にある「**[!UICONTROL Create Report]**」をクリックします。

**指標の追加**

`Report Builder` を開いたので、分析を実行する指標（例：`Revenue` または `Orders`）を追加します。

>[!NOTE]
>
>ネイティブの [!DNL Google Analytics] 指標は `Cohort Report Builder` と互換性がありません。

**指標ビューを`Cohort`** に切り替える

![](../../assets/visual-report-builder-cohort-toggle.png)

これにより、`Cohort` レポートの詳細を設定するための新しいウィンドウが開きます。

### `Cohort` しいレポートを作成するには、次の 5 つの仕様が必要です。

1. `cohorts` のグループ化方法
1. `cohort` の期間
1. 表示する `cohorts` 数
1. 各 `cohort` に含める必要があるデータの最小量
1. `cohort` の発生後の時間範囲

#### 1. グループ化 `cohorts`

`Cohorts` は、**登録日** や **初回注文日** など、タイムスタンプでグループ化されます。

>[!NOTE]
>
>指標が `cohort` 定の日付に対して構築されているのと同じタイムスタンプを使用することはできません。 これを必要とする分析の場合は、代わりに `Standard report builder` を使用できます。

#### （2）期 `Cohort`

グループ化の基準にする期間 `cohorts` 選択します。 つまり、上記で選択したタイムスタンプのうち、最も重要なのは `week`、`month`、`quarter`、`year` のどれですか？ レポートには、ここで選択した間隔でデータが表示されます

#### 3.と 4. 表示する `cohorts` 数と、各 `cohort` ーザーに必要なデータ量を設定します

これらのパラメーターは、関心のある `cohorts` のみを表示するのに役立ち、ウィンドウの下部にある便利な `Preview` ボックスは、レポートに表示されるコホートを正確に示します。

デフォルトでは、各 `cohort` ータに必要な最小限のデータ量を `0` に変更しない限り、現在の `cohort` は含まれません。 この場合、当期の `cohort` には部分的なデータのみが含まれます。

#### 5.`Cohort` 発生後の時間範囲

この機能を使用すると、選択した `cohorts` ータに対して表示するデータの時間範囲を設定できます。 例えば、`customer's first order date` に基づいて 24 か月の `cohorts` を表示したいが、各 `cohort` ータの最初の 3 か月のデータにのみ関心がある場合は、`number of cohorts to view` を `24`、`time range after cohort occurrence` を `3` に設定できます。

この値の間隔は、`cohort time period` で選択した値によって変わり、デフォルトでは値は `12` に設定されています。カレンダーアイコンをクリックして編集しない限り、値は変更されません。

![](../../assets/cohort-time-range.png)

#### その他のメモ

* [!UICONTROL Filters]:`Standard` 表示と `Cohort` 表示を切り替えても、指標に適用されるデータはそのまま維持されます。

* [`Perspectives`](#perspectives) を参照。

#### 例

これをすべて集める例を次に示します。 この例では、`cohort` ーザーの最初の購入後の注文行動を確認して、そのコホートが今後 6 か月以内にリピート購入を行うために戻ってきているかどうかを確認します。

![ 注文コホート ](../../assets/crb_example.gif)

### レガシーアーキテクチャ

#### レガシーアーキテクチャ {#personalinfo}

`Cohort Report Builder` のレガシーバージョンに固有の手順を以下に示します。 新しいバージョンの使用に関心がある場合、新しいアーキテクチャアカウントへの移行について詳しくは [ 新しいアーキテクチャ ](../../administrator/account-management/new-architecture.md) を参照し [!DNL Commerce Intelligence] ください。

#### 独自の `cohort` 分析を作成するにはどうすればよいですか？ {#create}

![](../../assets/create-cohort-analysis.png)

実行中の `Cohort` 分析 ここでは、時間の経過と共に売上高が累積およびユーザー単位で増加していることがわかります。

この節では、独自の `cohort` 分析を作成する手順について説明します。 例（およびプロセスを示すアニメーションGIF）については、このトピックの [ 例セクション ](#examples) を参照してください。

1. 左側のタブの「**[!UICONTROL Report Builder]**」または任意のダッシュボードの「**[!UICONTROL Add Report** > **Create Report]**」をクリックします。

1. `Report Builder Selection` 画面で、「`Cohort Analysis`」オプションの横にある「**[!UICONTROL Create Report]**」をクリックします。

#### 指標の追加

`Cohort Report Builder` を開いたので、分析を実行する指標（例：`Revenue` または `Number of orders`）を追加します。

>[!NOTE]
>
>ネイティブの [!DNL Google Analytics] 指標は `Cohort Report Builder` と互換性がありません。

#### コホート日の選択 {#date}

次の手順では、`cohort date` を指定します。 ユーザーをグループ化する日付です。 例えば、`User's first order date` や `User's registration date` のようになります。

>[!NOTE]
>
>指標を作成した日付（例：`created at`）と同じ日付を `cohort date` として使用することはできません。

#### 間隔と期間の設定

次に、`Interval` と `Time Period` を設定します。

`Interval`
「`Interval`」オプションを使用すると、`cohorts` の `length` を設定できます。 例えば、これを `Month` に設定すると、レポートは月単位で測定されます。

**期間** メニューを使用して、X 軸でのこれらの間隔の表示方法を変更できます。

`Time Period`
`Time Period` メニューを使用して、分析する特定のユーザー `cohorts` を選択します。 すべての `cohort` を表示したり、リストから選択したり、時間範囲を指定したり、含める `cohorts` のローリング時間範囲を定義したりできます。 例えば、「`Specific Cohorts`」オプションを使用した場合、分析に含める特定の月を選択できます。

![`Time Period` メニューを使用した特定の `Cohorts`](../../assets/Cohort_Time_Period.gif) の追加

グループ化する場合は、登録日を基準に `cohorts` 定し、`Specific Cohorts` ータリストで 4 月、5 月、6 月を選択すると、その月に登録したすべてのユーザーが含まれます。

#### X 軸の定義

「`duration`」で、グラフの X 軸設定を定義できます。 つまり、各データ・ポイントが表す期間の数と、分析に含めるデータ・ポイントの数です。

#### `counting members` テーブルの選択

別のテーブルから結合された `cohort date` でユーザーをグループ化することを選択した場合は、`counting members in the … table` のオプションが表示される場合があります。

![](../../assets/Cohort_Counting_Members_option.png)

この設定を理解するには、例を参照してください。 `Customer's registration date` 別の `Revenue` しい指標を示すレポートを作成したとします。 また、パースペクティブ `Average value per cohort member` を使用して、買い手ごとの売上高を経時的に確認する必要がありました。 買い手ごとの平均値を見つけるには、で割る買い手の数を決定する必要があります。 `customers` テーブルに登録されている顧客の数ですか、それとも同じ期間における `orders table` 内の個別の購入者の数ですか。

この設定は、その質問に回答します。 `customers` テーブル内のカウントメンバーには、（これまでに購入を行ったかどうかに関わらず）すべての顧客が平均で含まれます。 `orders` テーブル内のカウントメンバーには、購入を行った顧客のみが含まれます。

#### パースペクティブの選択 {#perspective}

指標と分析方法を定義したら、使用する指標を選択 `perspective` きます。

レポートビジュアライゼーションの真上に、設定のドロップダウン `perspective` あります。

[ パースペクティブ ](#perspectives) を参照してください。

![](../../assets/Cohort_Perspective_Menu.png)

## コホート分析の例 {#examples}

`cohort` しい分析の作成方法を説明したので、いくつかの例を見てみましょう。

### ユーザー `cohorts` が時間の経過と共にどのように成長しているかを知りたい。

![ 時間の経過に伴うユーザー `cohorts` の増加 ](../../assets/cohort1.gif)

この例では、`Revenue` 指標を分析し、コホートを `customer's first order date` 別にグループ化して、分析に含める最新の 8 つの `cohorts` （`Time Period` メニューで定義）を選択しました。 コホートが時間の経過と共にどのように成長するかを確認するには、`Cumulative Average Value per Cohort Member` `perspective` を使用しました。

### ユーザーが生涯の様々な時点で行った注文の平均を把握したいと思います。

 （../../assets/cohort2.gif

この例では、`Number of orders` の指標を分析し、`customer's first order date` 別にコホートをグループ化して、分析に最新の 8 つのコホート（`Time Period` メニューで定義）を含めました。 各コホートの平均注文数を確認するには、`perspective` を `Average Value per Cohort Member` に変更しました。

### ユーザーの今後の購買活動と、ビジネスでの最初の月の活動との比較を理解したいと思います。

![ ユーザーの将来の購買活動と活動の最初の月の比較 ](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
ライフサイクルの特定の時点における特定コホートグループの増分貢献度を示します。 （例：「6 週目」ポイントには、ユーザーが 6 週目に作成したすべてのデータポイントが表示されます）。

`Average Value per Cohort Member`
これにより、（1）の分 `Standard cohort` 分析が各 `cohort` グループのユーザー数で割られます。 すべてのコホートグループに同じ数のユーザーが含まれるとは限らないので、この方法は、各リンゴごとのコホートパフォーマンスを比較するのに役立ちます。 例えば、特定の `cohort` からのユーザーあたり 6 週目の平均売上高です。

`Cumulative`
この `perspective` では、従来の `cohort` 分析を `cumulative` に示します。 つまり、ライフサイクルの特定の時点における、特定のコホートの現在までの貢献度の合計を示します。 例えば、特定のコホートから 6 週間のユーザーが得た後の累積売上高などです。

`Cumulative Average Value per Cohort Member`
これにより、（3）の `Cumulative` 分析が各 `cohort` グループのユーザー数で割られます。 これは、`cohort's` 期の各期間における `cohort` メンバーあたりの平均生涯貢献度（多くの場合、平均生涯売上高）を示します。 例えば、6 月に参加したユーザーが 6 か月後の平均生涯売上高です。

`Percent of First Value (show first value)`
これは、`cohort's` のライフサイクルの特定の時間における貢献度 `cohort` 集計を、最初の期間における貢献度のパーセンテージとして分析します。 例えば、6 か月の売上高を 6 月に参加したユーザーの 1 か月の売上高で割ったとします。

`Percent of First Value (hide first value)`
これは上 `perspective` と同じですが、100% の最初の期間の値が非表示になります。

## まとめ {#finish}

`Cohort Report Builder` は、共通の `cohort date` でユーザーをグループ化するために最適化されています。 類似のアクティビティや属性でユーザーをグループ化したい場合があります。 Adobeでは、開始するには、[ 定性コホートに関するこのチュートリアル ](../dev-reports/create-qual-cohort-analysis.md) を確認することをお勧めします。
