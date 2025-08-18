---
title: SQL クエリのCommerce Intelligence レポートへの変換
description: SQL クエリをCommerce Intelligenceで使用する計算列（指標）に変換する方法について説明します。
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# Commerce Intelligenceでの SQL クエリの翻訳

SQL クエリを [ で使用する ](../data-warehouse-mgr/creating-calculated-columns.md) 計算列 [、](../../data-user/reports/ess-manage-data-metrics.md) 指標 [、および ](../../tutorials/using-visual-report-builder.md) レポート [!DNL Commerce Intelligence] に変換する方法を疑問に思ったことはありませんか？ SQL を大量に使用するユーザーの場合は、[!DNL Commerce Intelligence] での SQL の翻訳方法を理解することで、[Data Warehouse Manager でよりスマートに作業し ](../data-warehouse-mgr/tour-dwm.md) [!DNL Commerce Intelligence] プラットフォームを最大限に活用できます。

このトピックの最後には、SQL クエリ句と **要素の** 翻訳行列 [!DNL Commerce Intelligence] があります。

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

この例ではほとんどの翻訳ケースをカバーしていますが、例外もあります。 `aggregate` 関数の翻訳方法から説明します。

## 集計関数

クエリの集計関数（`count`、`sum`、`average`、`max`、`min` など）は、**では** 指標の集計 **または** 列の集計 [!DNL Commerce Intelligence] のいずれかの形式を取ります。 差別化要因は、集計を実行するために結合が必要かどうかです。

上記のそれぞれの例を参照してください。

## 指標の集計 {#aggregate}

`within a single table` ータを集計する場合は、指標が必要です。 したがって、例えば、上記のクエリの `SUM(b)` 集計関数は、列の `B` を合計する指標で表される可能性が高くなります。 

`Total Revenue` での [!DNL Commerce Intelligence] 指標の定義方法に関する、特定の例を見てみましょう。 翻訳を試みる以下のクエリを確認します。

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` （列） |
| `FROM orders` | `Metric source` テーブル |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 指標 `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | 指標 `timestamp` （およびレポート `time range`） |

