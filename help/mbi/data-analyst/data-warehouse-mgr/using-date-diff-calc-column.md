---
title: 日付差の計算列の使用
description: 日付の差異の計算列の目的と用途について説明します。
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 日付差の計算列

このトピックでは、 `Date Difference` で使用できる計算列 **[!DNL Manage Data > Data Warehouse]** ページに貼り付けます。 その動作の説明と、その後に例と、それを作る仕組みを次に示します。

**説明**

The `Date Difference` 列タイプは、イベントのタイムスタンプに基づいて、1 つのレコードに属する 2 つのイベント間の時間を計算します。 この列で計算される生の値は秒単位ですが、レポートに表示するために、分、時間、日などに自動変換されます。 ただし、でフィルターまたはグループ化として使用する場合は、秒単位の値を使用する必要があります。

A `date difference` 計算列は、顧客登録と初回注文の間の平均時間など、2 つのイベント間の平均時間または中央値時間を計算する指標の作成に使用できます。

**例**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}


上記の例では、 `Date Difference` 列は `Seconds between timestamp_2 and timestamp_1` 列。 計算を実行します `timestamp_2 minus timestamp_1`.

**力学**

次の手順で、 `Date Difference` 列。

1. 次に移動： **[!DNL Manage Data > Data Warehouse]** ページに貼り付けます。
1. この列を作成するテーブルに移動します。
1. クリック **[!UICONTROL Create a Column]** 列を次のように設定します。
   * 選択 `Column Definition Type` > `Same Table`
   * 選択 `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * 選択 `Ending DATETIME` 列/終了日時フィールドを選択します。通常は、後で発生するイベントです。
   * 選択 `Starting DATETIME` 列** /開始日時フィールドを選択します。これは通常、以前に発生したイベントです。

1. 列に名前を付け、 **[!UICONTROL Save]**.
1. この列は、 *即時*.

例えば、次の例は、 `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
