---
title: SQL とData Warehouse・マネージャの違い
description: SQL とData Warehouseマネージャーの違いについて説明します。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# の違い [!DNL SQL] および [!DNL Data Warehouse Manager]

で作成された列には、主な違いが 2 つあります。 [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) およびを使用して作成された [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). 1 つは更新サイクルへの依存で、もう 1 つはアカウントへの列の保存方法です。

## の列 [!DNL SQL Report Builder]

列は更新サイクルに依存しないので、列を繰り返し処理する前に列が完了するのを待つ必要はありません。 誤った場合は、修正に数回のキーストロークしかかかりません。作業に戻る前に 2 つの更新が完了するのを待つ必要はもうありません。

>[!IMPORTANT]
>
>を使用して作成する列 [!DNL SQL] エディターがData Warehouseに保存されていません。 列を含むクエリには常にアクセスできますが、複数のレポートで列を使用する場合は、各レポートのクエリで列を再作成する必要があります。 これは、を使用して作成された列を意味します [!DNL SQL] 従来のではエディターを使用できません [!DNL Report Builder].

## Data Warehouseマネージャーの列

列は更新サイクルに依存するので、編集する前に完全なサイクルを完了する必要があります。 これらの列はData Warehouseマネージャーに保存され、従来のに使用できます [!DNL Report Builder] または [!DNL SQL Report Builder].
