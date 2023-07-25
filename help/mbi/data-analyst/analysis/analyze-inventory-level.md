---
title: 在庫レベルの分析
description: 在庫レベルの分析方法を説明します。
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# 在庫レベルの分析

このトピックでは、現在のインベントリに関する洞察を提供し、レガシーアーキテクチャと新しいアーキテクチャの両方でクライアントに対する手順を含むダッシュボードを設定する方法について説明します。 既存のアーキテクチャを使用している ( **[!UICONTROL Data Warehouse Views]** オプションを **[!UICONTROL Manage Data]** メニュー レガシーアーキテクチャを使用している場合は、 [新しいサポートリクエスト](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 件名 **[!UICONTROL INVENTORY ANALYSIS]** 次に、 _計算列_ 以下の手順を参照してください。

## 追跡する列：

### 手順を追跡する列

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
      * 
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * を選択します。 [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * を選択します。 [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `AGE`
      * 選択 [!UICONTROL DATETIME column]: `Product's most recent order date`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * を選択します。 [!UICONTROL column]: `qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] 入力：
         * 回答： `Product's lifetime number of items sold`
         * B: `Product's first order date`
      * 
        [!UICONTROL Datatype]: `Decimal`
      * 定義：
         * A が null または B が null の場合は、null が null の場合は、それ以外の丸 (A::decimal/(extract(epocf from (current_timestamp - B)))::decimal/604800.0),2) end

* **[!UICONTROL cataloginventory_stock_item]** テーブル：
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * を選択します。 [!UICONTROL column]: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * を選択します。 [!UICONTROL column]: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * を選択します。 [!UICONTROL column]: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * を選択します。 [!UICONTROL column]: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] 入力：
         * 回答： `qty`
         * B: `Avg products sold per week (all time)`
      * 
        [!UICONTROL Datatype]: `Decimal`
      * 定義：
         * A が null または B が null または B = 0.0 の場合は、null の場合は、それ以外の場合は round(A::decimal/B,2) の終わり

+++
+++ レガシーアーキテクチャ

* **[!UICONTROL catalog_product_entity]** テーブル：
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * を選択します。 [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * を選択します。 [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * 
        [!UICONTROL Column equation]: `AGE`
      * DATETIME 列を選択： **`Product's most recent order date`**

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * 
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * を選択します。 [!UICONTROL column]: **`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * ファイル送信時にアナリストが作成 **[在庫分析]** サポートリクエスト

* **[!UICONTROL cataloginventory_stock_item]** テーブル：
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * を選択します。 [!UICONTROL column]: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * を選択します。 [!UICONTROL column]: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * を選択します。 [!UICONTROL column]: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * 
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * を選択します。 [!UICONTROL column]: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * ファイル送信時にアナリストが作成 **[!UICONTROL INVENTORY ANALYSIS]** サポートリクエスト

+++

## 指標

### 指標の手順

* **[!UICONTROL cataloginventory_stock_item]** テーブル：
   * **`Inventory on hand`**:この指標が
      * **合計** の
      * **`qty`** 並べ替えられた列
      * [なし] 列

## レポート

### レポートの手順

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * 時間間隔： `None`
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
   * 時間間隔： `None`
   * 
     [!UICONTROL グループ化基準]: `Sku`
   * 
     [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`

   * [!UICONTROL Time period]: `All time`
   * 時間間隔： `None`
   * 
     [!UICONTROL グループ化基準]: `Sku`
   * 
     [!UICONTROL Chart type]: `Table`

この分析の構築中に質問が発生した場合、または単に Professional Services チームを引き付けたい場合、 [連絡先サポート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
