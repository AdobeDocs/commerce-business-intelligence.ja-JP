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
>[ 管理者権限 ](../../administrator/user-management/user-management.md) が必要です。

指標は測定です。 SQL およびデータベース構造では、指標は可変期間にわたるストアド・クエリに似ています。

[!DNL Commerce Intelligence] では、指標を使用して [ グラフを作成 ](../../data-user/reports/ess-rpt-build-visual.md) できます。 例えば、指標 `revenue` は注文の合計数です。 指標 `average customer revenue per order` は、顧客の注文あたりの平均支出です。

レポートで使用する場合は、指定した期間にわたって指標を分析し、様々なカテゴリで [ フィルターまたはセグメント化 ](../../best-practices/segment-filter.md) できます。 性別でグループ化された平均顧客売上高の分析を検討します。この場合、`average customer revenue per order` は指標、性別はグループ化です。

## 指標の定義 {#define}

1. 指標を作成するには、「**[!UICONTROL Data** > **Metrics]**」をクリックします。

1. 「**[!UICONTROL Create New Metric]**」をクリックします。

1. ドロップダウンから、指標に使用するネイティブ列または計算列を含むテーブルをクリックします。

1. 指標に名前を付けます。

   Adobeでは、指標が何であるかを一目で把握できる名前を使用することをお勧めします。 例：`Average Order Revenue`。

1. 次の手順では、指標の動作を定義します。 ドロップダウンメニューを使用して、指標の操作、`operation` の列、`date` のディメンションを定義します。

   * 次のいずれかの操作を選択します。
      * `Count` – この操作は、データテーブルの行数をカウントします
      * `Max` – 最大は、特定のデータ列の最大値を返します
      * `Min` - Min は、特定のデータ列の最小値を返します
      * `Sum` – この操作は、特定のデータ列の値を合計します
      * `Average` – この操作は、データ列値の平均を計算します
      * `Count Distinct Value` – 特定のデータ列の一意の値の数をカウントします
      * `Median` – この操作は、データ列値の中央値を計算します
      * `First and Third Quartiles` – これらの操作は、データ列の値の 25 パーセンタイルと 75 パーセンタイルをそれぞれ計算します
      * `Tenth and Ninetieth Percentiles` – これらの操作は、データ列の値の 10 パーセンタイルと 90 パーセンタイルをそれぞれ計算します

   * 操作を実行する列を選択します。 例えば、合計売上高を見つけたい場合は、`order total` 列に対して合計操作を実行します。

     既存の指標を編集する場合は、この節で [ 指標の作業用テーブルを変更する ](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) こともできます。

   * 指標のトレンドに使用できる日付ディメンションを選択します。 例：`order date`。

## フィルターの追加 {#filters}

`Filter` のセクションでは、フィルターを作成したり、指標に [ 保存済みのフィルターセット ](../../data-user/reports/ess-manage-data-filters.md) を適用したりできます。

`average order revenue` 指標の場合、ストアの設定中に行われた可能性のあるテスト注文を含めることは望ましくありません。これにより、不正確な結果が得られます。 フィルタセットを適用して、データセットからそれらの注文を削除できます。 フィルターを作成すると、この指標を使用して作成されたすべてのグラフに適用されます。

`Filter Logic` の節では、指標の動作をさらに定義できます。

* 「\[`A`\] または\[`B`\]」は、フィルター\[`A`\] または\[`B`\] を満たすデータを許可します
* 「\[`A`\] および\[`B`\]」では、フィルター\[`A`\] と\[`B`\] の両方を満たすデータのみが許可されます
* 「（\[`A`\] と\[`B`\]） OR \[`C`\]」は、両方のフィルター\[`A`\] と\[`B`\] を満たす、またはフィルター\[`C`\] のみを満たすデータのみを許可します

## ディメンションの追加 {#dimensions}

[`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) のセクションには、フィルタリングまたはグループ化に使用できるすべてのデータディメンションが表示されます。デフォルトでは、使用可能なすべてのデータ列がディメンションとして一覧表示されます。 例を続けると、リファラルソースで売上高をセグメント化する場合は、ここで実行できます。

使用可能なすべてのデータ列をディメンションとしてリストする以外に、[!DNL Commerce Intelligence] では、グループ化できる列を推測します。 *レポート上のデータをセグメント化またはグループ化するには*、列をグループ化可能としてマークする必要があります。

## 仕上げ {#finish}

指標の動作を定義する方法に加えて、`User Rights` のセクションで権限レベルを設定することもできます。 ユーザー `Admin` すべての指標にアクセスできますが、適切なグループの横にあるボックスをオンにして、この指標を使用できるユーザーを指定する必要があります。

既存の指標を編集する場合は、「`Dependent Charts`」セクションで、この指標を使用するグラフ（およびその所有者）のリストを表示できます。

変更内容は自動的に保存され、指標は問題なく動作します。
