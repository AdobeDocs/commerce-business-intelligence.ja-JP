---
title: SQL クエリのCommerce Intelligence レポートへの変換
description: SQL クエリをCommerce Intelligence で使用する計算列（指標）に変換する方法を説明します。
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# Commerce Intelligence での SQL クエリの翻訳

SQL クエリがにどのように変換されるかを疑問に思ったことはありません [計算される列](../data-warehouse-mgr/creating-calculated-columns.md), [指標](../../data-user/reports/ess-manage-data-metrics.md)、および [報告書](../../tutorials/using-visual-report-builder.md) でを使用しています [!DNL Commerce Intelligence]? 大量の SQL ユーザーの場合は、での SQL の翻訳方法を理解する [!DNL Commerce Intelligence] を使用すると、でよりスマートに作業できます [Data Warehouse管理者](../data-warehouse-mgr/tour-dwm.md) を最大限に活用 [!DNL Commerce Intelligence] プラットフォーム。

このトピックの最後には、 **翻訳マトリックス** SQL 問合せ句および [!DNL Commerce Intelligence] 要素。

まず、一般的なクエリを確認します。

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | 報告書 `group by` |
| `SUM(b)` | `Aggregate function` （列） |
| `FROM c` | `Source` テーブル |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | 報告書 `time frame` |
| `GROUP BY a` | 報告書 `group by` |

この例ではほとんどの翻訳ケースをカバーしていますが、例外もあります。 方法から始まる、の詳細 `aggregate` 関数が翻訳されます。

## 集計関数

集計関数（例： `count`, `sum`, `average`, `max`, `min`）に設定する必要があります。 **指標集計** または **列の集計** 。対象： [!DNL Commerce Intelligence]. 差別化要因は、集計を実行するために結合が必要かどうかです。

上記のそれぞれの例を参照してください。

## 指標の集計 {#aggregate}

集計時には指標が必要です `within a single table`. 例： `SUM(b)` 上記のクエリの集計関数は、おそらく、列を合計する指標で表されます `B`. 

方法の具体的な例を見る `Total Revenue` 指標は次で定義できます [!DNL Commerce Intelligence]. 翻訳を試みる以下のクエリを確認します。

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` （列） |
| `FROM orders` | `Metric source` テーブル |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 指標 `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | 指標 `timestamp` （およびレポート `time range`） |

