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

このトピックでは、`Sequential Comparison` ページで使用できる **[!DNL Manage Data > Data Warehouse]** の計算列の目的と使用の概要を説明します。 以下に、その機能の説明を示し、その後に例と作成の仕組みを示します。

**説明**

`Sequential Comparison` 列タイプ：連続するイベントの違いを見つけます。 最も一般的な列 `Sequential Comparison` タイプは `Seconds since previous order` 列です。 この列には、次の 3 つの入力が必要です。

1. `Event Owner`：この入力は、行がグループ化されるエンティティを決定します。 例えば、「`Seconds since previous order`」列のイベント所有者が顧客である場合は、同じ顧客を前回注文からの秒数を求めるためです。
1. `Event Date`：この入力は、イベントのシーケンスを強制します。 `Seconds since previous order` の場合、注文のタイムスタンプを含む列は `Event Date` にする必要があります。 この入力は常にタイムスタンプです。
1. `Value to Compare`：この入力は、比較される実際の値です。 現在の行の値から前の行の値を減算します。 したがって、顧客の連続する注文の時間差を求める列は `Seconds since previous order` と呼ばれます。 この入力はタイムスタンプである必要はありません。 タイムスタンプ以外の例では、顧客の連続する注文間の注文値の違いを見つけます。

**例**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | NULL |
| **`2`** | B | 2015-01-01 00:30:00 | NULL |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

上記の例では、`Seconds since owner's previous event` が `Sequential Comparison` の計算列です。 `owner_id = A` の場合、最初に `timestamp` 列に基づいてシーケンスを識別し、次に現在のイベントのタイムスタンプから前のイベントの `timestamp` を減算します。 テーブルの 3 行目（`owner_id A` の 2 行目）の `Seconds since owner's previous event` の値は、「2015-01-01 02:00」と「2015-01-01 00:00:00」の間の秒数です。 この差は、2 時間= 7200 秒に等しくなります。

この計算列タイプの場合、所有者の最初のイベントに対応する行には `NULL` 値があります。

**力学**

**イベント番号** 列を作成するには：

1. **[!DNL Manage Data > Data Warehouse]** ページに移動します。

1. この列を作成するテーブルに移動します。

1. 右上隅の「**[!UICONTROL Create New Column]**」をクリックします。

1. `Same Table` として「`Definition Type`」を選択します（比較する列が同じテーブルにない場合は、再配置する必要がある可能性があります）。

1. `SEQUENTIAL_COMPARISON` として `Column Definition Equation` を選択します。

1. 入力を選択します（前述）。
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. フィルターを追加して、行を考慮から除外することもできます。 除外された行には、この列の `NULL` 値があります。

1. ページ上部の列の名前を指定し、「**[!UICONTROL Save]**」をクリックします。

1. この列は *即時* に使用できます。

![ 秒 ](../../assets/SEC_new.png)
