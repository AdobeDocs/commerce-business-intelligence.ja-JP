---
title: ビジュアルReport Builderの使用
description: 特定の期間に関するレポートのデータを分析する方法を説明します。
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# の使用 [!DNL Visual Report Builder]

この [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) を使用すると、データを視覚的に調べてインサイトを引き出し、ビジネス上の意思決定を促進できます。 このチュートリアルでは、基本的なレポートを作成するプロセスについて説明します。

>[!NOTE]
>
>ダッシュボードにレポートを追加するには、次が必要です `Standard` [ユーザー権限](../administrator/user-management/user-management.md) および `Edit` ダッシュボードにアクセスします。

## 手順 1：レポートの作成

レポートの作成を開始するには、 **[!UICONTROL Report Builder]** サイドバー上、または **[!UICONTROL Add Report]** ダッシュボードの上部 いつ `Report Builder` ページが表示されたら、 **[!UICONTROL Visual Report Builder]** オプション。

で作成したレポートを編集するには [!DNL Visual Report Builder]で、グラフの右上隅にある歯車（オプション）アイコンをクリックし、 **[!UICONTROL Edit]**.

## 手順 2：指標の追加

分析を作成するための最初の手順は、次の項目を選択することです。 [指標](../data-user/reports/ess-manage-data-metrics.md) を分析します。 デフォルトでは指標はアルファベット順に表示されますが、指標を強化するテーブルでグループ化することもできます。

最初の指標を選択した後に追加の指標を追加し、すべての指標を 1 つのレポートにオーバーレイしたり、式を追加して複数指標の計算を実行したりできます。

## 手順 3：追加 `Formulas`

`Formulas` をクリックすることでレポートに追加されます。 **[!UICONTROL Add Formula]**&#x200B;レポート内の指標リストのすぐ上にあります。 が含まれる [式エディター](../data-analyst/dev-reports/formulas-in-rpt-bldr.md)を設定する場合は、レポートに含まれる任意の指標を入力として使用できます。 様々な指標を操作するために、基本的な数学演算子が使用されます。

例えば、注文あたりの平均売上高を示すレポートを作成するとします。 この場合、を除算します `Revenue` による指標 `Number of orders` 指標。

![](../assets/ave-rev-per-order.png)

## 手順 4：の設定 `Time Period` および `Interval of Analysis` {#time}

特定の期間にゼロを設定するには、分析の期間を設定します。 また、データをセグメント化する時間間隔（年別、四半期別、月別など）を選択することもできます。 グラフの右上隅にあるメニューを使用して、期間と間隔を設定します。

![](../assets/Time_Options_Report_Builder.png)

期間の特定の日付範囲を設定する場合は、開始日が間隔の先頭にあり、終了日が間隔の末尾にあることを確認します。

例えば、から期間を設定します `January 1st` 対象： `March 1st` を選択し、 `monthly` 間隔の表示 `March` をデータポイントとして使用するが、では毎日無視される `March` 例外 `March 1`. その場合は、を作成する必要があります `Time Period` から `January 1 to March 31`.

## 手順 5: `Group by` / `Segmenting the Analysis` {#groupby}

[データディメンションで指標をセグメント化するには](../best-practices/segment-filter.md)を選択し、 **[!UICONTROL Group by]** グラフの左上にあるメニュー。 これにより、リストに含まれる最初の指標で使用可能なすべてのディメンションを含むドロップダウンが表示されます。

以下から選択できます `None` 指標がセグメント化されるのを防ぐ。 例えば、別の売上高指標を地域でセグメント化しながら、セグメント化せずに合計売上高を返す指標を使用したい場合があります。

注文あたりの平均売上高の例に戻り、グループ化の基準をプロモーションコードに設定します。 これにより、プロモーションコードの有無にかかわらず、注文あたりの平均売上高が表示されます。

![](../assets/Group_By_Report_Builder.png)

分析に含まれる指標が異なるデータテーブルに基づいて作成されている場合、ポップアップを使用して、各テーブルで一致するデータディメンションを選択できます。 ここでの目標は、セグメント化の値のタイプを共有するディメンションを見つけることです。

![](../assets/Dimension_Editor.png)

## 手順 6：設定 `Metric Filters`, `Perspective`、および `Time Interval` {#metric-specific}

