---
title: データベースと SQL エディタの間の結果の理解
description: データベースと SQL エディターの間の結果を理解する方法を説明します。
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# データベース結果と `SQL Editor` 結果

ご興味をお持ちの方は、 `Last successful update began` フィールドが `Integrations` ページ：

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## について `timestamp` フィールド

開始が表示されます `timestamp` （アカウントに設定されたタイムゾーンで） _最終更新サイクル_ お使いのアカウントで。

- 前回の更新サイクルで問題が発生した同期テーブルがある場合、このタイムスタンプは *更新されていません*.
- したがって、新しいデータでレポートが更新され、 *前回成功した更新が開始されました* まだ遅れが続いています。

## 最後の「実際の」データポイントを特定する

特定の統合に関する最新のデータポイントは、 `Last Data Point Received` `timestamp` は、各統合の右側にあります。 このタイムスタンプは、データベース、API、サードパーティ統合のいずれの場合でも、データウェアハウスがそのソースからデータポイントを正常に受け取った最後のポイントを表します。

からのデータの鮮度を確認するには *特定のテーブル*&#x200B;クイック [SQL レポート](../../dev-reports/sql-rpt-bldr.md) が `MAX(timestamp)` アカウントで最も重要な表で このタイムスタンプと `Last Data Point` は、問題がアカウント全体に影響を与えたか、テーブルのサブセットに影響を与えたかを示します。 一般的に使用される重要なテーブルを 3 ～ 4 つに対してこの操作をお勧めします。

- この `MAX(timestamp)` の値が `Last Data Point Received`つまり、テーブルのサブセットは影響を受けましたが、アカウント全体の更新サイクルは安定しています。
- この `MAX(timestamp)` 値が次の値と等しいかそれ以前 `Last Data Point Received`の場合は、アカウントの更新サイクルが影響を受けたことを意味します。 この状況では、 [サポートチケットを提出する](../../../guide-overview.md).
