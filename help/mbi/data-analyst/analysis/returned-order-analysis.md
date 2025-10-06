---
title: 返品受注の分析
description: ストアの収益を詳細に分析するダッシュボードの設定方法を説明します。
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# 返品注文

このトピックでは、ストアの収益を詳細に分析するダッシュボードの設定方法を説明します。

![&#x200B; 返品率と理由を示す詳細な返品ダッシュボード &#x200B;](../../assets/detailed-returns-dboard.png)

開始する前に、[Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) の顧客であり、会社が返品に `enterprise\_rma` テーブルを使用していることを確認する必要があります。

この分析には [&#x200B; 高度な計算列 &#x200B;](../data-warehouse-mgr/adv-calc-columns.md) が含まれています。

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
* フィルターセット名：`Returns we count`
* フィルターセットのロジック：
   * プレースホルダー – ここにカスタムロジックを入力します

* **`enterprise_rma_item_entity`** テーブル
* フィルターセット名：`Returns items we count`
* フィルターセットのロジック：
   * プレースホルダー – ここにカスタムロジックを入力します

### 計算される列

作成する列

* **`enterprise_rma`** テーブル
* **`Order's created at`**
* 定義を選択：`Joined Column`
* [!UICONTROL Create Path]:
* &#x200B;
  [!UICONTROL Many]: `enterprise_rma.order_id`
* &#x200B;
  [!UICONTROL One]: `sales_flat_order.entity_id`

* [!UICONTROL table] を選択：`sales_flat_order`
* [!UICONTROL column] を選択：`created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* 定義を選択：`Joined Column`
* [!UICONTROL table] を選択：`sales_flat_order`
* [!UICONTROL column] を選択：`Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** は、`[RETURNS ANALYSIS]` チケットの一部としてアナリストによって作成されます

* **`enterprise_rma_item_entity`** テーブル
* **`return_date_requested`**
* 定義を選択：`Joined Column`
* [!UICONTROL Create Path]:
   * &#x200B;
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * &#x200B;
     [!UICONTROL One]: `enterprise_rma.entity_id`

* [!UICONTROL table] を選択：`enterprise_rma`
* [!UICONTROL column] を選択：`date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** は、`[RETURNS ANALYSIS]` チケットの一部としてアナリストによって作成されます

* **`sales_flat_order`** テーブル
* **`Order contains a return? (1=yes/0=No)`**
* 定義を選択：`Exists`
* [!UICONTROL table] を選択：`enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** は、`[RETURNS ANALYSIS]` チケットの一部としてアナリストによって作成されます
* **`Customer's previous order contains return? (1=yes/0=no)`** は、`[RETURNS ANALYSIS]` チケットの一部としてアナリストによって作成されます

>[!NOTE]
>
>解決までの秒数または最初の応答までの秒数の営業時間のみを分析したい場合は、チケットを要求する際にアナリストにお知らせください。

### 指標

* **戻り値**
* **`enterprise_rma`** のテーブル内
* このメトリックは、**カウント** を実行します。
* **`entity_id`** 列
* **`date_requested`** 順
* [!UICONTROL Filter]: `Returns we count`

* **返された項目**
* **`enterprise_rma_item_entity`** のテーブル内
* このメトリックは **Sum** を実行します。
* **`qty_approved`** 列
* **`return date_requested`** 順
* [!UICONTROL Filter]: `Returns we count`

* **返された項目の合計値**
* **`enterprise_rma_item_entity`** のテーブル内
* このメトリックは **Sum** を実行します。
* **`Returned item total value (qty_returned * price)`** 列
* **`return date_requested`** 順
* [!UICONTROL Filter]: `Returns we count`

* **注文から返品までの平均時間**
* **`enterprise_rma`** のテーブル内
* この指標は **平均** を実行します
* **`Time between order's created_at and date_requested`** 列
* **`date_requested`** 順
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>新しいレポートを作成する前に、必ず [&#x200B; すべての新しい列をディメンションとして指標に追加する &#x200B;](../data-warehouse-mgr/manage-data-dimensions-metrics.md) ようにしてください。

### レポート

* **再来訪後の再来訪確率**
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
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Bar`

* **返される平均時間（すべての時間）**
* 指標 `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* &#x200B;
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
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **収益（月別）**
* 指標 `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Line`

* **返品したものの再購入していない顧客**
* 指標 `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* &#x200B;
  [!UICONTROL Group by]: `Customer_email`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Table`

* **品目別返品率**
* 指標 `A`: `Returned items` （非表示）
* [!UICONTROL Metric]：返された項目

* 指標 `B`: `Items sold` （非表示）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Table`

すべてのレポートをコンパイルした後、必要に応じてダッシュボード上で整理できます。 結果は、上記のサンプルダッシュボードのようになります。

分析中に質問が発生した場合や、プロフェッショナルサービスチームに依頼したい場合は、[&#x200B; サポートへのお問い合わせ &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)。
