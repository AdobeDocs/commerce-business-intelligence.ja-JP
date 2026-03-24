---
title: 指標の作成
description: 指標を使用してチャートを作成する方法を説明します。
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xPbHndhmDdKugylEyPC3yXwMQHHF7FdMvJI7ZNDk-Yo
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 612
ht-degree: 0%

---

# 指標の作成

>[!NOTE]
>
>[管理者権限](../../administrator/user-management/user-management.md)が必要です。

指標は測定です。 SQL構造とデータベース構造では、指標は変数期間にわたるストアド・クエリに似ています。

[!DNL Commerce Intelligence]では、指標を使用して[ グラフを作成](../../data-user/reports/ess-rpt-build-visual.md)できます。 例えば、指標`revenue`は注文の合計数です。 指標`average customer revenue per order`は、平均的な顧客が注文に費やした金額です。

レポートで使用する場合、指標は指定された期間にわたって分析され、異なるカテゴリによって[ フィルタリングまたはセグメント化](../../best-practices/segment-filter.md)されます。 性別でグループ化された平均顧客売上の分析を検討してください。この場合、`average customer revenue per order`が指標で、性別がグループ化されます。

## 指標の定義 {#define}

1. 指標を作成するには、**[!UICONTROL Data** > **Metrics]**&#x200B;をクリックします。

1. **[!UICONTROL Create New Metric]**&#x200B;をクリックします。

1. ドロップダウンから、指標に使用するネイティブ列または計算列を含むテーブルをクリックします。

1. 指標に名前を付けます。

   Adobeでは、指標が何であるかを示す名前を一目で確認できます。 例：`Average Order Revenue`。

1. 次のステップは、指標の機能を定義することです。 ドロップダウンメニューを使用して、指標の操作、`operation`列、`date` ディメンションを定義します。

   * 操作を選択：
      * `Count` – この操作では、データ テーブルの行数をカウントします
      * `Max` – 最大は、特定のデータ列の最大値を返します
      * `Min` – 最小は、特定のデータ列の最小値を返します
      * `Sum` – この操作は、特定のデータ列の値を合計します
      * `Average` – この操作は、データ列の値の平均を計算します
      * `Count Distinct Value` – 特定のデータ列の一意の値の数をカウントします
      * `Median` – この操作は、データ列の値の中央値を計算します
      * `First and Third Quartiles` – これらの操作では、データ列の値の25番目と75番目のパーセンタイルがそれぞれ計算されます
      * `Tenth and Ninetieth Percentiles` – これらの操作では、データ列の値の10番目と90番目のパーセンタイルがそれぞれ計算されます

   * 操作を実行する列を選択します。 例えば、総収益を求める場合は、`order total`列に対して総計演算を実行します。

     既存の指標を編集する場合は、このセクションで指標の操作テーブル [を](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md)変更することもできます。

   * 指標のトレンド分析に使用できる日付ディメンションを選択します。 例：`order date`。

## フィルターの追加 {#filters}

`Filter` セクションでは、フィルターを作成するか、[保存されたフィルターセット ](../../data-user/reports/ess-manage-data-filters.md)を指標に適用できます。

`average order revenue`指標の場合、ストアの設定中に行われた可能性のあるテスト注文を含めたくありません。これにより、不正確な結果が得られます。 フィルターセットを適用して、これらの注文をデータセットから削除できます。 フィルターを作成すると、この指標を使用して作成されたすべてのチャートに適用されます。

`Filter Logic` セクションでは、指標の動作をさらに定義できます。

* 「\[`A`\]または\[`B`\]」を使用すると、フィルター\[`A`\]または\[`B`\]を満たすデータを使用できます
* 「\[`A`\]および\[`B`\]」は、\[`A`\]と\[`B`\]の両方のフィルターを満たすデータのみを許可します
* 「（\[`A`\]と\[`B`\]）または\[`C`\]」は、\[`A`\]と\[`B`\]の両方を満たすデータまたはフィルター\[`C`\]のみを満たすデータのみを許可します

## ディメンションの追加 {#dimensions}

[`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) セクションには、フィルタリングまたはグループ化に使用できるすべてのデータディメンションが表示されます。デフォルトでは、使用可能なすべてのデータ列がディメンションとして一覧表示されます。 引き続き例として、収益を参照元でセグメンテーションする場合は、ここで行うことができます。

利用可能なすべてのデータ列をディメンションとして一覧表示することに加えて、[!DNL Commerce Intelligence]は、どの列がグループ化できるかを推測します。 *レポート*&#x200B;のデータをセグメント化またはグループ化するには、列をグループ化可能としてマークする必要があります。

## 仕上げ {#finish}

指標の動作を定義するだけでなく、`User Rights` セクションで権限レベルを設定することもできます。 `Admin` ユーザーはすべての指標にアクセスできますが、この指標を使用できるユーザーを示すには、適切なグループの横にあるボックスをオンにする必要があります。

既存の指標を編集する場合は、`Dependent Charts` セクションでこの指標を使用するグラフのリスト （およびそれらを所有するユーザー）を表示できます。

変更は自動的に保存され、指標はスムーズに実行できるようになりました。
