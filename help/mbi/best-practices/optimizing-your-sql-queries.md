---
title: SQL クエリの最適化
description: SQL クエリを最適化する方法を説明します。
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# SQL クエリの最適化

この [!DNL SQL Report Builder] を使用すると、任意の時点でこれらのクエリをクエリし、繰り返し実行できます。 これは、更新が必要な列やレポートを確認する前に、更新サイクルが完了するのを待たずにクエリを変更する必要がある場合に役立ちます。

クエリを実行する前に、 [[!DNL Commerce Intelligence] 費用を見積もる](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/sql-queries-explain-cost-errors.html). コストでは、クエリの実行に必要な時間とリソースの数が考慮されます。 そのコストが高すぎると見なされた場合、または返される行の数が [!DNL Commerce Intelligence] 制限を満たさない場合、クエリは失敗します。 のクエリ [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md)を使用すると、可能な限り効率的なクエリを記述できます。Adobeでは、次の操作をお勧めします。

## SELECT またはすべての列の選択の使用

すべての列を選択しても、タイムリーで簡単に実行できるクエリに対して実行されません。 使用するクエリ `SELECT *` は、特にテーブルに多数の列がある場合に、の実行にかなりの時間がかかる場合があります。

このため、Adobeでは `SELECT *` 可能な限り、必要な列のみを含めます。

| **この代わりに…** | **やってみて！** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style="table-layout:auto"}

## 完全外部結合の使用

外部結合では、結合する両方のテーブル全体を選択するので、クエリの計算コストが増加します。 つまり、クエリの実行に時間がかかり、失敗する可能性が高くなります。結果を返すのに実行制限より長くかかる場合があるからです。

このタイプの結合を使用する代わりに、内部または左側の結合を使用することを検討してください。 内部結合は、テーブル間で列が一致する場合 ( 例えば、 `order_id` 標準の `customers` および `orders` 表 )。 左結合は、左（最初）のテーブルからのすべての結果と、右（2 番目）のテーブルでの一致結果を返します。

FULL OUTER JOIN クエリを書き換える方法を見てみましょう。

| **この代わりに…** | **やってみて！** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style="table-layout:auto"}

これらのクエリは、使用する JOIN のタイプを除いて、あらゆる点で同一です。

## 複数の結合の使用

クエリに複数の結合を含めることができますが、クエリのコストが上がる可能性があることに注意してください。 コストしきい値に達しないように、Adobeでは、可能な限り複数の結合を避けることをお勧めします。

## フィルターの使用

可能な限り、フィルターを使用します。 `WHERE` および `HAVING` 句で結果を絞り込み、実際に必要なデータのみを提供します。

## JOIN 句でのフィルタの使用

結合を実行する際にフィルタを使用する場合は、必ず結合内の両方のテーブルに適用してください。 重複している場合でも、クエリの計算コストが削減され、実行時間が短縮されます。

| **この代わりに…** | **やってみて！** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style="table-layout:auto"}

## 演算子の使用

クエリを記述する際は、可能な限り「低コスト」の演算子を使用することを検討してください。 各クエリには計算コストがかかり、クエリを構成する関数、演算子、フィルターによって決まります。 一部の演算子は、必要な計算作業が少なく、他の演算子よりもコストが低くなります。

比較演算子（>、&lt;、=など）は最もコストが低く、その後に [例： と POSIX 演算子に類似](https://www.postgresql.org/docs/9.5/functions-matching.html) これは最も高価な演算子です。

## EXISTS と IN の使用

使用 `EXISTS` 対比 `IN` 返す結果のタイプに応じて異なります。 1 つの値のみを使用する場合は、 `EXISTS` 代わりに節を使う `IN`. `IN` は、コンマ区切り値のリストと共に使用され、クエリの計算コストが増加します。

条件 `IN` クエリを実行する場合、まずサブクエリ ( `IN` ステートメント ) を使用し、 `IN` 文。 `EXISTS` は、クエリを複数回実行する必要がないので、はるかに効率的です。クエリで指定した関係を確認する際に、true または false 値が返されます。

簡単に言うと、使用時にシステムが処理する必要はありません `EXISTS`.

| **この代わりに…** | **やってみて！** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style="table-layout:auto"}

## 並べ替え順の使用

`ORDER BY` は SQL の高価な関数で、クエリのコストを大幅に引き上げることができます。 クエリの EXPLAIN コストが高すぎるというエラーメッセージが表示された場合は、 `ORDER BY`をクエリから削除する必要があります（必要な場合）。

とは言えません。 `ORDER BY` は使用できません。必要な場合にのみ使用する必要があります。

## GROUP BY と ORDER BY の使用

この方法が、実行しようとしている操作に従わない場合もあります。 一般的なルールは、 `GROUP BY` および `ORDER BY`の場合、両方の句の列を同じ順序に配置する必要があります。 例：

| **この代わりに…** | **やってみて！** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style="table-layout:auto"}

## 折り返し

SQL の書き方を学ぶ最も良い方法は、試行錯誤を通じてです。 最適なレポートを見つけるには、SQL エディターのみを使用していくつかのレポートを再作成してみてください。