をクリックして指標ビルダーに移動します。 **[!UICONTROL Manage Data** > **&#x200B;指標&#x200B;**> **新しい指標を作成]**&#x200B;最初に、適切なを選択する必要があります `source` テーブル（この場合は） `orders` テーブル。 次に、指標は次のように設定されます。

![指標の集計](../../assets/Metric_aggregation.png)

## 列の集計

集計列は、別のテーブルから結合されている列を集計する場合に必要です。 例えば、に列を作成できます `customer` テーブル名 `Customer LTV`。この顧客に関連付けられているすべての注文の合計値を `orders` テーブル。

この集計のクエリは、次のようになります。

|  |  |
|--- |--- |
| `Select` | |
| `c.customer_id` | 集計所有者 |
| `SUM(o.order_total) as "Customer LTV"` | 集計操作（列） |
| `FROM customers c` | 所有者テーブルを集計 |
| `JOIN orders o` | 集計ソーステーブル |
| `ON c.customer_id = o.customer_id` | パス |
| `WHERE o.status = 'success'` | 集計フィルター |

での設定 [!DNL Commerce Intelligence] では、Data Warehouseマネージャーを使用して、 `orders` および `customers` テーブルで、という名前の列を作成します。 `Customer LTV` 顧客のテーブルに追加します。

間に新しいパスを確立する方法を見る `customers` および `orders`. 最後の目標は、に新しい集計列を作成することです。 `customers` テーブルなので、最初にに移動します `customers` Data Warehouseのテーブルで、 **[!UICONTROL Create a Column** > **&#x200B;定義を選択&#x200B;**> **SUM]**.

次に、ソーステーブルを選択する必要があります。 にパスが存在する場合 `orders` テーブル。ドロップダウンから選択するだけです。 ただし、新しいパスを作成する場合は、 **[!UICONTROL Create new path]** 次の画面が表示されます。

![新しいパスを作成](../../assets/Create_new_path.png)

ここでは、結合しようとしている 2 つのテーブル間の関係を慎重に検討する必要があります。 この場合、次の可能性があります `Many` 関連するオーダー `One` 顧客、したがって `orders` テーブルはに一覧表示されます `Many` 辺と、 `customers` で選択したテーブル `One` 辺。

>[!NOTE]
>
>対象： [!DNL Commerce Intelligence], a `path` は、と同等です。 `Join` （SQL の場合）。

パスを保存したら、 `Customer LTV` 列！ 以下を参照してください。

![](../../assets/Customer_LTV.gif)

これで、新しい `Customer LTV` の列 `customers` テーブルを作成する準備が整いました [指標の集計](#aggregate) この列の使用（例えば、顧客ごとの平均 LTV を検索） 以下の手順でも可能です `group by` または `filter` で作成された既存の指標を使用した、レポートの計算列別 `customers` テーブル。

>[!NOTE]
>
>後者の場合、新しい計算列を作成する際はいつでも次の操作を行う必要があります [既存の指標へのディメンションの追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) として使用する前に `filter` または `group by`.

参照： [計算列の作成](../data-warehouse-mgr/creating-calculated-columns.md) とData Warehouse管理者。

## `Group By` 条項

`Group By` クエリ内の関数は、多くの場合、で表現されます。 [!DNL Commerce Intelligence] ビジュアルレポートのセグメント化やフィルタリングに使用される列。 例として、を再検討します。 `Total Revenue` 以前に調査したクエリですが、今回は次の方法で売上高をセグメント化します `coupon\_code` 最も多くの売上高を生み出しているクーポンについての理解を深めるために。

以下のクエリから開始します。

| | |
|--- |--- |
| `SELECT coupon_code,` | 報告書 `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`（列） |
| `FROM orders` | `Metric source` テーブル |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 指標 `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | 指標 `timestamp` （およびレポート `time range`） |
| `GROUP BY coupon_code` | 報告書 `group by` |

>[!NOTE]
>
>以前に開始したクエリとの唯一の違いは、グループ化の基準として「coupon\_code」が追加されたことです。_

同じを使用 `Total Revenue` 以前に作成した指標を使用すると、クーポンコードでセグメント化された売上高のレポートを作成する準備が整います。 9 月から 11 月のデータを調べて、このビジュアルレポートを設定する方法を示す以下の gif を見てください。

![クーポンコード別売上高](../../assets/Revenue_by_coupon_code.gif)

## 数式

場合によっては、クエリには、別々の列間の関係を計算するために複数の集計が含まれることがあります。 例えば、次の 2 つの方法のいずれかを使用して、クエリの平均注文値を計算できます。

* `AVG('order\_total')` または
* `SUM('order\_total')/COUNT('order\_id')`

前の方法では、で平均を実行する新しい指標を作成します `order\_total` 列。 ただし、を計算するための指標が既に設定されている場合は、後者のメソッドを Report Builder で直接作成できます `Total Revenue` および `Number of orders`.

一歩下がって、のクエリ全体を確認します `Average order value`:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | 指標 `operation` （列） |
| `COUNT(order_id) as "Number of orders"` | 指標 `operation` （列） |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | 指標 `operation` （列）/指標の操作（列） |
| `FROM orders` | 指標 `source` テーブル |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 指標 `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | 指標のタイムスタンプ（およびレポートの時間範囲） |

次に、を計算するための指標が既に設定されているとします `Total Revenue` および `Number of orders`. これらの指標は存在するので、次を開くだけです： `Report Builder` を使用してオンデマンド計算を作成します `Formula` 機能：

![AOV フォーラム](../../assets/AOV_forumula.gif)

## まとめ

SQL を大量に使用する場合は、クエリの翻訳方法を検討します。 [!DNL Commerce Intelligence] では、計算列、指標およびレポートを作成できます。

クイックリファレンスについては、以下のマトリックスをご覧ください。 これは、SQL 句の同等のものを示します [!DNL Commerce Intelligence] 要素と、クエリでの使用方法に応じて、複数の要素にマッピングする方法。

## Commerce Intelligence の要素

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` （時間要素を使用） | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
