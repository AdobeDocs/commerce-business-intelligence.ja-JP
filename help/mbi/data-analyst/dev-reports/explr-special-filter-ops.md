---
title: 特別なフィルター演算子
description: レポートの作成時や指標の作成時に、フィルターで使用される特別な演算子について説明します。
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# フィルターオプション

このトピックでは、いくつかの特別な内容を紹介します `operators` 使用される `filters` when [レポートの作成](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} または [指標の作成](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;}。

## `Filter Operators`

* `LIKE` パターンマッチング用。 ワイルドカード文字%（可変数の文字を含むワイルドカードの場合）または_（ワイルドカードの単一文字の場合）と共に使用する必要があります。  例えば、制限 `LIKE \_ake%` は true を返します。 `Jake Stein`, `Jake Smith`または `Fake Smith`.  次の場合は false を返します。 `Drake Smith`.

* `NOT LIKE` は上記のパターンマッチングに似ていますが、どのパターンが一致しないかを確認します。

* `IS` 列が `NULL`、または空。

* `IS NOT` は、 `IS` 演算子を使用しますが、NULL 以外の列をチェックします。

* `IN` 値の存在をコンマ区切りリストで確認します。 ( 例： 「色」 `IN` 「red,orange」は色と同じです。 `equal to` 赤または色 `equal to` オレンジ色 )。

* `NOT IN` 次に類似 `IN` を超える値が存在しないかをチェックします。
