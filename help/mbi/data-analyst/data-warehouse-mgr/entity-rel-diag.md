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

**[!UICONTROL entity relationship (ER) diagram]** とは [!UICONTROL ER] 図は、データベース内のテーブルをビジュアライゼーションし、それらのテーブルが相互にどのように関連付けられているかを示します。 ここでは、一般的なAdobe Commerce データベーステーブル間の関係を視覚化するのに役立つ、いくつかの [!UICONTROL ER] 図を示します。

>[!NOTE]
>
>このトピック全体を通して、「**結合**」、「**関係**」、「**パス** という単語が表示されます。 これらの単語はすべて、2 つのテーブルがどのように接続されているかを表すために使用されます。

## Core Commerceの [!UICONTROL ER] 図

![4_DB_Chart](../../assets/4_DB_Chart.png)

次の `ER` 図は、Commerce データベース内のコアテーブル間の関係を表しています。 複数の関係を一度に表示すると、多数のテーブル間でデータがどのように関連するかを確認できます。

以下の節には、一度に 2 つ `ER` テーブルに固有の図が含まれます。 ダイアグラムおよび付随する説明を表示するには、そのセクションのヘッダーをクリックします。

## `customer\_entity & sales\_flat\_order`

![1 人の顧客が多数の注文を行う ](../../assets/2_OneCustomerManyOrders.png)

1 人の顧客が多数の注文を行うことができます。 この 2 つのテーブル間の関係は `customer\_entity.entity\_id = sales\_flat\_order.customer\_id` です

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` が `sales\_flat\_order.entity\_id` と等しくない。 1 つ目は `customer\_id` として、2 つ目は `order\_id.` として考えることができます

[!DNL Commerce Intelligence] 内でこれらの 2 つのテーブル間のパスが存在しない場合は、「Data Warehouse」タブ内で [ パスを作成 ](../data-warehouse-mgr/create-paths-calc-columns.md) できます。 パスを作成する準備が整ったら、次のように定義します。

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

1 つの注文に多数の品目を含めることができます。 この 2 つのテーブル間の関係は `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id` です。

[!DNL Commerce Intelligence] 内でこれらの 2 つのテーブル間のパスが存在しない場合は、「Data Warehouse」タブで [ パスを作成 ](../data-warehouse-mgr/create-paths-calc-columns.md) できます。 パスを作成する準備が整ったら、以下に示すようにパスを定義します。

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

1 つの製品は多くのアイテムを購入することができます。 この 2 つのテーブル間の関係は `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product` です。

[!DNL Commerce Intelligence] 内でこれらの 2 つのテーブル間のパスが存在しない場合は、「Data Warehouse」タブ内で [ パスを作成 ](../data-warehouse-mgr/create-paths-calc-columns.md) できます。 パスを作成する準備が整ったら、以下に示すようにパスを定義します。

![](../../assets/SFOI___CPE_path.png)
