---
title: 特殊フィルター演算子
description: レポートの作成時または指標の作成時にフィルターで使用される特殊演算子について説明します。
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# フィルターオプション

このトピックでは、いくつかの特別な機能について説明します `operators` 使用されている `filters` 条件 [レポートの作成](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} または [指標の作成](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;}。

## `Filter Operators`

* `LIKE` （パターンマッチング用）。 これは、ワイルドカード文字 % （可変文字数のワイルドカードの場合）または_ （ワイルドカードの 1 文字の場合）と共に使用する必要があります。  例えば、次のような制限があります `LIKE \_ake%` は true を返します `Jake Stein`, `Jake Smith`、または `Fake Smith`.  の場合は false が返されます `Drake Smith`.

* `NOT LIKE` は上記のパターンマッチングに似ていますが、どのパターンが一致しないかを確認します。

* `IS` 列がであるかどうかを確認します `NULL`、または空です。

* `IS NOT` 次に類似しています `IS` null 以外の列をチェックする上記の演算子。

* `IN` コンマ区切りリストで値の存在をチェックします。 （例：「カラー」 `IN` 赤、オレンジ」は色に相当します `equal to` 赤または色 `equal to` オレンジ）。

* `NOT IN` 次に類似している `IN` 上記の値が、値の欠落をチェックします。
