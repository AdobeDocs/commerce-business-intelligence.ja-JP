---
title: エンティティ関係図
description: いくつかの一般的な Commerce データベーステーブル間の関係を視覚化するのに役立つ、いくつかの ER 図について説明します。
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---

# エンティティ関係図

とは **[!UICONTROL entity relationship (ER) diagram]**? An [!UICONTROL ER] ダイアグラムとは、データベース内のテーブルと、それらの関係を視覚化したものです。 このトピックには、 [!UICONTROL ER] 図を使用すると、いくつかの一般的なAdobe Commerceデータベーステーブル間の関係を視覚化できます。

>[!NOTE]
>
>このトピック全体で、次の単語が表示されます。 **join**, **関係**、および **パス**. これらの単語は、2 つのテーブルの接続方法を表すのに使用されます。

## コアコマース [!UICONTROL ER] 図

![4_DB_Chart](../../assets/4_DB_Chart.png)

この `ER` この図は、Commerce データベース内のコアテーブル間の関係を表しています。 複数の関係を一度に表示すると、多数のテーブル間でのデータの関連付けを確認できます。

以下の節では、 `ER` 一度に 2 つのテーブルに固有の図。 図とそれに伴う説明を表示するには、そのセクションのヘッダーをクリックします。

## `customer\_entity & sales\_flat\_order`

![1 件のお客様の多数の注文](../../assets/2_OneCustomerManyOrders.png)

1 人の顧客が多くの注文をすることができます。 この 2 つのテーブル間の関係は、 `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` 次と等しくない `sales\_flat\_order.entity\_id`. 1 つ目は、 `customer\_id` そして二番目は `order\_id.`

Within [!DNL Commerce Intelligence]で指定した 2 つのテーブル間のパスが存在しない場合は、 [パスを作成](../data-warehouse-mgr/create-paths-calc-columns.md) を「Data Warehouse」タブ内に入力します。 パスを作成する準備が整ったら、次のように定義します。

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

1 つの注文に多数の項目を含めることができます。 この 2 つのテーブル間の関係は、 `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

Within [!DNL Commerce Intelligence]で指定した 2 つのテーブル間のパスが存在しない場合は、 [パスを作成](../data-warehouse-mgr/create-paths-calc-columns.md) (「Data Warehouse」タブ )。 パスを作成する準備が整ったら、次に示すようにパスを定義します。

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

1 つの商品は多くの商品を購入できます。 この 2 つのテーブル間の関係は、 `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

Within [!DNL Commerce Intelligence]で指定した 2 つのテーブル間のパスが存在しない場合は、 [パスを作成](../data-warehouse-mgr/create-paths-calc-columns.md) を「Data Warehouse」タブ内に入力します。 パスを作成する準備が整ったら、次に示すようにパスを定義します。

![](../../assets/SFOI___CPE_path.png)