分析に追加された各指標に対して、フィルターを追加し、関連するデータ観点を選択して、次の項目を設定できます `time interval` オプション。 これらの機能にアクセスするには、ファネル （`Filter`），目（`Perspective`）、および時計（`Time`）アイコンが表示されます。これは、レポートに含まれる指標の横にあります。

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` 分析に含まれるデータセットを制限します。 フィルターは、例えば、個々の獲得チャネルを評価し、異常値を削除する場合に役立ちます。

ドロップダウンメニューとテキストボックスの他に、次のような特別なフィルター演算子も使用できます `LIKE` または `IN` でフィルターを作成します。

ワイルドカードの使用（`%` または `_`）に設定します `LIKE` ステートメントがサポートされています。 この `%` ワイルドカードは複数の文字に一致しますが、 `_` 任意の 1 文字にのみ一致します。 例：

- `affiliate's name Like B%` で始まる名前の顧客からのデータのみを許可 `B`.

- `affiliate's name Like _ake` という名前の顧客からのデータのみを許可します `Jake`, `Rake`、または `Bake` ただし、そうではありません `Drake` または `Blake`.

複数のフィルターを追加すると、グラフのデータを厳密に制御できます。 デフォルトでは、データを組み込むにはすべてのフィルター条件が true である必要がありますが、「フィルタールール」テキストボックスを編集して OR 関係を作成できます。

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` では、データの様々なビューを簡単に切り替えることができます。 利用可能な情報を見る：

- `Standard perspective`：標準パースペクティブは、一致する日付の結果を X 軸に表示します（例：1 月の売上高）。 これは、注文あたりの平均売上高の例で使用するパースペクティブです。

![](../assets/Standard.png)

- `Amount` または `Percent Change` 対 `Previous Period` パースペクティブ：このパースペクティブは、ある間隔から次の間隔への変化量または変化率を示し、急速に変化する指標の変化率を測定するのに役立ちます。 また、前年の同じ期間との間隔を比較して、前年比の成長を示す視点もあります。

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`：です `cumulative perspective` 一定期間の指標の進行中または累積の合計金額を表示します。 これは、多くの場合、顧客全体を分析し、将来の処理能力を計画するために使用されます。

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`：このパースペクティブは、分析に含まれる初回の間隔のパーセンテージとしてデータを表示します。 これは、第 1 期間のパフォーマンスに対する特定のアクションの有効性を測定する際に役立ちます。

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`：ローリング平均ウィンドウのパースペクティブは、指定された時間範囲での指標のローリング平均値を表示します。 間隔は、レポートレベルで設定された間隔と同じである必要があります。 例えば、レポートで収益の最後の四半期が週別に表示されている場合は、ローリング平均期間の範囲を 4 週間に設定できます。 これにより、最初の 3 つの値が null になり、4 番目の値は売上高の最初の 4 週間の平均を表します。 わかりやすくするために、必ずチェックボックスをオフにします。 `Multiple Y-Axes` 下図の例のように、ローリング平均で同じ指標を表示している場合は、「」チェックボックスをオンにします。

![](../assets/rolling_avg_window.png)

### 指標固有の時間オプション

レポートで使用するメトリックには、2 つのオプションがあります。グローバル時間オプションに従って時間の経過とともにトレンドを表示できる場合と、表示されない場合があります。

指標の時間間隔の変更 `None` を返します `scalar` 数値。時間トレンド指標をで除算する式を作成する場合に役立ちます。 `scalar` 数値。 また、 `scalar` レポートの時間範囲とは独立した時間範囲を指す指標。

例えば、2019 年の月次売上高を 2019 年全体の売上高のパーセンテージで表示するとします。 2 つ追加できます `Revenue` グローバルな時間範囲が 2019 年 1 月 1 日～2019 年 12 月 31 日のレポートの指標を月単位の間隔でセグメント化したもの。

>[!NOTE]
>
>を追加する場合 `group by` ディメンション。新しいビジュアライゼーションを選択するか、時間間隔を調整してから数値（`scalar`）に設定します。 これらの調整は、次回ダッシュボードからそのレポートを開いたときに保持されるのではなく、時間範囲のみが保持されます。

レポートでの時間オプションの使用について詳しくは、こちらを参照してください [チュートリアル](../tutorials/time-options-visual-rpt-bldr.md).

## 手順 7：レポートの保存

作成したグラフは、以下をクリックして保存できます。 **[!UICONTROL Save]** の右上隅に `Visual Report Builder`.

グラフ、テーブル、または数値（`scalar`）を使用する `Type` ドロップダウンと、レポートの保存先となるダッシュボード（ `Location` ドロップダウン。

次に、以下をクリックしてレポートを保存できます **[!UICONTROL Save to Dashboard]**.

![](../assets/save-to-dashboard.png)

## レポート出力

選択するレポート出力を決定するには、次のトピックを参照してください。

### グラフ

![](../assets/RB_Chart.png)

### テーブル

![](../assets/RB_Table.png)

### 数値（`scalar`）

![](../assets/RB_Scalar.png)

おめでとうございます。完了しました。
