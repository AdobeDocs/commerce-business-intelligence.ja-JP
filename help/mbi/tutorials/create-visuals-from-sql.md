---
title: SQL クエリからのビジュアライゼーションの作成
description: SQLReport Builderで使用される用語を理解し、SQL ビジュアライゼーションを作成するための基盤を確立する方法を説明します。
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# SQL クエリからのビジュアライゼーションの作成

このチュートリアルの目的は、 `SQL Report Builder` を作成するための確固たる基盤を提供します。 `SQL visualizations`.

この [`SQL Report Builder`](../data-analyst/dev-reports/sql-rpt-bldr.md) は、次のオプションを含む Report Builder です。クエリは、データのテーブルを取得する目的でのみ実行できます。また、その結果をレポートに変換することもできます。 このチュートリアルでは、SQL クエリからビジュアライゼーションを作成する方法を説明します。

## 用語

このチュートリアルを開始する前に、 `SQL Report Builder`.

- `Series`:測定する列は、SQLReport Builderでは「系列」と呼ばれます。 一般的な例は次のとおりです。 `revenue`, `items sold`、および `marketing spend`. 1 つ以上の列を `Series` をクリックして、ビジュアライゼーションを作成します。

- `Category`:データのセグメント化に使用する列は、 `Category` これは、 `Group By` の機能 [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md). 例えば、顧客の全期間売上高を獲得ソース別にセグメント化する場合、獲得ソースを含む列は `Category`. 複数の列を `Category`.

>[!NOTE]
>
>日付とタイムスタンプは `Categories`. これらはクエリ内のデータの別の列であり、クエリ自体で必要に応じて書式設定および並べ替える必要があります。

- `Labels`:これらは X 軸のラベルとして適用されます。 経時的にデータトレンドを分析する場合、年と月の列をラベルとして指定します。 複数の列をラベルに設定できます。

## 手順 1:クエリを記述

次の点に注意してください。

- この `SQL Report Builder` uses [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- 時系列を含むレポートを作成する場合は、必ず `ORDER BY` タイムスタンプ列。 これにより、タイムスタンプがレポート上で適切な順序でプロットされます。

- この `EXTRACT` 関数は、タイムスタンプの日、週、月または年を解析するために使用するのに最適です。 これは、 `time interval` レポートに使用するのは、 `daily`, `weekly`, `monthly`または `yearly`.

利用を開始するには、 `SQL Report Builder` クリックして **[!UICONTROL Report Builder** > **SQL Report Builder]**.

例として、各製品の販売品目の月別合計数を返すクエリを考えてみましょう。

```sql
    SELECT SUM("qty") AS "Items Sold", "products's name" AS "product name",
    EXTRACT(year from "Order date") AS "year",
    EXTRACT(month from "Order date") AS "month"
    FROM "items"
    WHERE "products's name" LIKE '%Jeans'
    GROUP BY  "products's name", "year","month"
    ORDER BY "year" ASC,"month" ASC
    LIMIT 3500
```

このクエリは、次の結果のテーブルを返します。

![](../assets/SQL_results_table.png)

## 手順 2:ビジュアライゼーションの作成

この結果では、 *ビジュアライゼーションを作成する方法を教えてください。* 開始するには、 **[!UICONTROL Chart]** 」タブをクリックします。 `Results` ウィンドウ これにより、 `Chart settings` タブをクリックします。

クエリを最初に実行したとき、クエリ内のすべての列が一連としてプロットされるので、レポートは不可確に見える場合があります。

![](../assets/SQL_initial_report_results.png)

この例では、経時的なトレンドを示す折れ線グラフを使用します。 作成するには、次の設定を使用します。

- `Series`:を選択します。 `Items sold` 列を `Series` 測定したいので 次に `Series` 列には、レポートに 1 行がプロットされます。

- `Category`:この例では、各製品を別々の行としてレポートに表示します。 これをおこなうには、 `Product name` を `Category`.

- `Labels`:列を使用 `year` および `month` x 軸のラベルとして表示 `Items Sold` 経時的にトレンドを示す

>[!NOTE]
>
>クエリには `ORDER BY` ラベルの条件 `date`/`time` 列。

次に、クエリの実行からレポートの設定に至るまで、このビジュアライゼーションの作成方法を簡単に示します。

![](../assets/SQL_report_settings.gif)

## 手順 3:を選択します。 `Chart Type`

この例では、 `Line` グラフのタイプ。 別の `chart type`をクリックし、グラフオプションセクションの上にあるアイコンをクリックして変更します。

![](../assets/Chart_types.png)

## 手順 4:ビジュアライゼーションの保存

このレポートを再度使用する場合は、レポートに名前を付け、 **[!UICONTROL Save]** をクリックします。

ドロップダウンで、 `Chart` を `Type` 次に、レポートの保存先のダッシュボードを開きます。

## おめでとうございます。 完了しました。

もう少し踏み込みたい？ 以下を確認します。 [クエリ最適化のベストプラクティス](../best-practices/optimizing-your-sql-queries.md).
