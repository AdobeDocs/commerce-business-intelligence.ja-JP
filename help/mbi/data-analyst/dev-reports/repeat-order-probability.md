---
title: リピート注文確率レポート
description: リピート注文確率レポートについて説明します。
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# リピート注文確率レポート

## `Incremental Event Probability` パースペクティブを使用できるのはいつですか？

`incremental event probability` パースペクティブは、フィルターがすべての注文に等しいディメンション（ユーザーの `gender`、ユーザーの `age`、ユーザーの `source` など）を使用する場合にのみ使用できます。

これは、このパースペクティブが、ユーザーの購入に番号を付けるセグメント化のために `User's order number` と呼ばれるディメンションに依存しているからです（例えば、John の 1 番目、2 番目、3 番目の注文）。

すべての注文に等しくないディメンションを使用するフィルターを追加した場合（例：`Order's Region`）、`User's order number` のディメンションは正確ではなくなります。 これは、ユーザーの注文に番号を付けるときに、特定の地域が考慮されないからです（例えば、John の 1 番目、2 番目、3 番目の注文は、地域に関係なく同じままです）。

## 順序固有の寸法をユーザ固有の寸法に変換する

場合によっては、`order-specific` ディメンションを `user-specific` ディメンションに変換して、`Repeat Order Probability` グラフにフィルターとして追加できることがあります。 この場合、ユーザーの最初の注文または最新の注文の注文属性（ユーザーの最初の注文の地域名など）を返します。

このような新しいディメンションを作成する場合は、[ サポートにお問い合わせください ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)。

## 異なる属性を持つ注文の繰り返し確率の比較

異なる注文属性（注文の `region` など）の繰り返し購入の数を比較するために、Adobeでは `Users by lifetime number of orders` のようなグラフを作成することをお勧めします。 これにより、1、2、3、...の全期間の注文件数を行ったユーザー数が表示され、注文レベルのフィルターが追加されます。 （つまり、ユーザーがある地域でリピート購入を増やしているか減っているかを示すことができます）。

このようなグラフを構成する数値を excel にエクスポートして、繰り返し注文の確率を計算できます。 `(x)` の注文を行った顧客の確率を確認するには、`(x+1)` の注文、単に購入 ` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` ます。

### 例：

| カテゴリ | 値 |
|---|---|
| ライフタイムに 1 件の購入を行った顧客の数 | `90` |
| ライフタイムに 2 回購入した顧客の数 | `30` |
| ライフタイムに 3 回購入した顧客の数 | `10` |
| ライフタイム中に 1 回の購入を行い、2 回目の購入を行った顧客のリピート注文確率 | `(30 + 10) / (30+10+90) = 30.77%` |
