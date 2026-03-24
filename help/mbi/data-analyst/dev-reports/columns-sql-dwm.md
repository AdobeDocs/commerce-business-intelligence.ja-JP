---
title: SQLとData Warehouse Managerの相違点
description: SQLとData Warehouse Managerの違いについて説明します。
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
TQID: https://experienceleague.adobe.com/aWLLAi9e-A6Di7AGujRNd79W7GqSRo5yIgmQRZAHOEQ
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 210
ht-degree: 0%

---

# [!DNL SQL]と[!DNL Data Warehouse Manager]の相違点

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md)で作成された列と[[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md)を使用して作成された列には、主に2つの違いがあります。 1つは更新サイクルへの依存で、もう1つはアカウント内での列の保存方法です。

## [!DNL SQL Report Builder]の列

列は更新サイクルに依存しないため、列を繰り返し実行する前に、更新サイクルが完了するのを待つ必要がなくなります。 ミスをした場合、修正するのに数回のキーボード操作が必要なため、2回のアップデートが終了するのを待つことなく、作業を再開できます。

>[!IMPORTANT]
>
>[!DNL SQL] エディターを使用して作成した列は、Data Warehouseに保存されません。 列を含むクエリには常にアクセスできますが、複数のレポートで列を使用する場合は、各レポートのクエリで列を再作成する必要があります。 つまり、[!DNL SQL] エディターを使用して作成された列は、従来の[!DNL Report Builder]では使用できません。

## Data Warehouse Managerの列

列は更新サイクルに依存するため、完全なサイクルは編集する前に完了する必要があります。 これらの列はData Warehouse Managerに保存され、従来の[!DNL Report Builder]または[!DNL SQL Report Builder]で使用できます。
