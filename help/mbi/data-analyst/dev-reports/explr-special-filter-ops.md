---
title: 特殊フィルター演算子
description: レポートの作成時または指標の作成時にフィルターで使用される特殊演算子について説明します。
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# フィルターオプション

このトピックでは、`operators` レポートの作成 `filters` または [&#x200B; 指標の作成 &#x200B;](../../tutorials/using-visual-report-builder.md){: target="_blank"} の [&#x200B; に使用される特殊な &#x200B;](../../data-user/reports/ess-manage-data-metrics.md){: target="_blank"} を説明します。

## `Filter Operators`

* パターンマッチングの `LIKE`。 これは、ワイルドカード文字 % （可変文字数のワイルドカードの場合）または_ （ワイルドカードの 1 文字の場合）と共に使用する必要があります。  例えば、制限 `LIKE \_ake%` は、`Jake Stein`、`Jake Smith`、`Fake Smith` に対して true を返します。  `Drake Smith` の場合は false を返します。

* `NOT LIKE` は上記のパターンマッチングに似ていますが、どのパターンが一致しないかをチェックします。

* `IS` は、列が `NULL` であるか、空であるかをチェックします。

* `IS NOT` は上記の `IS` 演算子に似ていますが、NULL 以外の列をチェックします。

* `IN` 値の存在をコンマ区切りリストでチェックします。 （例えば、「赤 `IN` 色」、オレンジは赤の色、またはオレンジ `equal to` 色 `equal to` 同等です）。

* `NOT IN` は上記の `IN` に似ていますが、値が存在しないかどうかを確認します。
