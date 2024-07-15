---
title: ゲストによる注文
description: ゲストによる注文がデータに与える影響と、 [!DNL Commerce Intelligence] Data Warehouseのゲストによる注文を適切に考慮する必要があるオプションについて説明します。
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---

# ゲストによる注文

注文を確認しているときに、多くの `customer\_id` 値が null であるか、`customers` テーブルに結合する値がないことに気付いた場合、これは店舗がゲストの注文を許可していることを示しています。 つまり、`customers` テーブルには、すべての顧客が含まれる可能性は低くなります。

このトピックでは、データに対するゲスト注文の影響と、[!DNL Commerce Intelligence]Data Warehouseでのゲスト注文を適切に考慮する必要があるオプションについて説明します。

## ゲストの注文がデータに与える影響

通常のコマースデータベースには、`customers` テーブルに結合する `orders` テーブルがあります。 `orders` テーブルの各行には、`customers` テーブルの 1 つの行に固有の `customer\_id` 列があります。

* **すべての顧客が登録され** ゲストによる注文が許可されていない場合、`orders` テーブルのすべてのレコードの `customer\_id` 列に値が入っていることを意味します。 その結果、すべての注文が `customers` テーブルに結合されます。

  ![](../../assets/guest-orders-4.png)

* **ゲストによる注文が許可されている場合**、一部の注文の `customer\_id` 列に値が含まれていません。 登録済みの顧客にのみ、`orders` テーブルの `customer\_id` 列の値が提供されます。 登録されていないお客様には、この列の `NULL` 値（または空白）が表示されます。 その結果、すべての注文レコードが `customers` テーブル内に一致するレコードを持つわけではありません。

  >[!NOTE]
  >
  >注文を行った一意の個人を識別するには、注文に関連付けられた `customer\_id` の横に、別の一意のユーザー属性が必要です。 通常、顧客のメールアドレスが使用されます。

## Data Warehouse設定でのゲスト注文のアカウント設定方法

通常、お客様のアカウントを導入するセールス・エンジニアは、Data Warehouseの基盤を構築する際にゲストのオーダーを考慮に入れます。

ゲストの注文を考慮する最も最適な方法は、すべての顧客レベルの指標を `orders` テーブルに基づくことです。 この設定では、ゲストを含むすべての顧客が持つ一意の顧客 ID を使用します（通常は顧客のメールが使用されます）。 この場合、`customers` テーブルの登録データは無視されます。 このオプションを使用すると、1 つ以上の購入を行った顧客のみが顧客レベルのレポートに含まれます。 1 回購入していない登録ユーザーは含まれません。 このオプションを使用すると、`New customer` 指標は、`orders` のテーブルでの顧客の最初の注文日に基づきます。

このタイプの設定で設定された `Customers we count` フィルターには、`Customer's order number = 1` 用のフィルターがあることがわかります。

![](../../assets/guest-orders-filter-set.png)

ゲストからの注文がない場合、各顧客は顧客テーブル内に一意の行として存在します（画像 1 を参照）。 `New customers` などの指標は、単純に登録日に基づいてこのテーブルの ID をカウント `created\_at`、登録日に基づいて新規顧客を把握できます。

ゲスト注文の場合、すべての顧客指標が `orders` テーブルに基づいてゲスト注文を考慮するように設定するには、自分が `not counting customers twice` っていることを確認する必要があります。 注文テーブルの ID をカウントすると、すべての注文がカウントされます。 代わりに、`orders` テーブルの ID をカウントしてフィルター、`Customer's order number = 1` を使用する場合、一意の各顧客 `only one time` をカウントすることになります。 これは、`Customer's lifetime revenue` や `Customer's lifetime number of orders` など、すべての顧客レベルの指標に適用できます。

上記のように、`orders` テーブルに null`customer\_ids` が含まれています。 `customer\_email` を使用して一意の顧客を識別すると、`erin@test.com` が 3 件の注文を行ったことがわかります。 したがって、次の条件に基づいて、`orders` テーブルに `New customers` しい指標を作成できます。

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
