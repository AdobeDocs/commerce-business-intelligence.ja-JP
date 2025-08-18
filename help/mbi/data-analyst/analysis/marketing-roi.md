---
title: マーケティング ROI
description: チャネル分析（集計およびキャンペーン別の ROI など）を追跡するダッシュボードの設定方法を説明します。
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# マーケティング ROI

>[!NOTE]
>
>このトピックには、元のアーキテクチャと新しいアーキテクチャを使用しているクライアント向けの手順が含まれています。 メインツールバーから「データを管理」を選択した後に「Data Warehouseビュー」セクションが使用可能な場合は、[ 新しいアーキテクチャ ](../../administrator/account-management/new-architecture.md) になります。

オンライン広告にお金を費やしている場合は、この支出に対するリターンを追跡し、さらなる投資に関してデータに基づいた決定を下す必要があります。 このトピックでは、チャネル分析（集計およびキャンペーン別の ROI など）を追跡するダッシュボードの設定方法を説明します。

![](../../assets/Marketing_dashboard_example.png)

開始する前に、[!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md)、[!DNL [Adwords]](../importing-data/integrations/google-adwords.md)、[!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) のアカウントを接続し、追加のオンライン広告費用データを取り込みます。 この分析には [ 高度な計算列 ](../data-warehouse-mgr/adv-calc-columns.md) が含まれています。

## 統合テーブル

**オリジナルアーキテクチャ：** [!DNL Facebook Ads] や [!DNL Google Adwords] など、様々なソースからの広告支出をまとめるために、Adobeでは、すべての広告支出の **統合テーブル** を作成することをお勧めします。 この手順を完了するには、アナリストが必要です。 定義されていない場合は、件名 [ を付けて ](../../guide-overview.md#Submitting-a-Support-Ticket) サポートリクエストを提出 `[MARKETING ROI ANALYSIS]` し、アナリストがこのテーブルを作成します。

**新しいアーキテクチャ：** この分析ライブラリ [ のトピックの例に従うこ ](../../data-analyst/data-warehouse-mgr/create-dw-views.md) ができます。 統合テーブルは、新しいアーキテクチャではData Warehouse ビューと呼ばれるようになりました。

## 計算される列

作成する列

* **`Consolidated Digital Ad Spend`** テーブル
* **`Campaign name`** は、Adobe アナリストが **[マーケティング ROI 分析]** チケットの一部として作成します

**オリジナルおよび新しいアーキテクチャ：**

* **`sales_flat_order`** テーブル
   * **`Order's GA campaign`**
      * 定義を選択：`Joined Column`
      * [!UICONTROL Create Path]:
      * 
        [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 
        [!UICONTROL One]: `ecommerce####.transaction_id`

      * [!UICONTROL table] を選択：`ecommerce####`
      * [!UICONTROL column] を選択：`campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`

   * **`Order's GA medium`**
      * 定義を選択：結合列
      * [!UICONTROL table] を選択：`ecommerce####`
      * [!UICONTROL column] を選択：`medium`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce####.transactionId

   * **`Order's GA source`**
      * 定義を選択：結合列
      * [!UICONTROL table] を選択：`ecommerce####`
      * [!UICONTROL column] を選択：`source`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce####.transactionId
^

* **`customer_entity`** テーブル
* **`Customer's first order GA campaign`**
   * 定義を選択：`Max`
   * [!UICONTROL table] を選択：`sales_flat_order`
   * [!UICONTROL column] を選択：`Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * 定義を選択：`Max`
   * [!UICONTROL table] を選択：`sales_flat_order`
   * [!UICONTROL column] を選択：`Order's GA source`
   * [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * 定義を選択：`Max`
   * [!UICONTROL table] を選択：`sales_flat_order`
   * [!UICONTROL column] を選択：`Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** テーブル
* **`Customer's first order GA campaign`**
   * 定義を選択：`Joined Column`
   * [!UICONTROL table] を選択：`customer_entity`
   * [!UICONTROL column] を選択：`Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * 定義を選択：結合列
   * [!UICONTROL table] を選択：`customer_entity`
   * [!UICONTROL column] を選択：`Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * 定義を選択：`Joined Column`
   * [!UICONTROL table] を選択：`customer_entity`
   * [!UICONTROL column] を選択：`Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## 指標

* **広告費用**
* **`Consolidated Digital Ad Spend`** のテーブル内
* このメトリックは **Sum** を実行します。
* **`adCost`** 列
* **`date`** タイムスタンプで並べ替え

* **広告インプレッション**
* **`Consolidated Digital Ad Spend`** のテーブル内
* このメトリックは **Sum** を実行します。
* **`Impressions`** 列
* **`Month`** タイムスタンプで並べ替え

* **広告クリック数**
* **`Consolidated Digital Ad Spend`** のテーブル内
* このメトリックは **Sum** を実行します。
* **`adClicks`** 列
* **`Month`** タイムスタンプで並べ替え

>[!NOTE]
>
>新しいレポートを作成する前に、必ず [ すべての新しい列をディメンションとして指標に追加する ](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) ようにしてください。

## レポート

* **広告費用（すべての時間）**
   * [!UICONTROL Metric]：広告費用

* 指標 `A`：広告費用
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **広告顧客の獲得（常時）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * フィルターロジック：（[`A`] または [`B`] または [`C`]）および [`D`]

* 指標 `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **広告 ROI**
   * [!UICONTROL Metric]：広告費用

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * フィルターロジック：（[`A`] または [`B`] または [`C`]）および [`D`]

   * [!UICONTROL Metric]：平均生涯売上高
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * フィルターロジック：（[`A`] または [`B`] または [`C`]）および [`D`]

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 
     [!UICONTROL Format]: `Percentage`

* 指標 `A`: `Ad Spend (hide)`
* 指標 `B`: `Ad customer acquisitions (hide)`
* 指標 `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **ga メディア別のオーダー数**
   * 
     [!UICONTROL 指標]: `Orders`

* 指標 `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 
  [!UICONTROL Chart Type]: `Area`

* **キャンペーン別の広告 ROI**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * フィルターロジック：（[`A`] または [`B`] または [`C`]）および [`D`]

   * [!UICONTROL Metric]：平均生涯売上高
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * フィルターロジック：（[`A`] または [`B`] または [`C`]）および [`D`]

   * [!UICONTROL Metric]：注文の平均ライフタイム数
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * フィルターロジック：（[`A`] または [`B`] または [`C`]）および [`D`]

   * [!UICONTROL Formula]: `(A / B)`
   * 
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * 
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * 
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * 
     [!UICONTROL Format]: `Currency`

* 指標 `A`: `Ad Spend` （非表示）
* 指標 `B`: `Ad customer acquisitions`
* 指標 `C`: `Average LTV`
* 指標 `D`: `Average lifetime # of orders`
* 
  [!UICONTROL 数式]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* 指標 `H`: `adClicks`
* 指標 `I`: `Impressions`
* 
  [!UICONTROL 数式]: `CTR`
* 
  [!UICONTROL 数式]: `CPC`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL Group by]: `campaign` (広告以外の費用テーブル指標に対する「顧客の最初の注文」キャンペーンの使用)
* 
  [!UICONTROL Chart Type]: `Table`

分析中に質問が発生した場合や、プロフェッショナルサービスチームに依頼したい場合は、[ サポートにお問い合わせください ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

### 関連

* [ [!DNL Google Analytics] の UTM タグ付けのベストプラクティス](../../best-practices/utm-tagging-google.md)
* [ [!DNL Google Analytics] UTM アトリビューションの仕組み](../analysis/utm-attributes.md)
