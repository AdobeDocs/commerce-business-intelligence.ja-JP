---
title: ゲストによる注文
description: データに対するゲスト注文の影響と、ゲスト注文を適切に考慮する必要があるオプションについて説明します [!DNL Commerce Intelligence] Data Warehouse。
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# ゲストによる注文

注文を確認する際に、多くの `customer\_id` 値が null であるか、に結合する値がありません `customers` 表。これは、ストアがゲストによる注文を許可していることを示します。 これはを意味します `customers` テーブルには、すべての顧客が含まれているとは限りません。

このトピックでは、ゲスト注文がデータに与える影響と、ゲスト注文について適切に考慮する必要があるオプションについて説明します [!DNL Commerce Intelligence] Data Warehouse。

## ゲストの注文がデータに与える影響

通常のコマースデータベースには、 `orders` に結合するテーブル `customers` テーブル。 のすべての行 `orders` テーブルに `customer\_id` 上の 1 行に固有の列 `customers` テーブル。

* **すべての顧客が登録されている場合** また、ゲストによる注文は許可されません。これは、 `orders` テーブルには、に値があります `customer\_id` 列。 その結果、すべての注文がに戻されます `customers` テーブル。

  ![](../../assets/guest-orders-4.png)

* **ゲストによる注文が許可されている場合**。これは、一部の注文ののフィールドに値が含まれていないことを意味します `customer\_id` 列。 登録済みの顧客にのみ、の値が指定されます `customer\_id` の列 `orders` テーブル。 登録されていないお客様は、 `NULL` （または空白）この列の値。 その結果、すべての注文レコードがに一致するレコードを持つわけではありません `customers` テーブル。

  >[!NOTE]
  >
  >注文を行った一意の個人を識別するには、の横に別の一意のユーザー属性が必要です `customer\_id` 注文に添付します。 通常、顧客のメールアドレスが使用されます。

## Data Warehouse設定でのゲスト注文のアカウント設定方法

通常、お客様のアカウントを導入するセールス・エンジニアは、Data Warehouseの基盤を構築する際にゲストのオーダーを考慮に入れます。

ゲストからの注文を考慮する最も最適な方法は、すべての顧客レベルの指標を `orders` テーブル。 この設定では、ゲストを含むすべての顧客が持つ一意の顧客 ID を使用します（通常は顧客のメールが使用されます）。 この場合、からの登録データは無視されます `customers` テーブル。 このオプションを使用すると、1 つ以上の購入を行った顧客のみが顧客レベルのレポートに含まれます。 1 回購入していない登録ユーザーは含まれません。 このオプションを使用すると、 `New customer` 指標は、顧客の内の最初の注文日に基づいています `orders` テーブル。

次のことに気付くかもしれません `Customers we count` このタイプの設定で設定されたフィルターには、次のフィルターがあります `Customer's order number = 1`.

![](../../assets/guest-orders-filter-set.png)

ゲストからの注文がない場合、各顧客は顧客テーブル内に一意の行として存在します（画像 1 を参照）。 などの指標 `New customers` に基づいてこのテーブルの id をカウントするだけです `created\_at` 登録日に基づいて新規顧客を把握する日付。

ゲスト注文の設定で、すべての顧客指標が次に基づく `orders` ゲストからの注文を考慮したテーブル。次の点を確認する必要があります `not counting customers twice`. 注文テーブルの ID をカウントすると、すべての注文がカウントされます。 代わりに、の ID をカウントする場合 `orders` テーブルとフィルターの使用 `Customer's order number = 1`次に、一意の各顧客をカウントします `only one time`. 次のようなすべての顧客レベルの指標に適用できます `Customer's lifetime revenue` または `Customer's lifetime number of orders`.

null があることがわかります `customer\_ids` が含まれる `orders` テーブル。 使用する場合 `customer\_email` 一意の顧客を識別する方法は、次のとおりです `erin@test.com` は 3 回注文しました。 したがって、以下を構築できます `New customers` に関する指標 `orders` 以下の条件に基づいたテーブル：

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
