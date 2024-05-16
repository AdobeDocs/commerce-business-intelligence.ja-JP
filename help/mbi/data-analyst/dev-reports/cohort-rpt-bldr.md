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

時間の経過と共にユーザーの様々なサブセットがどのように動作するかを研究したいと思ったことはありますか？ 例えば、プロモ期間中に登録したユーザーの平均生涯売上高が、そうでないユーザーの平均生涯売上高よりも高いかどうか疑問に思ったことはありませんか。 次のような場合 `Yes`を選択し、続いて `Cohort Report Builder` は、お客様に最適なツールです。 [!DNL Adobe Commerce Intelligence] は、この分析を実行し、ビジネスに関連させるために最適化されています。

## コホート分析とは {#what}

`Cohort` 分析は、ライフサイクルを通じて類似した特性を共有するユーザーグループの分析として広く定義できます。 これにより、様々なユーザーグループにわたる行動のトレンドを特定できます。

に関する詳細な基礎知識 `cohort` 分析、レビュー [このページ](https://www.cohortanalysis.com/).

あなたの [!DNL Commerce Intelligence] ダッシュボード、ユーザーの作成が簡単 `cohorts` に基づく `cohort` アカウントの日付および指標。

## コホート分析はなぜ重要なのでしょうか？ {#important}

前述のとおり、 `cohort` analysis を使用すると、様々なユーザーグループ間の行動のトレンドを特定できます。 特定のグループの行動をしっかりと理解することで、決定と支出を調整して売上を最大化できます。 例えば、生涯売上高を取り込みます `cohort` 分析 – この種の分析は多くの理由で有益ですが、当面のものは顧客獲得に関する意思決定が優れています。

## 独自に作成する方法 `cohort` 分析？

### 新しいアーキテクチャ

を使用する手順は次のとおりです `Cohort Report Builder` 日 [新しいアーキテクチャ](../../administrator/account-management/new-architecture.md).

1. クリック **[!UICONTROL Report Builder]** 左側のタブまたは **[!UICONTROL Add Report** > **Create Report]** を任意のダッシュボードに表示します。

1. が含まれる `Report Builder` 選択画面、クリック **[!UICONTROL Create Report]** 「」の横 `Visual Report Builder` オプション。

**指標の追加**

現在は、 `Report Builder`で、分析を実行する指標（例： `Revenue` または `Orders`）に設定します。

>[!NOTE]
>
>ネイティブ [!DNL Google Analytics] 指標は、と互換性がありません `Cohort Report Builder`.

**指標ビューをに切り替えます。`Cohort`**

![](../../assets/visual-report-builder-cohort-toggle.png)

新しいウィンドウが開き、の詳細が設定されます `Cohort` レポート。

### を構築するには 5 つの仕様が必要です。 `Cohort` レポート :

1. のグループ化方法 `cohorts`
1. この `cohort` 期間
1. 次の数 `cohorts` 表示対象
1. 各データの最小量 `cohort` 次を含める必要があります
1. 後の時間範囲 `cohort` 発生件数

#### 1. グループ化 `cohorts`

`Cohorts` 次のようにタイムスタンプでグループ化されます。 **登録日** または **初回注文日**.

>[!NOTE]
>
>指標が用に構築されているのと同じタイムスタンプを使用することはできません `cohort` 日付。 これを必要とする分析の場合、を使用できます `Standard report builder` その代わり。

#### 2. `Cohort` 期間

グループ化する期間を選択 `cohorts` による。 つまり、上記で選択したタイムスタンプの一部が最も重要です。 `week`, `month`, `quarter`、または `year`? レポートには、ここで選択した間隔でデータが表示されます

#### 3.と 4. 次の数を設定 `cohorts` 各データを表示して量を確認するには `cohort` に要件があります

これらのパラメーターは、 `cohorts` あなたが興味を持っていること、そして便利 `Preview` ウィンドウ下部のボックスには、レポートに表示されるコホートが正確に表示されます。

デフォルトでは、 `cohort` それぞれに必要な最小量のデータを変更しない限り、は含まれません `cohort` 対象： `0`. この場合、 `cohort` 当期のデータには、部分的なデータのみが含まれます。

#### 5.後の時間範囲 `Cohort` 発生件数

この機能を使用すると、選択したのデータを表示する時間範囲を設定できます `cohorts`. 例えば、24 か月ごとに表示したい場合 `cohorts` 基準： `customer's first order date`ただし、関心があるのは、それぞれのデータの最初の 3 か月間のみです `cohort`を設定できます `number of cohorts to view` 対象： `24` および `time range after cohort occurrence` 対象： `3`.

この値の間隔は、 `cohort time period` 値はに設定されます。 `12` デフォルトでは、カレンダーアイコンをクリックして編集しない限り、値は変更されません。

![](../../assets/cohort-time-range.png)

#### その他のメモ

* [!UICONTROL Filters]：切り替えても、指標に適用されるデータは変わりません `Standard` および `Cohort` ビュー。

* 参照： [`Perspectives`](#perspectives).

#### 例

これをすべて集める例を次に示します。 この例では、注文の後の動作を確認します。 `cohort`の最初の購入は、今後 6 か月以内にコホートがリピート購入を行うために戻ってきているかどうかを確認するためのものです。

![注文コホート](../../assets/crb_example.gif)

### レガシーアーキテクチャ

#### レガシーアーキテクチャ {#personalinfo}

のレガシーバージョンに固有の手順は次のとおりです `Cohort Report Builder`. 新しいバージョンを使用する場合は、を参照してください [新しいアーキテクチャ](../../administrator/account-management/new-architecture.md) への移行の詳細 [!DNL Commerce Intelligence] 新しいアーキテクチャアカウント

#### 独自に作成する方法 `cohort` 分析？ {#create}

![](../../assets/create-cohort-analysis.png)

`Cohort` 実行中の分析 ここでは、時間の経過と共に売上高が累積およびユーザー単位で増加していることがわかります。

この節では、独自のテンプレートを作成する手順について説明します `cohort` 分析。 例（およびプロセスを示すアニメーションGIF）については、 [例セクション](#examples) （このトピック）。

1. クリック **[!UICONTROL Report Builder]** 左側のタブまたは **[!UICONTROL Add Report** > **Create Report]** を任意のダッシュボードに表示します。

1. が含まれる `Report Builder Selection` 画面、クリック **[!UICONTROL Create Report]** 「」の横 `Cohort Analysis` オプション。

#### 指標の追加

現在は、 `Cohort Report Builder`指標を追加します（例： `Revenue` または `Number of orders`）に入力します。

>[!NOTE]
>
>ネイティブ [!DNL Google Analytics] 指標は、と互換性がありません `Cohort Report Builder`.

#### コホート日の選択 {#date}

次の手順では、を指定します。 `cohort date`. ユーザーをグループ化する日付です。 例えば、次のようになります `User's first order date` または `User's registration date`.

>[!NOTE]
>
>指標と同じ日付を使用することはできません（例： `created at`）に設定する `cohort date`.

#### 間隔と期間の設定

次に、 `Interval` および `Time Period`.

`Interval`
この `Interval` オプションを使用すると、 `length` の `cohorts`. 例えば、が次のように設定されているとします `Month`の場合、レポートは月単位で測定されます。

これらの間隔を X 軸に表示する方法は、 **期間** メニュー。

`Time Period`
の使用 `Time Period` 特定のユーザーを選択するためのメニュー `cohorts` を分析します。 次を表示できます `cohort`、リストから選択、時間範囲を指定、または周期的な時間範囲を定義します `cohorts` を含めます。 例えば、 `Specific Cohorts` オプションとして、分析に含める特定の月を選択できます。

![使用， `Time Period` 特定のを追加するメニュー `Cohorts`](../../assets/Cohort_Time_Period.gif)

グループ化を行う場合 `cohorts` 登録日別およびその後で 4 月、5 月、6 月を `Specific Cohorts` このリストには、その月に登録したすべてのユーザーが含まれます。

#### X 軸の定義

次の下 `duration`グラフの X 軸の設定を定義できます。 つまり、各データ・ポイントが表す期間の数と、分析に含めるデータ・ポイントの数です。

#### の選択 `counting members` テーブル

でユーザーをグループ化することを選択した場合 `cohort date` が別のテーブルから結合されている場合は、 `counting members in the … table` オプション。

![](../../assets/Cohort_Counting_Members_option.png)

この設定を理解するには、例を参照してください。 を含むレポートを作成したとします `Revenue` 指標の基準 `Customer's registration date`. また、パースペクティブを使用する必要がありました `Average value per cohort member` バイヤーごとの収益を経時的に確認します。 買い手ごとの平均値を見つけるには、で割る買い手の数を決定する必要があります。 登録済みの顧客数 `customers` テーブルに含まれるか、またはユーザー内のユニーク購入者数です `orders table` 同じ期間？

この設定は、その質問に回答します。 内のメンバーのカウント `customers` 表には、すべての顧客（購入を行ったかどうかに関わらず）を平均で含めます。 内のメンバーのカウント `orders` テーブルには、購入を行った顧客のみが含まれます。

#### パースペクティブの選択 {#perspective}

指標と分析方法を定義したら、 `perspective` を使用する。

レポートビジュアライゼーションのすぐ上に、のドロップダウンがあります `perspective` 設定。

参照： [視点](#perspectives).

![](../../assets/Cohort_Perspective_Menu.png)

## コホート分析の例 {#examples}

では、を作成する方法を説明しました `cohort` 分析、いくつかの例を見てください。

### ユーザーの状況を知りたい `cohorts` は時間と共に成長しています。

![ユーザー `cohorts` 時間の経過と共に成長する](../../assets/cohort1.gif)

この例では、を分析しました `Revenue` 指標、コホートをでグループ化 `customer's first order date`、および最新 8 件の選択 `cohorts` （で定義） `Time Period` メニュー）を選択して、解析に含めます。 コホートが時間の経過と共にどのように成長するかを確認するには、を使用しました `Cumulative Average Value per Cohort Member` `perspective`.

### ユーザーが生涯の様々な時点で行った注文の平均を把握したいと思います。

（../../assets/cohort2.gif

この例では、を分析しました `Number of orders` 指標、コホートをでグループ化 `customer's first order date`に定義され、最新の 8 つのコホート（ `Time Period` メニュー）に表示されます。 各コホートの平均注文数を確認するには、 `perspective` 対象： `Average Value per Cohort Member`.

### ユーザーの今後の購買活動と、ビジネスでの最初の月の活動との比較を理解したいと思います。

![ユーザーの将来の購買活動と活動の最初の月の比較](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
ライフサイクルの特定の時点における特定コホートグループの増分貢献度を示します。 （例：「6 週目」ポイントには、ユーザーが 6 週目に作成したすべてのデータポイントが表示されます）。

`Average Value per Cohort Member`
これにより、 `Standard cohort` （1）の各ユーザー数による分析 `cohort` グループ。 すべてのコホートグループに同じ数のユーザーが含まれるとは限らないので、この方法は、各リンゴごとのコホートパフォーマンスを比較するのに役立ちます。 例えば、特定のユーザーからのユーザーあたり 6 週目の平均売上高です `cohort`.

`Cumulative`
この `perspective` 従来のを表示 `cohort` に関する分析 `cumulative` 基準 つまり、ライフサイクルの特定の時点における、特定のコホートの現在までの貢献度の合計を示します。 例えば、特定のコホートから 6 週間のユーザーが得た後の累積売上高などです。

`Cumulative Average Value per Cohort Member`
これにより、 `Cumulative` （3）の各ユーザー数による分析 `cohort` グループ。 1 人当たりの平均生涯貢献度（多くの場合、平均生涯売上高）が表示されます `cohort` の各期間のメンバー `cohort's` 人生。 例えば、6 月に参加したユーザーが 6 か月後の平均生涯売上高です。

`Percent of First Value (show first value)`
これにより、集計が分析されます `cohort` における特定の時間の貢献度 `cohort's` ライフサイクル （最初の期間における貢献度のパーセンテージ）。 例えば、6 か月の売上高を 6 月に参加したユーザーの 1 か月の売上高で割ったとします。

`Percent of First Value (hide first value)`
これは `perspective` 上記の例外として、最初の期間の値 100% は非表示になっています。

## まとめ {#finish}

この `Cohort Report Builder` は、共通の基準でユーザーをグループ化するために最適化されています `cohort date`. 類似のアクティビティや属性でユーザーをグループ化したい場合があります。 Adobeでは、チェックアウトをお勧めします [このチュートリアルでは、質的なコホートについて説明します](../dev-reports/create-qual-cohort-analysis.md) をクリックして開始します。
