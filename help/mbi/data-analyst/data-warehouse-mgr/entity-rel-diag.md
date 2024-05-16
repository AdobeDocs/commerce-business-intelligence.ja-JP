---
title: エンティティ関係図
description: いくつかの ER 図を使用して、一般的なCommerce データベーステーブル間の関係を視覚化する方法について説明します。
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# エンティティ関係図

とは **[!UICONTROL entity relationship (ER) diagram]**? An [!UICONTROL ER] 図は、データベース内のテーブルとそれらの相互関係を視覚化したものです。 このトピックには、 [!UICONTROL ER] 一般的なAdobe Commerce データベーステーブル間の関係を視覚化するのに役立つ図。

>[!NOTE]
>
>このトピック全体を通して、次の単語が表示されます **結合**, **関係**、および **パス**. これらの単語はすべて、2 つのテーブルがどのように接続されているかを表すために使用されます。

## コアCommerce [!UICONTROL ER] 図

![4_DB_Chart](../../assets/4_DB_Chart.png)

この `ER` 図は、Commerce データベース内のコアテーブル間の関係を表します。 複数の関係を一度に表示すると、多数のテーブル間でデータがどのように関連するかを確認できます。

以下のセクションには、が含まれます `ER` 一度に 2 つのテーブルに固有の図。 ダイアグラムおよび付随する説明を表示するには、そのセクションのヘッダーをクリックします。

## `customer\_entity & sales\_flat\_order`

![1 人の顧客が多数の注文](../../assets/2_OneCustomerManyOrders.png)

1 人の顧客が多数の注文を行うことができます。 この 2 つのテーブルの関係は次のとおりです。 `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` 次と等しくない `sales\_flat\_order.entity\_id`. 1 つ目は `customer\_id` 2 つ目は `order\_id.`

内 [!DNL Commerce Intelligence]この 2 つのテーブル間のパスが存在しない場合は、次のことができます [パスの作成](../data-warehouse-mgr/create-paths-calc-columns.md) 「Data Warehouse」タブ内で設定します。 パスを作成する準備が整ったら、次のように定義します。

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

1 つの注文に多数の品目を含めることができます。 この 2 つのテーブルの関係は次のとおりです。 `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

内 [!DNL Commerce Intelligence]この 2 つのテーブル間のパスが存在しない場合は、次のことができます [パスの作成](../data-warehouse-mgr/create-paths-calc-columns.md) 「Data Warehouse」タブで、次の手順を実行します。 パスを作成する準備が整ったら、以下に示すようにパスを定義します。

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

1 つの製品は多くのアイテムを購入することができます。 この 2 つのテーブルの関係は次のとおりです。 `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

内 [!DNL Commerce Intelligence]この 2 つのテーブル間のパスが存在しない場合は、次のことができます [パスの作成](../data-warehouse-mgr/create-paths-calc-columns.md) 「Data Warehouse」タブ内で設定します。 パスを作成する準備が整ったら、以下に示すようにパスを定義します。

![](../../assets/SFOI___CPE_path.png)
