---
title: Report Builder内の数式
description: Report Builderで数式を使用する方法を説明します。
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# 内の数式 `Report Builder`

が含まれる [`Report Builder`](../../tutorials/using-visual-report-builder.md)を使用すると、強力なビジュアライゼーションを作成できます [定義済みの指標](../../data-user/reports/ess-manage-data-metrics.md) あなたの口座に。 これらの指標を式で組み合わせることで、データから追加のインサイトを得ることができます。 このトピックでは、で式を使用する方法について説明します `Report Builder`  – 飛び込もう！

## とは `formula`? {#what}

が含まれる `Report Builder`, a `formula` は、何らかの数学的論理に基づいて 1 つ以上の指標を組み合わせたものです。 典型的な例を次に示します。

![](../../assets/formula-example.png)

この例では、を使用します `Number of orders metric (A)` および `Distinct buyers metric (B)`を選択します。その後の目標は、「購入者が月に作成した注文の平均数はどれくらいか」という質問に答えることです。 式のパラメーターは次のとおりです。

* `Definition`：ここでは、入力指標に数学を適用します。 この例では、注文数を個別の購入者の数で割ると、注文数の平均がわかります。 したがって、の定義は（A/B）になります。

* `Format`：数式は数値、期間、または通貨金額を返しますか？ 数式の定義の横にはドロップダウンがあり、これを使用して戻り値の形式を指定できます。 この場合、数値です。

* `Miscellaneous`：数式のタイムスタンプ、グループ化、パースペクティブ、フィルターはすべて、入力指標に継承されます。 何もすることがない！

## 使用方法 `formulas` 報告書に？ {#how}

基本について説明したので、いくつかの例を見てみましょう。

### 例：初回注文に起因する売上高の割合を確認したい。

![数式を使用して初回注文に起因する収益の割合を見つける](../../assets/first_time_orders.gif)

この例では、を使用しました `Revenue` および `Revenue (first time orders)` 指標。 を除算する `Revenue (first time orders)(B)` による指標 `Revenue metric (A)` 戻り値の形式をに設定します。 `Percent`を使用すると、初回注文の売上高に占める割合を確認できます。

### 例：オファーを行う場合と行わない場合の、注文あたりの平均売上高を知りたい `promo code`.

![プロモーションコードを使用した場合と使用しない場合の、注文あたりの平均売上高を示す数式の使用](../../assets/promo_code.gif)

この例では、を使用しました `Revenue` および `Number of orders` 指標。 この質問に対する答えは、次の 2 つの手順で構成されます。 `Revenue (A)` 基準： `Number of orders (B)` 戻り値の形式をに設定します。 `Currency`. 次に、式の結果（`Avg. Revenue per order`）を選択して、結果を次の基準で表示およびグループ化します `Promo code`.

### 例：新規顧客の UTM ソースの配布を知りたいとします。

![数式を使用して新規顧客の UTM ソースの配分を検索する](../../assets/distro.gif)

この質問に対する答えを見つけるには、次の手順が必要です。

1. 最初にを追加しました `New Customers` 指標、さらにグループ化の基準 `utm_source - all`. これは指標です `A`、または `New Customers (grouped)`.

1. 次に、を複製しました `New Customers (grouped)` 指標を使用し、独立のディメンションを使用するように設定します。 指標 `B` - `New customers (ungrouped)`  – 新規顧客の合計数を表示します。

1. 両方の指標を非表示にした後、数式の定義をに設定します `A/B`. これにより、 `New customers (grouped)` 基準： `New Customers (ungrouped)`.

1. 次に、結果の形式をに設定します。 `Percent`.

この例では、を使用しました `Stacked Columns` パースペクティブ：結果を月ごとに表示します。 これにより、新規顧客の配分を月単位で比較できます。

## まとめ {#wrapup}

上記の例で、式がであることに気付きましたか `timestamp`, `groupings`, `perspectives`、および `filters` 入力指標から継承されるか の使用には数式を使用できます `perspectives` および [独立時間のオプション](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;} は、指標と同様です。

で数式を使用する方法について質問がある場合 `Report Builder`, [サポートに連絡する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
