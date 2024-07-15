---
title: 在庫レベルの分析
description: 在庫レベルの分析方法を説明します。
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# 在庫レベルの分析

このトピックでは、現在のインベントリに関するインサイトを提供し、レガシーアーキテクチャと新しいアーキテクチャの両方についてクライアントに対する手順を含むダッシュボードを設定する方法について説明します。 **[!UICONTROL Manage Data]** メニューの **[!UICONTROL Data Warehouse Views]** オプションがない場合は、従来のアーキテクチャを使用します。 レガシーアーキテクチャを使用している場合は、以下の [ 計算列 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 手順で指定されたセクションに到達したら、件名 **[!UICONTROL INVENTORY ANALYSIS]** の _新規サポートリクエスト_ を送信します。

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

## 計算される列：

+++ 新しいアーキテクチャ

* **[!UICONTROL catalog_product_entity]** テーブル：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] を選択：`created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] を選択：`created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `AGE`
      * [!UICONTROL DATETIME column] を選択：`Product's most recent order date`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] を選択：`qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] 入力：
         * A: `Product's lifetime number of items sold`
         * B: `Product's first order date`
      * 
        [!UICONTROL Datatype]: `Decimal`
      * 定義：
         * a が null または B が null の場合は null で、それ以外の場合は round （A::decimal/（extract （epoch from （current_timestamp - B））::decimal/604800.0）,2） end

* **[!UICONTROL cataloginventory_stock_item]** テーブル：
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] を選択：`sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] を選択：`Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] を選択：`Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] を選択：`Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] 入力：
         * A: `qty`
         * B: `Avg products sold per week (all time)`
      * 
        [!UICONTROL Datatype]: `Decimal`
      * 定義：
         * a が null または B が null または B = 0.0 の場合、null または round （A::decimal/B,2）終了

+++
+++ レガシーアーキテクチャ

* **[!UICONTROL catalog_product_entity]** テーブル：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] を選択：`created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] を選択：`created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `AGE`
      * DATETIME 列の選択：**`Product's most recent order date`**

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * [!UICONTROL column] を選択：**`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * **[在庫分析]** サポート要求を提出する際に、アナリストによって作成されます

* **[!UICONTROL cataloginventory_stock_item]** テーブル：
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] を選択：`sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] を選択：`Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] を選択：`Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * [!UICONTROL column] を選択：`Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * **[!UICONTROL INVENTORY ANALYSIS]** サポートのリクエストを送信する際にアナリストによって作成されます

+++

## 指標

### 指標の手順

* **[!UICONTROL cataloginventory_stock_item]** テーブル：
   * **`Inventory on hand`**：このメトリックは、
      * **合計**
      * **`qty`** 順に並べ替えられた列
      * [ なし ] 列

## レポート

### レポートの手順

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * 時間間隔：`None`
   * [!UICONTROL Group by]:
      * `Sku`
      * `Weeks on hand`
   * 
     [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `< 2`

   * [!UICONTROL Time period]: `All time`
   * 時間間隔：`None`
   * 
     [!UICONTROL Group by]: `Sku`
   * 
     [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`

   * [!UICONTROL Time period]: `All time`
   * 時間間隔：`None`
   * 
     [!UICONTROL Group by]: `Sku`
   * 
     [!UICONTROL Chart type]: `Table`

分析中に質問が発生した場合や、プロフェッショナルサービスチームに依頼したい場合は、[ サポートにお問い合わせください ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
