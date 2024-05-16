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

# データベース結果と [!DNL SQL Editor] 結果

あなたは何が興味があるかもしれない `Last successful update began` フィールドが内にある `Integrations` ページ：

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## について `timestamp` フィールド

それはスタートを示しています `timestamp` （アカウントに設定されたタイムゾーンで） _前回成功した更新サイクル_ あなたのアカウント上。

- 同期されたテーブルで最後の更新サイクル中に問題が発生した場合、このタイムスタンプは *更新はありません*.
- したがって、レポートが新しいデータで更新された場合もありますが、 *前回成功した更新の開始* まだ遅れている。

## 最後の「実際」のデータポイントを特定

特定の統合の最新のデータポイントは、 `Last Data Point Received` 各統合の右側にあるタイムスタンプ。 このタイムスタンプは、データベース、API、サードパーティの統合のいずれであっても、Data Warehouseがそのソースからデータポイントを正常に受信した最後のポイントを指します。

からのデータの鮮度をチェックするには *特定のテーブル*、Adobeでは、クイック作成をお勧めします [[!DNL SQL] 報告書](../../dev-reports/sql-rpt-bldr.md) を実行します `MAX(timestamp)` あなたのアカウント上で最も重要なテーブルに。 このタイムスタンプとの比較 `Last Data Point` 問題がアカウント全体に影響を与えたか、テーブルのサブセットに影響を与えたかを示します。 Adobeでは、一般的に使用される 3～4 つの重要なテーブルに対してこれを行うことをお勧めします。

- 次の場合 `MAX(timestamp)` 値はより新しい `Last Data Point Received`つまり、テーブルのサブセットは影響を受けましたが、アカウント全体の更新サイクルは安定しています。
- 次の場合 `MAX(timestamp)` 値が次と等しいか、以前 `Last Data Point Received`、アカウントの更新サイクルが影響を受けていることを意味します。 この場合、 [サポートチケットを送信](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
