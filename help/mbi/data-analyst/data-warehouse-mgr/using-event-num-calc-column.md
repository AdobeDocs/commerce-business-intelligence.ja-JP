---
title: イベント数計算列
description: イベント番号の計算列の目的と使用について説明します。
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# イベント数計算列

このトピックでは、`Event Number` ページで使用できる **[!DNL Manage Data > Data Warehouse]** の計算列の目的と使用の概要を説明します。 以下に、その機能の説明、例、およびそれを作成する仕組みを示します。

**説明**

`Event Number` 列タイプは、**や** など、特定の `customer` イベント所有者 `user` に対してイベントが発生したシーケンスを識別します。 SQL に精通している場合、このカラム タイプは `RANK` 関数と同じです。 これを使用すると、データ内の初回イベント、リピートイベントまたは n 番目のイベント間で動作の違いを確認できます。

同数の場合、この列には同数のイベントに対して同じ **ランク** が含まれ、後続の数値はスキップされます。 例えば、5,8,10,10,12 という数字をランク付けした場合、ランクは 1,2,3,3,5 になります。

この列の最も一般的なユースケースは、初回購入者とリピート購入者を分析することです。 最初に購入者を識別するには、（指標またはレポートに）フィルターを `Customer's order number` = 1 に追加します。 `Customer's order number` は `Event Number` 型の列です。

**例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

上記の例では、列 `Owner's event number` は `Event Number` 列です。 所有者のイベントを、発生した順序（`timestamp` 列に基づく）でランク付けします。

例えば、`owner_id = A` のすべての行を考慮に入れます。 テーブルの最初の行は、この所有者の最も古いタイムスタンプ、テーブルの 3 行目、テーブルの 4 行目が続きます。

**力学**

`Event Number` 列の作成手順を次に示します。

1. **[!UICONTROL Manage Data > Data Warehouse]** ページに移動します。

1. この列を作成するテーブルに移動します。

1. 「**[!UICONTROL Create a Column]**」をクリックし、「`EVENT_NUMBER (…)`」セクションで `Same Table` 列タイプを選択します。

1. 最初のドロップダウン `Event Owner` は、ランクを決定するエンティティを指定します。 `Customer's order number` の場合、`customer_id` や `customer_email` などの顧客識別子が `Event Owner` になります。

1. 2 つ目のドロップダウン `Event Rank` は、行のランクを決定するシーケンスを強制する列を指定します。 `Customer's order number` の場合、`created_at` のタイムスタンプは `Event Rank` になります。

1. `Options` のドロップダウンで、フィルターを追加して、行を考慮から除外することができます。 除外された行には、この列の `NULL` 値があります。

1. 列に名前を付け、「**[!UICONTROL Save]**」をクリックします。

1. この列は、_immediately._ を使用できます。
