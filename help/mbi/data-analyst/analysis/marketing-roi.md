---
title: マーケティング ROI
description: 総合的な ROI やキャンペーン別の ROI など、チャネル分析をトラッキングするダッシュボードを設定する方法を説明します。
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# マーケティング ROI

>[!NOTE]
>
>このトピックでは、元のアーキテクチャと新しいアーキテクチャを使用しているお客様向けの手順について説明します。 あなたは、 [新しいアーキテクチャ](../../administrator/account-management/new-architecture.md) メインツールバーから「Data Warehouseを管理」を選択した後で「データビュー」セクションを使用できる場合。

オンライン広告にお金を費やしている場合は、この支出に対する収益を追跡し、さらなる投資に関するデータ主導型の決定を下す必要があります。 このトピックでは、総合的な ROI やキャンペーン別の ROI など、チャネル分析を追跡するダッシュボードの設定方法について説明します。

![](../../assets/Marketing_dashboard_example.png)

使用を開始する前に、 [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md), [!DNL [Adwords]](../importing-data/integrations/google-adwords.md)、および [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) アカウントを作成し、追加のオンライン広告費用データを取り込みます。 この分析に含まれる内容 [高度な計算列](../data-warehouse-mgr/adv-calc-columns.md).

## 統合テーブル

**元のアーキテクチャ：** 様々なソースから支出を集めるために、 [!DNL Facebook Ads] または [!DNL Google Adwords]を使用する場合、Adobeは、 **連結表** のすべての広告費用。 この手順を完了するには、アナリストが必要です。 もしそうでなければ [支援要請を行う](../../guide-overview.md#Submitting-a-Support-Ticket) 問題を `[MARKETING ROI ANALYSIS]`をクリックし、アナリストがこのテーブルを作成します。

**新しいアーキテクチャ：** 次の例は、 [この分析ライブラリ](../../data-analyst/data-warehouse-mgr/create-dw-views.md) トピック。 統合テーブルは、新しいアーキテクチャのData Warehouse・ビューと呼ばれるようになりました。

## 計算列

作成する列

* **`Consolidated Digital Ad Spend`** 表
* **`Campaign name`** は、Adobeアナリストによって **[マーケティング ROI 分析]** チケット

**オリジナルおよび新しいアーキテクチャ：**

* **`sales_flat_order`** 表
   * **`Order's GA campaign`**
      * 定義を選択します。 `Joined Column`
      * [!UICONTROL Create Path]:
      * 
        [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 
        [!UICONTROL One]: `ecommerce####.transaction_id`

      * を選択します。 [!UICONTROL table]: `ecommerce####`
      * を選択します。 [!UICONTROL column]: `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`

   * **`Order's GA medium`**
      * 定義の選択：結合列
      * を選択します。 [!UICONTROL table]: `ecommerce####`
      * を選択します。 [!UICONTROL column]: `medium`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce####.transactionId

   * **`Order's GA source`**
      * 定義の選択：結合列
      * を選択します。 [!UICONTROL table]: `ecommerce####`
      * を選択します。 [!UICONTROL column]: `source`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce####.transactionId ^

* **`customer_entity`** 表
* **`Customer's first order GA campaign`**
   * 定義を選択します。 `Max`
   * を選択します。 [!UICONTROL table]: `sales_flat_order`
   * を選択します。 [!UICONTROL column]: `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * 定義を選択します。 `Max`
   * を選択します。 [!UICONTROL table]: `sales_flat_order`
   * を選択します。 [!UICONTROL column]: `Order's GA source`
   * [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * 定義を選択します。 `Max`
   * を選択します。 [!UICONTROL table]: `sales_flat_order`
   * を選択します。 [!UICONTROL column]: `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** 表
* **`Customer's first order GA campaign`**
   * 定義を選択します。 `Joined Column`
   * を選択します。 [!UICONTROL table]: `customer_entity`
   * を選択します。 [!UICONTROL column]: `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * 定義の選択：結合列
   * を選択します。 [!UICONTROL table]: `customer_entity`
   * を選択します。 [!UICONTROL column]: `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * 定義を選択します。 `Joined Column`
   * を選択します。 [!UICONTROL table]: `customer_entity`
   * を選択します。 [!UICONTROL column]: `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## 指標

* **広告費用**
* Adobe Analytics の **`Consolidated Digital Ad Spend`** 表
* この指標では **合計**
* 次の日： **`adCost`** 列
* 並べ替え元 **`date`** timestamp

* **広告インプレッション数**
* Adobe Analytics の **`Consolidated Digital Ad Spend`** 表
* この指標では **合計**
* 次の日： **`Impressions`** 列
* 並べ替え元 **`Month`** timestamp

* **広告クリック数**
* Adobe Analytics の **`Consolidated Digital Ad Spend`** 表
* この指標では **合計**
* 次の日： **`adClicks`** 列
* 並べ替え元 **`Month`** timestamp

>[!NOTE]
>
>必ず [すべての新しい列を指標のディメンションとして追加](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に。

## レポート

* **広告費用（全時間）**
   * [!UICONTROL Metric]：広告費用

* 指標 `A`：広告費用
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **広告顧客獲得（常時）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * フィルター論理式： ([`A`] または [`B`] または [`C`]) および [`D`]

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
      * フィルター論理式： ([`A`] または [`B`] または [`C`]) および [`D`]

   * [!UICONTROL Metric]：全期間の平均売上高
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * フィルター論理式： ([`A`] または [`B`] または [`C`]) および [`D`]

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

* **Ga Medium ごとの注文**
   * 
     [!UICONTROL 指標]: `Orders`

* 指標 `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 
  [!UICONTROL Chart Type]: `Area`

* **キャンペーン別広告 ROI**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * フィルター論理式： ([`A`] または [`B`] または [`C`]) および [`D`]

   * [!UICONTROL Metric]：全期間の平均売上高
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * フィルター論理式： ([`A`] または [`B`] または [`C`]) および [`D`]

   * [!UICONTROL Metric]：平均ライフタイム注文数
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * フィルター論理式： ([`A`] または [`B`] または [`C`]) および [`D`]

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
  [!UICONTROL グループ化基準]: `campaign` (非広告費用テーブル指標に対して「顧客の最初の注文」キャンペーンを使用する)
* 
  [!UICONTROL Chart Type]: `Table`

この分析の構築中に質問が発生した場合、または単に Professional Services チームを引き付けたい場合は、 [連絡先サポート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

### 関連

* [での UTM タグ付けのベストプラクティス [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [方法 [!DNL Google Analytics] UTM 属性は機能しますか？](../analysis/utm-attributes.md)
