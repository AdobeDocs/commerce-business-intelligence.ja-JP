---
title: イベント番号計算列
description: イベント番号計算列の目的と用途について説明します。
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# イベント番号計算列

このトピックでは、 `Event Number` 計算列は **[!DNL Manage Data > Data Warehouse]** ページ。 その動作の説明と、その後に例と、それを作る仕組みを示します。

**説明**

この `Event Number` 列タイプ：特定の **イベント所有者**、 `customer` または `user`. SQL に詳しい場合、この列のタイプは `RANK` 関数に置き換えます。 この関数を使用して、データ内の初回イベント、繰り返しイベント、n 番目のイベントの動作の違いを観察できます。

結び付けの場合、この列には同じ **rank** 結び付けられたイベントに対して実行し、後続の数値をスキップします。 例えば、5、8、10、10、12 という数値をランク付けしている場合、ランクは 1、2、3、3、5 になります。

この列の最も一般的な使用例は、初めての購入者とリピート購入者を分析することです。 初めて、購入者が、 `Customer's order number` = 1. `Customer's order number` はタイプの列です `Event Number`.

**例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

上記の例では、列 `Owner's event number` は `Event Number` 列。 所有者のイベントを、発生した順序 ( `timestamp` 」列 ) を参照してください。

例えば、次の場所にあるすべての行を考えてみます。 `owner_id = A`. テーブルの最初の行がこの所有者の最も早いタイムスタンプで、その後にテーブルの 3 番目の行、その後にテーブルの 4 番目の行が続きます。

**力学**

以下に、 `Event Number` 列：

1. 次に移動： **[!UICONTROL Manage Data > Data Warehouse]** ページ。
1. この列を作成するテーブルに移動します。
1. クリック **[!UICONTROL Create a Column]** を選択し、 `EVENT_NUMBER (…)` 列タイプ：の下に `Same Table` 」セクションに入力します。
1. 最初のドロップダウン `Event Owner` ランクを決定するエンティティを指定します。 の場合 `Customer's order number`、顧客識別子（例： ） `customer_id` または `customer_email` は `Event Owner`.
1. 2 番目のドロップダウン `Event Rank` 行のランクを決定する順序を強制する列を指定します。 の場合 `Customer's order number`、 `created_at` timestamp は `Event Rank`.
1. 以下 `Options` ドロップダウンで、フィルターを追加して、考慮しない行を除外できます。 除外された行には、 `NULL` の値を指定します。
1. 列に名前を付け、「 **[!UICONTROL Save]**.
1. この列は、 _すぐに_
