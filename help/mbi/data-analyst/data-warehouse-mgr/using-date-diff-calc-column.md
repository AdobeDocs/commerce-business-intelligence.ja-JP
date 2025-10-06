---
title: 日付の差異の計算列の使用
description: 日付差異の計算列の目的と使用について説明します。
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# 日付の差異の計算列

このトピックでは、`Date Difference` ページで使用できる **[!DNL Manage Data > Data Warehouse]** の計算列の目的と使用の概要を説明します。 以下に、その機能の説明、例、およびそれを作成する仕組みを示します。

**説明**

`Date Difference` 列タイプは、イベントのタイムスタンプに基づいて、1 つのレコードに属する 2 つのイベント間の時間を計算します。 この列で計算された生の値は秒単位ですが、レポートに表示するために分、時間、日などに自動変換されます。 ただし、でフィルター/グループ化として使用する場合は、秒単位の値を使用します。

`date difference` の計算列を使用すると、顧客登録から最初の注文までの平均時間など、2 つのイベント間の平均時間または中央値を計算する指標を作成できます。

**例**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}


上記の例では、`Date Difference` 列が `Seconds between timestamp_2 and timestamp_1` 列です。 計算 `timestamp_2 minus timestamp_1` を実行します。

**力学**

次の手順では、`Date Difference` 列の作成方法を説明します。

1. **[!DNL Manage Data > Data Warehouse]** ページに移動します。
1. この列を作成するテーブルに移動します。
1. 「**[!UICONTROL Create a Column]**」をクリックして、列を次のように設定します。
   * `Column Definition Type` > `Same Table` を選択します。
   * `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)` を選択します。
   * 列 `Ending DATETIME` 選択/終了日時フィールドを選択します（通常、後で発生するイベント）
   * 列 `Starting DATETIME` 選択** /開始時刻フィールドを選択します。通常、このフィールドは以前に発生したイベントです

1. 列に名前を付け、「**[!UICONTROL Save]**」をクリックします。
1. この列は *即時* に使用できます。

例えば、次の例は、`Seconds between order date and customer's creation date` を計算するように設定されています。

![datetime 列の選択を示す日付差異の計算の設定 &#x200B;](../../assets/date_diff.png)
