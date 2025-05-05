---
title: データベースと SQL エディター間の結果について
description: データベースと SQL エディターの間の結果を理解する方法を説明します。
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# データベースの結果と [!DNL SQL Editor] の結果

`Integrations` ページ内の `Last successful update began` フィールドが何かを知りたいかもしれません。

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## `timestamp` フィールドについて

アカウントの _最後の成功した更新サイクル）の開始 `timestamp` （アカウントで設定されたタイムゾーン_ が表示されます。

- 同期されたテーブルで最後の更新サイクル中に問題が発生した場合、このタイムスタンプは *更新されていません*。
- したがって、レポートが新しいデータで更新されたにもかかわらず、*最後に成功した更新が開始された* が、まだ遅れている場合があります。

## 最後の「実際」のデータポイントを特定

特定の統合の最新のデータポイントは、各統合の右側にある `Last Data Point Received` タイムスタンプによって決定されます。 このタイムスタンプは、データベース、API、サードパーティの統合のいずれであっても、Data Warehouseがそのソースからデータポイントを正常に受信した最後のポイントを指します。

*特定のテーブル* からのデータの鮮度を確認するために、Adobeでは、アカウント上の最も重要なテーブルに対して `MAX(timestamp)` を実行するクイック [[!DNL SQL]  レポート ](../../dev-reports/sql-rpt-bldr.md) を作成することをお勧めします。 このタイムスタンプを `Last Data Point` と比較すると、問題がアカウント全体に影響を与えたか、テーブルのサブセットに影響を与えたかが示されます。 Adobeでは、一般的に使用される 3～4 つの重要なテーブルに対してこれを行うことをお勧めします。

- `MAX(timestamp)` の値が `Last Data Point Received` より新しい場合は、テーブルのサブセットが影響を受けましたが、アカウント全体の更新サイクルは安定しています。
- `MAX(timestamp)` の値が `Last Data Point Received` 以前の場合は、アカウントの更新サイクルが影響を受けていることを意味します。 この場合は、[ サポートチケットを送信 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja) します。
