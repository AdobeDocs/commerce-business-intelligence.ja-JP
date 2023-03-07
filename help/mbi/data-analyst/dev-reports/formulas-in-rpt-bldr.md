---
title: Report Builder内の数式
description: 数式をReport Builderで使用する方法を説明します。
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# 内の数式 `Report Builder`

内 [`Report Builder`](../../tutorials/using-visual-report-builder.md)を使用すると、 [定義済み指標](../../data-user/reports/ess-manage-data-metrics.md) 」と入力します。 これらの指標を数式で組み合わせると、データから追加のインサイトを収集できます。 この記事では、 `Report Builder`  — 飛び込みましょう！

## とは `formula`? {#what}

内 `Report Builder`, a `formula` は、数学的論理に基づく 1 つ以上の指標の組み合わせに過ぎません。 典型的な例を次に示します。

![](../../assets/formula-example.png)

この例では、 `Number of orders metric (A)` および `Distinct buyers metric (B)`目標は次の質問に答えることです。購入者が毎月行っている注文の平均数はどれくらいですか？ 式のパラメーターは次のとおりです。

* `Definition`:ここでは、入力指標に数学を適用します。 この例では、注文件数を個別購入者数で割った値が、平均注文数を示しています。 したがって、定義は (A/B) です。

* `Format`:数値、期間、または通貨額を返す数式を指定します。 数式の定義の横にはドロップダウンが表示され、このドロップダウンを使用して戻り値の形式を指定できます。 この場合、数値です。

* `Miscellaneous`:数式のタイムスタンプ、グループ化、パースペクティブおよびフィルターは、すべて入力指標に継承されます。 ここには何もすることがありません！

## 使用方法 `formulas` 」と表示されます。 {#how}

基本を説明したので、いくつか例を見てみましょう。

### 例：初回の注文に対する売上高の割合を調べたいと思います。

![数式を使用して、初回注文に関連する売上高の割合を検索する](../../assets/first_time_orders.gif)

この例では、 `Revenue` および `Revenue (first time orders)` 指標。 を `Revenue (first time orders)(B)` 指標 `Revenue metric (A)` 戻りフォーマットを `Percent`を使用すると、初回注文に関連付けることができる売上高の割合を検索できます。

### 例：注文あたりの平均売上高を知りたいが、オファーを実行せず、 `promo code`.

![式を使用した、プロモコードの有無に関わらず、注文あたりの平均売上高の検索](../../assets/promo_code.gif)

この例では、 `Revenue` および `Number of orders` 指標。 この質問に対する答えは、2 つの手順（分割）で構成されます。 `Revenue (A)` を `Number of orders (B)` 戻りフォーマットを `Currency`. 次に、数式の結果 (`Avg. Revenue per order`) をクリックして、結果を表示およびグループ化します。 `Promo code`.

### 例：新規顧客の UTM ソースの分布を知りたい。

![数式を使用した新規顧客の UTM ソースの分布の検索](../../assets/distro.gif)

この質問に対する回答を見つけるには、いくつかの手順が必要です。

1. まず、 `New Customers` 指標を選択し、 `utm_source - all`. これは指標です `A`または `New Customers (grouped)`.

1. 次に、 `New Customers (grouped)` 指標を追加し、独立したディメンションを使用するように設定します。 指標 `B` - `New customers (ungrouped)`  — 新規顧客の合計数を表示します。

1. 両方の指標を非表示にした後、数式の定義を `A/B`. これにより、 `New customers (grouped)` を `New Customers (ungrouped)`.

1. 次に、結果のフォーマットを `Percent`.

この例では、 `Stacked Columns` 月別に結果を表示するパースペクティブ。 これにより、新規顧客の分布を月単位で比較できます。

## 折り返し {#wrapup}

上記の例で、数式の `timestamp`, `groupings`, `perspectives`、および `filters` は、入力指標から継承されますか。 数式は `perspectives` および [独立時間オプション](../../tutorials/time-options-visual-rpt-bldr.md){:target=&quot;_blank&quot;} は、指標と同様です。

また、 `Report Builder`, [連絡先サポート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
