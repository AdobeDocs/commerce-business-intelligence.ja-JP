---
title: SQL クエリからのビジュアライゼーションの作成
description: SQL Report Builderで使用されている用語を理解し、SQL ビジュアライゼーションを作成するための堅牢な基盤を提供します。
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
role: Admin, Data Architect, Data Engineer, Leader, User
feature: SQL Report Builder, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# SQL クエリからのビジュアライゼーションの作成

このチュートリアルの目的は、[!DNL SQL Report Builder] で使用されている用語を理解し、`SQL visualizations` を作成するための強固な基盤を提供することです。

[[!DNL SQL Report Builder]](../data-analyst/dev-reports/sql-rpt-bldr.md) は、オプションを備えた Report Builder です。データのテーブルを取得することのみを目的としてクエリを実行したり、その結果をレポートに変換したりできます。 このチュートリアルでは、SQL クエリからビジュアライゼーションを作成する方法について説明します。

## 用語

このチュートリアルを開始する前に、`SQL Report Builder` で使用されている次の用語を参照してください。

- `Series`：測定する列は、SQL Report Builderでは系列と呼ばれます。 一般的な例には、`revenue`、`items sold`、`marketing spend` があります。 ビジュアライゼーションを作成するには、少なくとも 1 つの列が `Series` として設定されている必要があります。

- `Category`：データのセグメント化に使用する列は `Category` と呼ばれます。これは、`Group By` の [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md) 機能と似ています。 例えば、顧客の生涯売上高を獲得ソースでセグメント化する場合、獲得ソースを含む列は `Category` として指定されます。 複数の列を `Category` として設定できます。

>[!NOTE]
>
>日付とタイムスタンプは `Categories` として使用することもできます。 これらは、クエリ内の別のデータ列にすぎず、クエリ自体で必要に応じて書式設定および並べ替える必要があります。

- `Labels`：これらは X 軸ラベルとして適用されます。 時間の経過に伴うデータのトレンドを分析する場合、年と月の列はラベルとして指定されます。 複数の列をラベルに設定できます。

## 手順 1：クエリを記述する

次の点に注意してください。

- [!DNL SQL Report Builder] は [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html) を使用します。

- 時系列を含むレポートを作成する場合は、必ずタイムスタンプ列を `ORDER BY` します。 これにより、タイムスタンプがレポートに正しい順序でプロットされます。

- `EXTRACT` 関数は、タイムスタンプの日、週、月、年を解析するために使用するのに最適です。 これは、レポートで使用する `time interval` が `daily`、`weekly`、`monthly` または `yearly` の場合に便利です。

開始するには、「開 [!DNL SQL Report Builder]」をクリックして **[!UICONTROL Report Builder** > **SQL Report Builder]** を開きます。

例えば、各製品で販売された項目の月別の合計数を返す次のクエリについて考えてみます。

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

このクエリは、次の結果テーブルを返します。

![ 製品、年、月ごとに販売されたアイテムを含む SQL クエリ結果を示すテーブル ](../assets/SQL_results_table.png)

## 手順 2：ビジュアライゼーションの作成

これらの結果から、*ビジュアライゼーションはどのように作成されますか？* 開始するには、**[!UICONTROL Chart]** ウィンドウの [`Results`] タブをクリックします。 「`Chart settings`」タブが表示されます。

クエリを初めて実行すると、クエリ内のすべての列が系列としてプロットされるので、レポートが不可解に見える場合があります。

![ すべての列を系列としてプロットした初期 SQL レポート ](../assets/SQL_initial_report_results.png)

この例では、経時的なトレンドを示す折れ線グラフにする必要があります。 作成するには、次の設定を使用します。

- `Series`:`Items sold` 列を測定するため、`Series` として選択します。 `Series` 列を定義すると、レポートに 1 行がプロットされます。

- `Category`：この例では、各製品を異なる明細としてレポートに表示します。 それには、`Product name` を `Category` として設定します。

- `Labels`：列 `year` および `month` を X 軸のラベルとして使用し、`Items Sold` を経時的なトレンドとして表示できるようにします。

>[!NOTE]
>
>`ORDER BY`/`date` 列の場合、クエリにはラベルに `time` 句を含める必要があります。

クエリの実行からレポートの設定に至るまで、このビジュアライゼーションがどのように作成されたかを以下に示します。

![SQL レポートビジュアライゼーション設定の設定に関するアニメーションのデモ ](../assets/SQL_report_settings.gif)

## 手順 3:`Chart Type` ールの選択

次の使用例では、`Line` グラフの種類を使用します。 別の `chart type` を使用するには、[ グラフ オプション ] セクションの上にあるアイコンをクリックして変更します。

![ 折れ線グラフ、棒グラフ、面グラフ、その他のビジュアライゼーションオプションなど、使用可能なグラフタイプのアイコン ](../assets/Chart_types.png)

## 手順 4：ビジュアライゼーションを保存

このレポートを再度使用する場合は、レポートに名前を付け、右上隅の「**[!UICONTROL Save]**」をクリックします。

ドロップダウンで、`Chart` として「`Type`」を選択し、レポートの保存先のダッシュボードを選択します。

## まとめ

もう一歩進んでみませんか？ [ クエリの最適化のベストプラクティス ](../best-practices/optimizing-your-sql-queries.md) を確認してください。
