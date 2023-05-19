---
title: 繰り返し注文の確率レポート
description: 繰り返し注文の確率レポートの詳細と理解。
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# 繰り返し注文の確率レポート

## が `Incremental Event Probability` パースペクティブを利用できますか？

この `incremental event probability` パースペクティブは、フィルターがすべての注文 ( ユーザーの `gender`、ユーザーの `age` またはユーザーの `source`) をクリックします。

これは、このパースペクティブが「 」と呼ばれるディメンションに依存するためです `User's order number` セグメントの場合。これは、ユーザーの購入数（ジョンの 1 回目、2 回目、3 回目の注文など）を表します。

すべての注文に対して等しくないディメンション ( 例： `Order's Region`)、 `User's order number` ディメンションの正確性は失われます。 これは、ユーザーの注文に番号を付ける際に、特定の地域を考慮しないためです（例えば、John の 1 番目、2 番目、3 番目の注文は、その地域に関係なく、まだ同じです）。

## 注文固有のディメンションをユーザー固有のディメンションに変換する

場合によっては、 `order-specific` 次元を `user-specific` フィルターとして追加するディメンション `Repeat Order Probability` グラフ。 この場合、ユーザーの最初の注文または最新の注文の注文属性（ユーザーの最初の注文地域名など）を返します。

このような新しいディメンションを作成する場合は、 [連絡先サポート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## 異なる属性の注文の繰り返し確率の比較

異なる注文属性 ( 注文の `region`) を使用する場合、Adobeでは、 `Users by lifetime number of orders`. これにより、全期間で 1、2、3、...の注文数を達成したユーザーの数が表示され、注文レベルのフィルターが追加されます。 （つまり、ユーザーが 1 つの地域でリピート購入を行うかどうかを示すことができます）。

その後、このようなグラフを構成する数値を Excel にエクスポートして、繰り返し注文の確率を計算できます。 顧客が `(x)` 命令 `(x+1)` 注文、単に` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` 購入。

### 例：

| カテゴリ | 値 |
|---|---|
| 生涯に 1 回購入した顧客の数 | `90` |
| 全期間に 2 回購入した顧客の数 | `30` |
| 全期間に 3 回購入した顧客の数 | `10` |
| 生涯に 1 回購入して 2 回目の購入をおこなった顧客のリピート注文確率 | `(30 + 10) / (30+10+90) = 30.77%` |
