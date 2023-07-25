---
title: データベースと SQL エディタの間の結果の理解
description: データベースと SQL エディターの間の結果を理解する方法を説明します。
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# データベース結果と [!DNL SQL Editor] 結果

ご興味をお持ちの方は、 `Last successful update began` フィールドが `Integrations` ページ：

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## について `timestamp` フィールド

開始が表示されます `timestamp` （アカウントに設定されたタイムゾーンで） _最終更新サイクル_ お使いのアカウントで。

- 前回の更新サイクルで問題が発生した同期テーブルがある場合、このタイムスタンプは *更新されていません*.
- したがって、新しいデータでレポートが更新され、 *前回成功した更新が開始されました* まだ遅れが続いています。

## 最後の「実際の」データポイントを特定する

特定の統合に関する最新のデータポイントは、 `Last Data Point Received` 各統合の右側にあるタイムスタンプ。 このタイムスタンプは、Data Warehouseがデータベース、API、サードパーティ統合のいずれの場合でも、そのソースからデータポイントを正常に受け取った最後のポイントを示します。

からのデータの鮮度を確認するには *特定のテーブル*&#x200B;を使用する場合、Adobeはクイックを作成することをお勧めします [[!DNL SQL] レポート](../../dev-reports/sql-rpt-bldr.md) が `MAX(timestamp)` アカウントで最も重要な表で このタイムスタンプと `Last Data Point` 問題がアカウント全体に影響を与えたか、テーブルのサブセットに影響を与えたかを示します。 Adobeでは、一般的に使用される 3 ～ 4 つの重要なテーブルに対してこの操作をお勧めします。

- この `MAX(timestamp)` の値が `Last Data Point Received`つまり、テーブルのサブセットは影響を受けましたが、アカウント全体の更新サイクルは安定しています。
- この `MAX(timestamp)` 値が次の値と等しいかそれ以前 `Last Data Point Received`の場合は、アカウントの更新サイクルが影響を受けたことを意味します。 この状況では、 [サポートチケットを提出する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
