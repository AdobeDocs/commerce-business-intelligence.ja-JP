---
title: SQL とData Warehouse・マネージャの違い
description: SQL とData Warehouse・マネージャの違いを説明します。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# SQL とData Warehouse・マネージャの違い

列には、 [SQLReport Builder](../dev-reports/sql-rpt-bldr.md) また、 [Data Warehouse管理](../data-warehouse-mgr/creating-calculated-columns.md). 1 つは更新サイクルへの依存性で、もう 1 つはアカウントでの列の保存方法です。

## 列 `SQL Report Builder`

列は更新サイクルに依存しないので、列で繰り返し処理を行う前に、列が完了するのを待つ必要がなくなりました。 誤りを犯した場合、修正には数回のキー操作しかかかりません。2 回の更新が終わるのを待たずに、作業に戻ることができます。

>[!IMPORTANT]
>
>SQL エディタを使用して作成した列は、Data Warehouseに保存されません。 常にその列を含むクエリにアクセスできますが、その列を複数のレポートで使用する場合は、各レポートのクエリでその列を再作成する必要があります。 つまり、SQL エディターを使用して作成した列は、従来の `Report Builder`.

## Data Warehouseマネージャの列

列は更新サイクルに依存するので、編集する前に完全なサイクルを完了する必要があります。 これらの列はData Warehouseマネージャに保存され、従来の `Report Builder` または `SQL Report Builder`.
