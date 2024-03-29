---
title: 指標の作成
description: 指標を使用してグラフを作成する方法を説明します。
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# 指標の作成

>[!NOTE]
>
>が必要 [管理者権限](../../administrator/user-management/user-management.md).

指標は測定値です。 SQL およびデータベース構造では、指標は、変数期間にわたって保存されたクエリのようなものです。

In [!DNL Commerce Intelligence]を使用する場合、指標を [グラフを作成](../../data-user/reports/ess-rpt-build-visual.md). 例えば、指標 `revenue` は、注文の合計数です。 指標 `average customer revenue per order` は、顧客が注文あたりに費やす平均値です。

レポートで使用すると、指標を指定した期間にわたって分析でき、 [フィルター済みまたはセグメント化済み](../../best-practices/segment-filter.md) 異なるカテゴリ別。 性別でグループ化した平均顧客売上高の分析を検討します。この場合、 `average customer revenue per order` は指標で、性別はグループ化です。

## 指標の定義 {#define}

1. 指標を作成するには、 **[!UICONTROL Data** > **Metrics]**.

1. クリック **[!UICONTROL Create New Metric]**.

1. ドロップダウンで、指標に使用するネイティブ列または計算列を含むテーブルをクリックします。

1. 指標に名前を付けます。

   Adobeでは、指標が何であるかを示す名前が推奨されます。 例： `Average Order Revenue`.

1. 次の手順では、指標の動作を定義します。 ドロップダウンメニューを使用して、指標の操作を定義します。 `operation` 列、および `date` ディメンション：

   * 次の操作を選択します。
      * `Count`  — この操作は、データテーブルの行数をカウントします
      * `Max` - Max は、特定のデータ列の最大値を戻します
      * `Min`  — 最小は、特定のデータ列の最小値を戻します
      * `Sum`  — この操作は、特定のデータ列の値を合計します
      * `Average`  — この操作は、データ列の値の平均を計算します
      * `Count Distinct Value`  — 特定のデータ列の一意の値をカウントします
      * `Median`  — この操作は、データ列の値の中央値を計算します
      * `First and Third Quartiles`  — これらの演算は、それぞれデータ列の値の第 25 パーセンタイル値と第 75 パーセンタイル値を計算します
      * `Tenth and Ninetieth Percentiles`  — これらの演算は、それぞれデータ列の値の第 10 パーセンタイルと第 90 パーセンタイルを計算します

   * 操作を実行する列を選択します。 例えば、合計売上高を見つけたい場合、 `order total` 列。

     既存の指標を編集している場合は、 [指標の運用可能テーブルを変更する](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) （この節を参照）。

   * 指標のトレンド表示に使用できる日付ディメンションを選択します。 例： `order date`.

## フィルターの追加 {#filters}

The `Filter` 「 」セクションでは、フィルターの作成や適用をおこなうことができます。 [保存済みフィルターセット](../../data-user/reports/ess-manage-data-filters.md) を指標に追加します。

の `average order revenue` 」指標を使用する場合、ストアの設定中に行われた可能性のあるテスト注文を含めたくない場合があります。これにより、不正確な結果が得られます。 フィルターセットを適用して、これらの注文をデータセットから削除できます。 フィルターを作成すると、この指標を使用して作成されたすべてのグラフに適用されます。

The `Filter Logic` セクションでは、指標の動作をさらに詳しく定義できます。

* &quot;\[`A`\] または\[`B`「\]」では、フィルター「\[」を満たすすべてのデータを許可します`A`\] または\[`B`\]
* &quot;\[`A`\] と\[`B`\]」では、両方のフィルター\[`A`\] と\[`B`\]
* &quot;(\[`A`\] と\[`B`\]) または\[`C`\]」では、両方のフィルタ\[`A`\] と\[`B`\]、またはフィルタ\[ を満たしています`C`\] 単独

## 追加Dimension {#dimensions}

The [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 「 」セクションには、フィルタリングまたはグループ化に使用可能なすべてのデータディメンションが表示されます。デフォルトでは、使用可能なすべてのデータ列がディメンションとして表示されます。 この例では、紹介元別に売上高をセグメント化する場合は、ここでそれを実行できます。

使用可能なすべてのデータ列をディメンションとして表示する以外に、 [!DNL Commerce Intelligence] 列がグループ化可能な場所です。 *レポートでデータをセグメント化またはグループ化するには*、列はグループ化可能としてマークする必要があります。

## 終了中 {#finish}

指標の動作の定義に加えて、 `User Rights` 」セクションに入力します。 While `Admin` ユーザーはすべての指標にアクセスできます。この指標を使用できるユーザーは、該当するグループの横にあるボックスをオンにして指定する必要があります。

既存の指標を編集している場合は、 `Dependent Charts` 」セクションに入力します。

変更は自動的に保存され、指標は正常に保存されました。