**[!UICONTROL Manage Data** > **&#x200B; 指標 &#x200B;**/**新しい指標を作成]** をクリックして指標ビルダーに移動します。まず、適切な `source` テーブル（この場合は `orders` テーブル）を選択する必要があります。 次に、指標は次のように設定されます。

![ 指標の集計 ](../../assets/Metric_aggregation.png)

## 列の集計

集計列は、別のテーブルから結合されている列を集計する場合に必要です。 例えば、`customer` テーブルに `Customer LTV` という列を作成し、その顧客に関連付けられたすべての注文の合計値を `orders` テーブルに合計するとします。

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

[!DNL Commerce Intelligence] でこれを設定するには、Data Warehouse Manager を使用する必要があります。ここでは、`orders` と `customers` のテーブルの間にパスを作成し、顧客のテーブルに `Customer LTV` という列を作成します。

`customers` と `orders` の間に新しいパスを確立する方法を確認します。 最後の目標は、`customers` テーブルに新しい集計列を作成することです。そのため、まずData Warehouseの `customers` テーブルに移動し、**[!UICONTROL Create a Column** > **&#x200B; 定義を選択 &#x200B;**/**SUM]** をクリックします。

次に、ソーステーブルを選択する必要があります。 `orders` テーブルへのパスが存在する場合は、ドロップダウンから選択するだけです。 ただし、新しいパスを作成している場合は、「**[!UICONTROL Create new path]**」をクリックすると、次の画面が表示されます。

![ 新しいパスを作成 ](../../assets/Create_new_path.png)

ここでは、結合しようとしている 2 つのテーブル間の関係を慎重に検討する必要があります。 この場合、顧客に関連付けられた注文が `Many` い可能性があ `One` ので、`orders` 側には `Many` のテーブルが表示され、`customers` 側には `One` のテーブルが選択されます。

>[!NOTE]
>
>[!DNL Commerce Intelligence] では、`path` は SQL の `Join` と同等です。

パスを保存したら、`Customer LTV` の列を作成できます。 以下を参照してください。

![](../../assets/Customer_LTV.gif)

`Customer LTV` テーブルに新しい `customers` 列を作成したので、この列を使用して [ 指標の集計 ](#aggregate) を作成する準備が整いました（例えば、顧客あたりの平均 LTV を見つける場合）。 また、`group by` テーブルに基づいて作成された既存の指標を使用して、レポートの計算列で `filter` 計または `customers` 計することもできます。

>[!NOTE]
>
>後者の場合、新しい計算列を作成する際は、ディメンションを [ または ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) として使用する前に、`filter` 既存の指標にディメンションを追加 `group by` する必要があります。

詳しくは、Data Warehouse Manager で [ 計算列の作成 ](../data-warehouse-mgr/creating-calculated-columns.md) を参照してください。

## `Group By` 句

クエリの `Group By` 関数は、多くの場合、視覚的なレポートのセグメント化やフィルタリングに使用される列として、[!DNL Commerce Intelligence] で表されます。 例として、以前に調べた `Total Revenue` クエリを再確認しますが、今回は、最も売上高が多いクーポンを理解するために、`coupon\_code` による売上高をセグメント化します。

以下のクエリから開始します。

| | |
|--- |--- |
| `SELECT coupon_code,` | 報告書 `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` （列） |
| `FROM orders` | `Metric source` テーブル |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 指標 `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | 指標 `timestamp` （およびレポート `time range`） |
| `GROUP BY coupon_code` | 報告書 `group by` |

>[!NOTE]
>
>以前に開始したクエリとの唯一の違いは、グループ化の基準として「coupon\_code」が追加されたことです。_

以前に作成したのと同じ `Total Revenue` 指標を使用して、クーポンコードでセグメント化された売上高のレポートを作成する準備が整いました。 9 月から 11 月のデータを調べて、このビジュアルレポートを設定する方法を示す以下の gif を見てください。

![ クーポンコード別売上高 ](../../assets/Revenue_by_coupon_code.gif)

## 数式

場合によっては、クエリには、別々の列間の関係を計算するために複数の集計が含まれることがあります。 例えば、次の 2 つの方法のいずれかを使用して、クエリの平均注文値を計算できます。

* `AVG('order\_total')` または
* `SUM('order\_total')/COUNT('order\_id')`

前者の方法では、`order\_total` 列を平均する新しい指標を作成します。 ただし、`Total Revenue` と `Number of orders` を計算するための指標が既に設定されている場合は、後者のメソッドを Report Builder で直接作成できます。

一歩下がって、`Average order value` のクエリ全体を確認します。

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | 指標 `operation` （列） |
| `COUNT(order_id) as "Number of orders"` | 指標 `operation` （列） |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | 指標 `operation` （列）/指標操作（列） |
| `FROM orders` | 指標 `source` テーブル |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | 指標 `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | 指標のタイムスタンプ（およびレポートの時間範囲） |

ここで、`Total Revenue` と `Number of orders` を計算するための指標が既に設定されているとします。 これらの指標は存在するので、`Report Builder` を開き、`Formula` の機能を使用してオンデマンド計算を作成するだけです。

![AOV forumula](../../assets/AOV_forumula.gif)

## まとめ

SQL を大量に使用する場合は、クエリが [!DNL Commerce Intelligence] でどのように翻訳されるかを考えることで、計算列、指標およびレポートを作成できます。

クイックリファレンスについては、以下のマトリックスをご覧ください。 これは、SQL 句の同等の [!DNL Commerce Intelligence] 要素と、クエリでの使用方法に応じて、複数の要素にどのようにマッピングできるかを示します。

## Commerce Intelligenceの要素

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` （時間要素を含む） | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
