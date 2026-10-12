---
title: エンティティ関係図
description: いくつかのER図について学び、一般的なCommerceデータベーステーブルの関係を視覚化するのに役立ちます。
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: 'https://experienceleague.adobe.com/pWd5aVoaq2TPkGr37cNeF8CEZ63fItwCEez61eEgGBo'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%
---
# エンティティ関係図

**[!UICONTROL entity relationship (ER) diagram]**&#x200B;とは [!UICONTROL ER]図は、データベース内のテーブルとその相互関係を視覚化したものです。 このトピックでは、いくつかの一般的なAdobe Commerce データベーステーブル間の関係を視覚化するのに役立つ、いくつかの[!UICONTROL ER]図が含まれています。

>[!NOTE]
>
>このトピック全体を通して、**join**、**relationship**、**path**&#x200B;という単語が表示されます。 これらの単語はすべて、2つのテーブルの接続方法を説明するために使用されます。

## コア Commerce [!UICONTROL ER]図

![4_DB_Chart](../../assets/4_DB_Chart.png)

この`ER`図は、Commerce データベース内のコアテーブル間の関係を表しています。 複数の関係を一度に表示すると、複数のテーブル間でデータがどのように関連付けられるかを確認できます。

以下のセクションには、一度に2つのテーブルに固有の`ER`図が含まれています。 ダイアグラムとその付随する説明を表示するには、そのセクションのヘッダーをクリックします。

## `customer\_entity & sales\_flat\_order`

![1人のお客様からの多数の注文](../../assets/2_OneCustomerManyOrders.png)

1人の顧客が多くの注文を行うことができます。 これら2つのテーブル間の関係は`customer\_entity.entity\_id = sales\_flat\_order.customer\_id`です

>[!IMPORTANT]
>
>`customer\_entity.entity\_id`が`sales\_flat\_order.entity\_id`と等しくありません。 最初は`customer\_id`と見なすことができ、2番目は`order\_id.`と見なすことができます

[!DNL Commerce Intelligence]内で、これらの2つのテーブル間のパスが存在しない場合は、「Data Warehouse」タブ内で[ パス ](../data-warehouse-mgr/create-paths-calc-columns.md)を作成できます。 パスを作成する準備ができたら、次のように定義します。

sales_flat_orderからcustomer_entity](../../assets/SFO___CE_path.png)へのパスを示す![ エンティティ関係ダイアグラム

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

1つの注文に多くの項目を含めることができます。 これら2つのテーブル間の関係は`sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`です。

[!DNL Commerce Intelligence]内で、これらの2つのテーブル間のパスが存在しない場合は、「Data Warehouse」タブで[ パス ](../data-warehouse-mgr/create-paths-calc-columns.md)を作成できます。 パスを作成する準備ができたら、以下に示すようにパスを定義します。

sales_flat_order_itemからsales_flat_order](../../assets/SFOI___SFO_path.png)へのパスを示す![ エンティティ関係ダイアグラム

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

1つの製品は多くの項目を購入することができます。 これら2つのテーブル間の関係は`catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`です。

[!DNL Commerce Intelligence]内で、これらの2つのテーブル間のパスが存在しない場合は、「Data Warehouse」タブ内で[ パス ](../data-warehouse-mgr/create-paths-calc-columns.md)を作成できます。 パスを作成する準備ができたら、以下に示すようにパスを定義します。

sales_flat_order_itemからcatalog_product_entity](../../assets/SFOI___CPE_path.png)へのパスを示す![ エンティティ関係ダイアグラム
