---
title: 順次比較の計算列
description: 順次比較計算列の目的と使用について説明します。
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# 順次比較の計算列

このトピックでは、 `Sequential Comparison` で使用できる計算列 **[!DNL Manage Data > Data Warehouse]** ページ。 以下に、その機能の説明を示し、その後に例と作成の仕組みを示します。

**説明**

この `Sequential Comparison` 列タイプ：連続したイベントの違いを検索します。 最も一般的なタイプの `Sequential Comparison` 列は `Seconds since previous order` 列。 この列には、次の 3 つの入力が必要です。

1. `Event Owner`：この入力は、行がグループ化されるエンティティを決定します。 例： `Seconds since previous order` 列で、イベントの所有者は顧客です。これは、同じ顧客の前回の注文からの秒数を求めるためです。
1. `Event Date`：この入力は、イベントのシーケンスを強制します。 の場合 `Seconds since previous order`。注文のタイムスタンプを含む列は、です `Event Date`. この入力は常にタイムスタンプです。
1. `Value to Compare`：比較される実際の値です。 現在の行の値から前の行の値を減算します。 したがって、顧客の連続する注文の時間差を求める列が呼び出されます `Seconds since previous order`. この入力はタイムスタンプである必要はありません。 タイムスタンプ以外の例では、顧客の連続する注文間の注文値の違いを見つけます。

**例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | NULL |
| **`2`** | B | 2015-01-01 00:30:00 | NULL |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

上記の例では、 `Seconds since owner's previous event` が `Sequential Comparison` 集計列。 の場合 `owner_id = A`最初に、に基づいてシーケンスを識別します `timestamp` 列に追加し、直前のイベントの `timestamp` 現在のイベントのタイムスタンプから。 テーブルの 3 行目 – 2 行目 `owner_id A`  – の値 `Seconds since owner's previous event` は、「2015-01-01 02:00」から「2015-01-01 00」までの秒数です:00:00&#39;。 この差は、2 時間= 7200 秒に等しくなります。

この計算列タイプの場合、所有者の最初のイベントに対応する行には `NULL` の値。

**仕組み**

を作成するには **イベント番号** 列：

1. に移動します。 **[!DNL Manage Data > Data Warehouse]** ページ。

1. この列を作成するテーブルに移動します。

1. クリック **[!UICONTROL Create New Column]** 右上隅

1. を選択 `Same Table` as the `Definition Type` （比較する列が同じテーブルにない場合は、再配置する必要がある可能性があります）。

1. を選択 `SEQUENTIAL_COMPARISON` as the `Column Definition Equation`.

1. 入力を選択します（前述）。
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. フィルターを追加して、行を考慮から除外することもできます。 除外行には、 `NULL` この列の値。

1. ページ上部の列の名前を指定し、 **[!UICONTROL Save]**.

1. 列は使用可能です *即時*.

![秒](../../assets/SEC_new.png)
