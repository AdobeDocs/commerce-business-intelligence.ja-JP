---
title: 順次比較計算列
description: 順次比較計算列の目的と用途について説明します。
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 2%

---

# 順次比較計算列

このトピックでは、 `Sequential Comparison` で使用できる計算列 **[!DNL Manage Data > Data Warehouse]** ページに貼り付けます。 次に、その動作の説明と、それを作成する手法の例を示します。

**説明**

The `Sequential Comparison` 列タイプ：連続するイベント間の差異を検索します。 最も一般的なタイプの `Sequential Comparison` 列は `Seconds since previous order` 列。 この列には、次の 3 つの入力が必要です。

1. `Event Owner`：この入力は、行がグループ化されるエンティティを決定します。 例えば、 `Seconds since previous order` 列に含まれるイベントの所有者は顧客です。同じ顧客の前回の注文からの秒数を求めるからです。
1. `Event Date`：この入力により、イベントのシーケンスが強制されます。 の場合 `Seconds since previous order`の場合、注文のタイムスタンプを含む列は、 `Event Date`. この入力は常にタイムスタンプです。
1. `Value to Compare`：この入力は、比較する実際の値です。 現在の行の値から前の行の値を引きます。 したがって、顧客の連続注文の時間差を見つける列は、と呼ばれます。 `Seconds since previous order`. この入力は、タイムスタンプにする必要はありません。 タイムスタンプのない例は、顧客の連続した注文の注文件数の差を見つけることです。

**例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | NULL |
| **`2`** | B | 2015-01-01 00:30:00 | NULL |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

上記の例では、 `Seconds since owner's previous event` が `Sequential Comparison` 計算列。 の `owner_id = A`の場合、最初に、 `timestamp` 列の後に、前のイベントの `timestamp` 現在のイベントのタイムスタンプから。 テーブルの 3 行目 — 2 行目 `owner_id A`  — の値 `Seconds since owner's previous event` は、「2015-01-01 02:00」から「2015-01-01 00」までの秒数です:00:00&#39;. この差は 2 時間= 7200 秒です。

この計算列タイプの場合、所有者の最初のイベントに対応する行には、 `NULL` の値です。

**力学**

次の手順で、 **イベント番号** 列：

1. 次に移動： **[!DNL Manage Data > Data Warehouse]** ページに貼り付けます。

1. この列を作成するテーブルに移動します。

1. クリック **[!UICONTROL Create New Column]** をクリックします。

1. 選択 `Same Table` として `Definition Type` （比較する列が同じテーブル上にない場合は、その列を再配置する必要がある場合があります）。

1. 選択 `SEQUENTIAL_COMPARISON` として `Column Definition Equation`.

1. 上記の説明に従って、入力を選択します。
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. また、フィルターを追加して、行が考慮されないようにします。 除外された行には、 `NULL` の値を指定します。

1. ページ上部の列の名前を指定し、 **[!UICONTROL Save]**.

1. この列は、 *即時*.

![秒](../../assets/SEC_new.png)
