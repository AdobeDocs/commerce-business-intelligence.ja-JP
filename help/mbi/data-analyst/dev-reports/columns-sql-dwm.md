---
title: SQL とData Warehouse Manager の違い
description: SQL とData Warehouse Manager の違いについて説明します。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# [!DNL SQL] と [!DNL Data Warehouse Manager] の違い

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) で作成された列と [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md) を使用して作成された列には、大きな違いが 2 つあります。 1 つは更新サイクルへの依存で、もう 1 つはアカウントへの列の保存方法です。

## [!DNL SQL Report Builder] の列

列は更新サイクルに依存しないので、列を繰り返し処理する前に列が完了するのを待つ必要はありません。 誤った場合は、修正に数回のキーストロークしかかかりません。作業に戻る前に 2 つの更新が完了するのを待つ必要はもうありません。

>[!IMPORTANT]
>
>[!DNL SQL] エディターを使用して作成した列は、Data Warehouseに保存されません。 列を含むクエリには常にアクセスできますが、複数のレポートで列を使用する場合は、各レポートのクエリで列を再作成する必要があります。 つまり、[!DNL SQL] エディターを使用して作成された列は、従来の [!DNL Report Builder] では使用できません。

## Data Warehouse Manager の列

列は更新サイクルに依存するので、編集する前に完全なサイクルを完了する必要があります。 これらの列はData Warehouse Manager に保存され、従来の [!DNL Report Builder] や [!DNL SQL Report Builder] で使用できます。
