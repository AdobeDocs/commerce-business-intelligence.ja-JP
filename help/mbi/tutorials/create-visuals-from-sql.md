---
title: SQL クエリからのビジュアライゼーションの作成
description: SQL Report Builderで使用される用語を理解し、SQL ビジュアライゼーションを作成するための堅牢な基盤を提供します。
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
role: Admin, Data Architect, Data Engineer, Leader, User
feature: SQL Report Builder, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# SQL クエリからのビジュアライゼーションの作成

このチュートリアルの目的は、で使用されている用語を理解することです [!DNL SQL Report Builder] 作成するための強固な基盤を提供します `SQL visualizations`.

この [[!DNL SQL Report Builder]](../data-analyst/dev-reports/sql-rpt-bldr.md) は、オプションを備えた report builder です。データのテーブルを取得することのみを目的としてクエリを実行することも、その結果をレポートに変換することもできます。 このチュートリアルでは、SQL クエリからビジュアライゼーションを作成する方法について説明します。

## 用語

このチュートリアルを開始する前に、で使用されている次の用語を参照してください `SQL Report Builder`.

- `Series`：測定する列は、SQL Report Builderでは系列と呼ばれます。 一般的な例を以下に示します `revenue`, `items sold`、および `marketing spend`. 少なくとも 1 つの列がとして設定されている必要があります `Series` でビジュアライゼーションを作成します。

- `Category`：データのセグメント化に使用する列はです `Category` これはまさにのようなものです `Group By` の機能 [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md). 例えば、顧客の生涯売上高を獲得ソースでセグメント化する場合、獲得ソースを含む列はのように指定します `Category`. 複数の列をとして設定できます `Category`.

>[!NOTE]
>
>日付とタイムスタンプは、次としても使用できます `Categories`. これらは、クエリ内の別のデータ列にすぎず、クエリ自体で必要に応じて書式設定および並べ替える必要があります。

- `Labels`：これらは X 軸ラベルとして適用されます。 時間の経過に伴うデータのトレンドを分析する場合、年と月の列はラベルとして指定されます。 複数の列をラベルに設定できます。

## 手順 1：クエリを記述する

次の点に注意してください。

- この [!DNL SQL Report Builder] 使用 [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- 時系列を含むレポートを作成する場合は、次の点に注意してください `ORDER BY` タイムスタンプ列。 これにより、タイムスタンプがレポートに正しい順序でプロットされます。

- この `EXTRACT` 関数は、タイムスタンプの日、週、月、年の解析に使用するのに最適です。 次の場合に役立ちます `time interval` レポートで使用したいのは次のとおりです `daily`, `weekly`, `monthly`、または `yearly`.

開始するには、を開きます [!DNL SQL Report Builder] クリックして **[!UICONTROL Report Builder** > **SQL Report Builder]**.

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

![](../assets/SQL_results_table.png)

## 手順 2：ビジュアライゼーションの作成

この結果では、 *ビジュアライゼーションの作成方法* 開始するには、 **[!UICONTROL Chart]** タブ `Results` ペイン。 次が表示されます `Chart settings` タブ。

クエリを初めて実行すると、クエリ内のすべての列が系列としてプロットされるので、レポートが不可解に見える場合があります。

![](../assets/SQL_initial_report_results.png)

この例では、経時的なトレンドを示す折れ線グラフにする必要があります。 作成するには、次の設定を使用します。

- `Series`：を選択します `Items sold` 列 `Series` あなたはそれを測定したいので。 を定義した後 `Series` 列に、レポートにプロットされた 1 行が表示されます。

- `Category`：この例では、各製品を異なる行としてレポートに表示します。 それには、を設定します `Product name` as the `Category`.

- `Labels`：列を使用します `year` および `month` x 軸のラベルとして表示可能 `Items Sold` 経時的なトレンドと同様。

>[!NOTE]
>
>クエリには、を含める必要があります。 `ORDER BY` ラベルが次の場合、ラベルの句 `date`/`time` 列。

クエリの実行からレポートの設定に至るまで、このビジュアライゼーションがどのように作成されたかを以下に示します。

![](../assets/SQL_report_settings.gif)

## 手順 3：を選択 `Chart Type`

この例では、を使用します `Line` グラフタイプ。 別のを使用するには `chart type`を変更するには、「グラフオプション」セクションの上にあるアイコンをクリックします。

![](../assets/Chart_types.png)

## 手順 4：ビジュアライゼーションを保存

このレポートを再度使用する場合は、レポートに名前を付けて、 **[!UICONTROL Save]** 右上隅

ドロップダウンで「」を選択します。 `Chart` as the `Type` 次に、レポートの保存先のダッシュボードを選択します。

## まとめ

もう一歩進んでみませんか？ を確認してください。 [クエリの最適化のベストプラクティス](../best-practices/optimizing-your-sql-queries.md).
