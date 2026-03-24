---
title: データベースとSQL エディター間の結果の理解
description: データベースとSQL エディター間の結果を理解する方法を説明します。
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/pScH-yKW8hbSNZzsJ537CN7rxhcuygaLmCu3fdVaYgk
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
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 257
ht-degree: 0%

---

# データベース結果と[!DNL SQL Editor]結果の比較

`Last successful update began` ページ内の`Integrations` フィールドの内容に興味がある場合があります。

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## `timestamp` フィールドについて

アカウントの`timestamp`最後に成功した更新サイクル _の開始_ （アカウントに設定されたタイムゾーン）が表示されます。

- 同期されたテーブルのいずれかが、前回の更新サイクル中に問題が発生した場合、このタイムスタンプは&#x200B;*更新されません*。
- そのため、新しいデータでレポートが更新された場合もありますが、*最後に正常に更新が開始された*&#x200B;はまだ遅れています。

## 最後の「実際の」データポイントの特定

特定の統合の最新のデータポイントは、各統合の右側にある`Last Data Point Received` タイムスタンプによって決まります。 このタイムスタンプとは、データベース、API、サードパーティ統合など、Data Warehouseがそのソースからデータポイントを正常に受信した最後の時点を指します。

*特定のテーブル*&#x200B;のデータの鮮度を確認するには、Adobeでは、アカウントの最も重要なテーブルで[[!DNL SQL] を実行する簡単な](../../dev-reports/sql-rpt-bldr.md) レポート `MAX(timestamp)`を作成することをお勧めします。 このタイムスタンプを`Last Data Point`と比較すると、問題がアカウント全体またはテーブルのサブセットに影響を与えたかどうかを示します。 Adobeでは、3つから4つの重要な一般的に使用されるテーブルに対して行うことをお勧めします。

- `MAX(timestamp)`の値が`Last Data Point Received`より新しい場合、テーブルのサブセットが影響を受けましたが、アカウント全体の更新サイクルは安定しています。
- `MAX(timestamp)`の値が`Last Data Point Received`以前の場合、アカウントの更新サイクルが影響を受けたことを意味します。 このような状況では、[&#x200B; サポートチケットを送信](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)します。
