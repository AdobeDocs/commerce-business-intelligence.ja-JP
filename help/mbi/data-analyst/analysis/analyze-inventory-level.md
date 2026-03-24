---
title: 在庫レベルの分析
description: 在庫レベルの分析方法。
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
role: Admin, Developer, User
feature: Dashboards, Reports
TQID: https://experienceleague.adobe.com/z2NS33cMO3wETk6FFyI-rkbPkWxxw2zYxUUjdC4zRa4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 0%

---

# 在庫レベルの分析

このトピックでは、現在のインベントリに関するインサイトを提供し、従来のアーキテクチャと新しいアーキテクチャの両方に関するクライアントの手順を含むダッシュボードを設定する方法を説明します。 **[!UICONTROL Data Warehouse Views]** メニューの&#x200B;**[!UICONTROL Manage Data]** オプションがない場合は、レガシーアーキテクチャを使用しています。 従来のアーキテクチャを使用している場合は、以下の[計算列](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)の手順で指定されたセクションに到達したら、件名&#x200B;**[!UICONTROL INVENTORY ANALYSIS]**&#x200B;を付けて&#x200B;_新しいサポートリクエスト_&#x200B;を送信します。

## 追跡する列：

### 指示を追跡する列

* **[!UICONTROL cataloginventory_stock_item]** テーブル：
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]** テーブル：
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## 計算列：

+++ 新しいアーキテクチャ

* **[!UICONTROL catalog_product_entity]** テーブル：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column]を選択：`created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column]を選択：`created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `AGE`
      * [!UICONTROL DATETIME column]を選択：`Product's most recent order date`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column]を選択：`qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column]入力：
         * A: `Product's lifetime number of items sold`
         * B: `Product's first order date`
      * &#x200B;
        [!UICONTROL Datatype]: `Decimal`
      * 定義：
         * aがnullまたはBがnullの場合、その後null else round （A::decimal/（extract （epoch from （current_timestamp - B）））::decimal/604800.0）,2）終了

* **[!UICONTROL cataloginventory_stock_item]** テーブル：
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column]を選択：`sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column]を選択：`Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column]を選択：`Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column]を選択：`Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column]入力：
         * A: `qty`
         * B: `Avg products sold per week (all time)`
      * &#x200B;
        [!UICONTROL Datatype]: `Decimal`
      * 定義：
         * aがnullまたはBがnullまたはB = 0.0の場合、その後null else round （A::decimal/B,2）終了

+++
+++ レガシーアーキテクチャ

* **[!UICONTROL catalog_product_entity]** テーブル：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column]を選択：`created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column]を選択：`created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `AGE`
      * DATETIME列を選択：**`Product's most recent order date`**

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * [!UICONTROL column]を選択：**`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * **[INVENTORY ANALYSIS]** サポートリクエストを提出するときにアナリストによって作成されました

* **[!UICONTROL cataloginventory_stock_item]** テーブル：
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column]を選択：`sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column]を選択：`Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column]を選択：`Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column]を選択：`Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * **[!UICONTROL INVENTORY ANALYSIS]** サポートリクエストの送信時にアナリストによって作成されました

+++

## 指標

### 指標の手順

* **[!UICONTROL cataloginventory_stock_item]** テーブル：
   * **`Inventory on hand`**：この指標は、次の操作を実行します。
      * **合計**
      * **`qty`**&#x200B;列が次によって注文されました
      * [なし]列

## レポート

### レポートの手順

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * 時間間隔：`None`
   * [!UICONTROL Group by]:
      * `Sku`
      * `Weeks on hand`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `< 2`

   * [!UICONTROL Time period]: `All time`
   * 時間間隔：`None`
   * &#x200B;
     [!UICONTROL グループ化：]: `Sku`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`

   * [!UICONTROL Time period]: `All time`
   * 時間間隔：`None`
   * &#x200B;
     [!UICONTROL グループ化：]: `Sku`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

この分析の構築中に質問が発生した場合、または単にプロフェッショナルサービスチームに連絡したい場合は、[&#x200B; サポートにお問い合わせください](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
