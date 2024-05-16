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

指標は測定です。 SQL およびデータベース構造では、指標は可変期間にわたるストアド・クエリに似ています。

対象： [!DNL Commerce Intelligence]指標を使用すると、次のことができます [グラフの作成](../../data-user/reports/ess-rpt-build-visual.md). 例えば、指標です `revenue` は、注文の合計数です。 指標 `average customer revenue per order` は、顧客が注文ごとに費やす平均金額です。

レポートで使用する場合は、指定した期間にわたって指標を分析でき、 [フィルタリングまたはセグメント化](../../best-practices/segment-filter.md) カテゴリー別。 男女別にグループ化された平均顧客売上高の分析を検討します。この場合は、 `average customer revenue per order` は指標、性別はグループ化です。

## 指標の定義 {#define}

1. 指標を作成するには、をクリックします **[!UICONTROL Data** > **Metrics]**.

1. クリック **[!UICONTROL Create New Metric]**.

1. ドロップダウンから、指標に使用するネイティブ列または計算列を含むテーブルをクリックします。

1. 指標に名前を付けます。

   Adobeでは、指標を一目で把握できる名前を推奨しています。 例： `Average Order Revenue`.

1. 次の手順では、指標の動作を定義します。 ドロップダウンメニューを使用して、指標の操作（ `operation` 列および `date` ディメンション :

   * 次のいずれかの操作を選択します。
      * `Count`  – この操作は、データテーブルの行数をカウントします
      * `Max`  – 最大は、特定のデータ列の最大値を返します
      * `Min`  – 最小：特定のデータ列の最小値を返します
      * `Sum`  – この操作は、特定のデータ列の値を合計します
      * `Average`  – この操作は、データ列の値の平均を計算します
      * `Count Distinct Value`  – 特定のデータ列の一意の値の数をカウントします
      * `Median`  – この操作は、データ列値の中央値を計算します
      * `First and Third Quartiles`  – これらの操作は、データ列の値の 25 パーセンタイルと 75 パーセンタイルをそれぞれ計算します
      * `Tenth and Ninetieth Percentiles`  – これらの操作は、データ列の値の 10 パーセンタイルと 90 パーセンタイルをそれぞれ計算します

   * 操作を実行する列を選択します。 例えば、総売上高を求める場合は、次のフィールドに対して合計操作を実行します `order total` 列。

     既存の指標を編集する場合は、次のこともできます [指標の操作テーブルの変更](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) この節を参照してください。

   * 指標のトレンドに使用できる日付ディメンションを選択します。 例： `order date`.

## フィルターの追加 {#filters}

この `Filter` 「」セクションでは、フィルターを作成または適用できます [保存済みフィルターセット](../../data-user/reports/ess-manage-data-filters.md) を指標に追加します。

の場合 `average order revenue` 指標として、ストアの設定中に行われた可能性のあるテスト注文を含めないでください。含めると、不正確な結果が得られます。 フィルタセットを適用して、データセットからそれらの注文を削除できます。 フィルターを作成すると、この指標を使用して作成されたすべてのグラフに適用されます。

この `Filter Logic` セクションでは、指標の動作をさらに定義できます。

* ``\[`A`\] または\[`B`\]&#39;&#39; フィルタ \[[`A`\] または\[`B`\]
* ``\[`A`\] と\[`B`\]&#39;&#39;では、両方のフィルター\[`A`\] と\[`B`\]
* &quot;（\[`A`\] と\[`B`\]）または\[`C`\]&#39;&#39;では、両方のフィルター\[`A`\] と\[`B`\]、または filter \[`C`\] 単独

## Dimensionの追加 {#dimensions}

この [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 「」セクションには、フィルタリングまたはグループ化に使用できるすべてのデータディメンションが表示されます。デフォルトでは、使用可能なすべてのデータ列がディメンションとして一覧表示されます。 例を続けると、リファラルソースで売上高をセグメント化する場合は、ここで実行できます。

使用可能なすべてのデータ列をディメンションとしてリストする以外に、 [!DNL Commerce Intelligence] グループ化できる列を推測します。 *レポートでデータをセグメント化またはグループ化するには*、列はグループ化可能としてマークする必要があります。

## 仕上げ {#finish}

指標の動作を定義する以外に、で権限レベルを設定することもできます `User Rights` セクション。 While `Admin` ユーザーはすべての指標にアクセスできます。適切なグループの横にあるボックスをオンにして、この指標を使用できるユーザーを指定する必要があります。

既存の指標を編集している場合、この指標を使用しているグラフ（およびグラフを所有しているユーザー）のリストを `Dependent Charts` セクション。

変更内容は自動的に保存され、指標は問題なく動作します。
