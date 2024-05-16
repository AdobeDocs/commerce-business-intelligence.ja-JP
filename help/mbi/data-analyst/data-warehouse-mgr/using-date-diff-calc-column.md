---
title: 日付の差異の計算列の使用
description: 日付差異の計算列の目的と使用について説明します。
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---

# 日付の差異の計算列

このトピックでは、 `Date Difference` で使用できる計算列 **[!DNL Manage Data > Data Warehouse]** ページ。 以下に、その機能の説明、例、およびそれを作成する仕組みを示します。

**説明**

この `Date Difference` 列タイプは、イベントのタイムスタンプに基づいて、1 つのレコードに属する 2 つのイベント間の時間を計算します。 この列で計算された生の値は秒単位ですが、レポートに表示するために分、時間、日などに自動変換されます。 ただし、でフィルター/グループ化として使用する場合は、秒単位の値を使用します。

A `date difference` 計算列を使用すると、顧客登録から最初の注文までの平均時間など、2 つのイベント間の平均または中央値の時間を計算する指標を作成できます。

**例**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}


上記の例では、 `Date Difference` 列は `Seconds between timestamp_2 and timestamp_1` 列。 計算が実行されます `timestamp_2 minus timestamp_1`.

**仕組み**

以下の手順では、を作成する方法について説明します `Date Difference` 列。

1. に移動します。 **[!DNL Manage Data > Data Warehouse]** ページ。
1. この列を作成するテーブルに移動します。
1. クリック **[!UICONTROL Create a Column]** そして、次のように列を設定します。
   * を選択 `Column Definition Type` > `Same Table`
   * を選択 `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * を選択 `Ending DATETIME` 列 > 終了日時フィールドを選択します（通常、後で発生するイベント）
   * を選択 `Starting DATETIME` 列** > 開始時刻フィールドを選択します。通常、このフィールドより前に発生するイベントです

1. 列に名前を付け、 **[!UICONTROL Save]**.
1. 列は使用可能です *即時*.

例えば、次の例はを計算するように設定されています。 `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
