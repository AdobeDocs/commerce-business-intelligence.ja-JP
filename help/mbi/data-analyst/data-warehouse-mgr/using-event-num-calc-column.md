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

このトピックでは、 `Event Number` で使用できる計算列 **[!DNL Manage Data > Data Warehouse]** ページ。 以下に、その機能の説明、例、およびそれを作成する仕組みを示します。

**説明**

この `Event Number` 列タイプは、特定のイベントが発生したシーケンスを識別します **イベント所有者**。例： `customer` または `user`. SQL を熟知している場合、この列タイプはと同じです `RANK` 関数。 これを使用すると、データ内の初回イベント、リピートイベントまたは n 番目のイベント間で動作の違いを確認できます。

同数の場合、この列には同じ値が含まれます **ランク** 結び付けられたイベントについては、後続の数値をスキップします。 例えば、5,8,10,10,12 という数字をランク付けした場合、ランクは 1,2,3,3,5 になります。

この列の最も一般的なユースケースは、初回購入者とリピート購入者を分析することです。 初回購入者は、（指標またはレポートに）フィルターを追加することで識別されます `Customer's order number` = 1。 `Customer's order number` は、型の列です `Event Number`.

**例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

上記の例では、列 `Owner's event number` は `Event Number` 列。 所有者のイベントを、発生した順序で（に基づいて）ランク付けします `timestamp` 列）に含まれます。

例えば、次のようなすべての行を検討します `owner_id = A`. テーブルの最初の行は、この所有者の最も古いタイムスタンプ、テーブルの 3 行目、テーブルの 4 行目が続きます。

**仕組み**

以下は、を作成する手順です。 `Event Number` 列：

1. に移動します。 **[!UICONTROL Manage Data > Data Warehouse]** ページ。

1. この列を作成するテーブルに移動します。

1. クリック **[!UICONTROL Create a Column]** を選択し、 `EVENT_NUMBER (…)` 列タイプ：の下 `Same Table` セクション。

1. 最初のドロップダウン `Event Owner` ランクを決定するエンティティを指定します。 次の場合 `Customer's order number`、などの顧客識別子。 `customer_id` または `customer_email` はになります。 `Event Owner`.

1. 2 つ目のドロップダウン `Event Rank` 行のランクを決定するシーケンスを強制する列を指定します。 次の場合 `Customer's order number`, `created_at` timestamp はとなります。 `Event Rank`.

1. の下 `Options` ドロップダウンでは、フィルターを追加して、行を考慮から除外できます。 除外行には、 `NULL` この列の値。

1. 列に名前を付け、 **[!UICONTROL Save]**.

1. 列は使用可能です _すぐに。_
