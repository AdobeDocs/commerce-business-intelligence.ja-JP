---
title: イベント数計算列
description: イベント数計算列の目的と用途について説明します。
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/vLN8AubwPn0Cq0CmmVq4nHbWNjWrCZNBvfhSDsE6lBw
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 399
ht-degree: 1%

---

# イベント数計算列

このトピックでは、`Event Number` ページで利用できる&#x200B;**[!DNL Manage Data > Data Warehouse]**&#x200B;計算列の目的と用途について説明します。 以下では、その仕組みと例、そして作成方法について説明します。

**説明**

`Event Number`列タイプは、**や**&#x200B;など、特定の`customer` イベント所有者`user`に対してイベントが発生したシーケンスを識別します。 SQLに精通している場合、この列タイプは`RANK`関数と同じです。 初回イベント、リピートイベント、データ内のn回のイベントの行動の違いを確認するために使用できます。

タイの場合、この列には、タイ付きイベントに対して同じ&#x200B;**ランク**&#x200B;が含まれており、後続の数値はスキップされます。 例えば、5,8,10,10,12という数字をランク付けした場合、ランクは1,2,3,3,5になります。

この列の最も一般的な使用例は、初回購入者とリピート購入者を分析することです。 `Customer's order number` = 1に（指標またはレポートに）フィルターを追加することで、初めての購入者を識別します。 `Customer's order number`は型`Event Number`の列です。

**例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

上記の例では、列`Owner's event number`は`Event Number`列です。 所有者のイベントを発生した順序でランク付けします（`timestamp`列に基づいて）。

例えば、`owner_id = A`のすべての行を考えてみましょう。 テーブルの最初の行は、この所有者の最も早いタイムスタンプで、次にテーブルの3番目の行、次にテーブルの4番目の行です。

**力学**

`Event Number`列の作成手順を以下に示します。

1. **[!UICONTROL Manage Data > Data Warehouse]** ページに移動します。

1. この列を作成するテーブルに移動します。

1. 「**[!UICONTROL Create a Column]**」をクリックし、「`EVENT_NUMBER (…)`」セクションの「`Same Table`」列タイプを選択します。

1. 最初のドロップダウン `Event Owner`は、ランクを決定するエンティティを指定します。 `Customer's order number`の場合、`customer_id`や`customer_email`などの顧客識別子は`Event Owner`になります。

1. 2番目のドロップダウン `Event Rank`は、行のランクを決定するシーケンスを適用する列を指定します。 `Customer's order number`の場合、`created_at` タイムスタンプは`Event Rank`になります。

1. `Options` ドロップダウンで、フィルターを追加して、行を考慮から除外できます。 除外された行には、この列の`NULL`値があります。

1. 列に名前を指定して、**[!UICONTROL Save]**&#x200B;をクリックします。

1. この列は、_をすぐに使用できます。_
