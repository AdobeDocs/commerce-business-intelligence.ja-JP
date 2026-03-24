---
title: リピート注文確率レポート
description: リピート注文確度レポートについて説明します。
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/MW9jxiwitZyjc6-woelN-FOAmvEFPCWDt01wyTOX16k
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 343
ht-degree: 0%

---

# リピート注文確率レポート

## `Incremental Event Probability` パースペクティブはいつ利用できますか？

`incremental event probability` パースペクティブは、フィルターがすべての注文に対して等しいディメンション（ユーザーの`gender`、ユーザーの`age`、ユーザーの`source`など）を使用する場合にのみ使用できます。

これは、この視点が、ユーザーの購入を示すセグメンテーションの`User's order number`というディメンション（例えば、Johnの1st、2nd、3rdの注文）に依存しているためです。

すべての注文（例：`Order's Region`）に対して等しくないディメンションを使用するフィルターを追加すると、`User's order number` ディメンションは正確ではなくなります。 これは、ユーザーの注文に番号を付ける際に、特定の地域を考慮しないためです（例えば、Johnの1st、2nd、3rdの注文は、地域に関係なく、依然として同じです）。

## 受注固有のディメンションをユーザー固有のディメンションに変換

場合によっては、`order-specific` ディメンションを`user-specific` ディメンションに変換して、`Repeat Order Probability` チャートにフィルターとして追加できます。 この場合、ユーザーの最初の注文または最新の注文のorder属性（ユーザーの最初の注文地域名など）を返します。

このような新しいディメンションを作成する場合は、[&#x200B; サポートにお問い合わせください](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

## 異なる属性を持つ注文の繰り返し確率の比較

異なる注文属性（注文の`region`など）のリピート購入数を比較するために、Adobeでは、`Users by lifetime number of orders`に似たチャートを作成することをお勧めします。 これは、1、2、3、...注文のライフタイム数を行ったユーザーの数を表示し、注文レベルのフィルターを追加します。 （言い換えれば、これは、ユーザーがある地域または別の地域で多かれ少なかれリピート購入をするかどうかを示すことができます。）

このようなグラフを構成する数値をExcelにエクスポートして、繰り返し注文確率率を計算できます。 `(x)`件の注文を行った顧客が`(x+1)`件の注文を行った可能性を確認するには、単に` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)`件の購入を行います。

### 例：

| カテゴリ | 値 |
|---|---|
| 生涯で1回の購入をした顧客の数 | `90` |
| 生涯に2回の購入をした顧客の数 | `30` |
| 生涯で3回の購入を行った顧客の数 | `10` |
| 生涯一度の購入で2回目の購入を行った顧客のリピート注文率 | `(30 + 10) / (30+10+90) = 30.77%` |
