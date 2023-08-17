---
title: SQL とData Warehouse・マネージャの違い
description: SQL とData Warehouse・マネージャの違いを説明します。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# 次の間の違い [!DNL SQL] および [!DNL Data Warehouse Manager]

次の 2 つの主な違いがあります： [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) また、 [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). 1 つは更新サイクルへの依存性で、もう 1 つはアカウントでの列の保存方法です。

## 列の [!DNL SQL Report Builder]

列は更新サイクルに依存しないので、列で繰り返し処理を行う前に、列が完了するのを待つ必要がなくなりました。 誤りを犯した場合、修正には数回のキー操作しかかかりません。2 回の更新が終わるのを待たずに、作業に戻ることができます。

>[!IMPORTANT]
>
>を使用して作成した列 [!DNL SQL] エディターはData Warehouseに保存されません。 常にその列を含むクエリにアクセスできますが、その列を複数のレポートで使用する場合は、各レポートのクエリでその列を再作成する必要があります。 つまり、 [!DNL SQL] エディターは、従来の [!DNL Report Builder].

## Data Warehouseマネージャの列

列は更新サイクルに依存するので、編集する前に完全なサイクルを完了する必要があります。 これらの列はData Warehouseマネージャに保存され、従来の [!DNL Report Builder] または [!DNL SQL Report Builder].
