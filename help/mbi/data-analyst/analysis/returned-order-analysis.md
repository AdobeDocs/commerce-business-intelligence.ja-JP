---
title: 返品受注の分析
description: ストアの収益を詳細に分析するダッシュボードの設定方法を説明します。
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 返品注文

このトピックでは、ストアの収益を詳細に分析するダッシュボードの設定方法を説明します。

![](../../assets/detailed-returns-dboard.png)

使用を開始する前に、 [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) お客様と、会社が以下を使用していることを確認する必要があります `enterprise\_rma` 戻り値のテーブル

この分析に含まれる内容 [高度な計算列](../data-warehouse-mgr/adv-calc-columns.md).

## はじめに

追跡する列

* **`enterprise_rma`** または **`rma`** テーブル
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`** または **`rma_item_entity`** テーブル
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

作成するフィルターセット

* **`enterprise_rma`** テーブル
* フィルターセット名： `Returns we count`
* フィルターセットのロジック：
   * プレースホルダー – ここにカスタムロジックを入力します

* **`enterprise_rma_item_entity`** テーブル
* フィルターセット名： `Returns items we count`
* フィルターセットのロジック：
   * プレースホルダー – ここにカスタムロジックを入力します

### 計算される列

作成する列

* **`enterprise_rma`** テーブル
* **`Order's created at`**
* 定義を選択： `Joined Column`
* [!UICONTROL Create Path]:
* 
  [!UICONTROL Many]: `enterprise_rma.order_id`
* 
  [!UICONTROL One]: `sales_flat_order.entity_id`

* を選択 [!UICONTROL table]: `sales_flat_order`
* を選択 [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* 定義を選択： `Joined Column`
* を選択 [!UICONTROL table]: `sales_flat_order`
* を選択 [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** は、の一部としてアナリストによって作成されます `[RETURNS ANALYSIS]` チケット

* **`enterprise_rma_item_entity`** テーブル
* **`return_date_requested`**
* 定義を選択： `Joined Column`
* [!UICONTROL Create Path]:
   * 
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * 
     [!UICONTROL One]: `enterprise_rma.entity_id`

* を選択 [!UICONTROL table]: `enterprise_rma`
* を選択 [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** は、の一部としてアナリストによって作成されます `[RETURNS ANALYSIS]` チケット

* **`sales_flat_order`** テーブル
* **`Order contains a return? (1=yes/0=No)`**
* 定義を選択： `Exists`
* を選択 [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** は、の一部としてアナリストによって作成されます `[RETURNS ANALYSIS]` チケット
* **`Customer's previous order contains return? (1=yes/0=no)`** は、の一部としてアナリストによって作成されます `[RETURNS ANALYSIS]` チケット

>[!NOTE]
>
>解決までの秒数または最初の応答までの秒数の営業時間のみを分析したい場合は、チケットを要求する際にアナリストにお知らせください。

### 指標

* **戻り値**
* が含まれる **`enterprise_rma`** テーブル
* このメトリックは、 **カウント**
* 日 **`entity_id`** 列
* による並べ替え **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **返された項目**
* が含まれる **`enterprise_rma_item_entity`** テーブル
* このメトリックは、 **合計**
* 日 **`qty_approved`** 列
* による並べ替え **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **返される項目の合計値**
* が含まれる **`enterprise_rma_item_entity`** テーブル
* このメトリックは、 **合計**
* 日 **`Returned item total value (qty_returned * price)`** 列
* による並べ替え **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **注文から返品までの平均時間**
* が含まれる **`enterprise_rma`** テーブル
* このメトリックは、 **平均**
* 日 **`Time between order's created_at and date_requested`** 列
* による並べ替え **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>必ずしてください [すべての新規列をディメンションとして指標に追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に、

### レポート

* **リターンを行った後の繰り返し注文確率**
* 指標 `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is in current month? = No`

* 指標 `B`: `Non-last orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Is customer's last order? (1=yes/0=no) = 0`
   * `Order contains a return? (1=yes/0=No) = 1`

* 数式：繰り返し注文の確率
* [!UICONTROL Formula]: `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* 
  [!UICONTROL グラフ タイプ]: `Bar`

* **返す平均時間（すべての時間）**
* 指標 `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL グラフ タイプ]: `Number`

* **返品のある注文の割合**
* 指標 `A`: `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* 指標 `B`: `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`

* 数式：返品付き注文の %
* [!UICONTROL Formula]: `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **収益（月別）**
* 指標 `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* 
  [!UICONTROL グラフ タイプ]: `Line`

* **返品したが再購入していない顧客**
* 指標 `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL Group by]: `Customer_email`
* 
  [!UICONTROL グラフ タイプ]: `Table`

* **返品率（品目別）**
* 指標 `A`: `Returned items` （Hide）
* [!UICONTROL Metric]：返された項目

* 指標 `B`: `Items sold` （Hide）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* 
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* 
  [!UICONTROL グラフ タイプ]: `Table`

すべてのレポートをコンパイルした後、必要に応じてダッシュボード上で整理できます。 結果は、上記のサンプルダッシュボードのようになります。

分析中に質問が発生した場合や、Professional Services チームに依頼したい場合、 [サポートに連絡する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
