---
title: マーケティング ROI
description: チャネル分析を追跡するダッシュボードの設定方法（集計およびキャンペーン別のROIを含む）について説明します。
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
TQID: https://experienceleague.adobe.com/TJ0KsU551M5PkQcY-Ic0PuExtC9SCkO0MhZGdHL4N6g
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 02934da4962380494ab8a2becf5f06efb15d84dc
workflow-type: tm+mt
source-wordcount: 691
ht-degree: 21%

---

# マーケティング ROI

>[!NOTE]
>
>このトピックには、元のアーキテクチャと新しいアーキテクチャを使用しているクライアントの手順が含まれています。 メインツールバーから「データの管理」を選択した後に「Data Warehouse ビュー」セクションを使用できる場合は、[新しいアーキテクチャ &#x200B;](../../administrator/account-management/new-architecture.md)に移行しています。

オンライン広告に予算を費やしている場合は、この支出のリターンを追跡し、さらなる投資に関してデータ主導の意思決定をおこないます。 このトピックでは、チャネル分析を追跡するダッシュボードを設定する方法（集計およびキャンペーン別のROIを含む）について説明します。

ROI指標とキャンペーンのパフォーマンスを示す![&#x200B; マーケティングダッシュボード &#x200B;](../../assets/Marketing_dashboard_example.png)

開始する前に、[[!DNL [Facebook Ads]]](../importing-data/integrations/facebook-ads.md)、[[!DNL [Adwords]]](../importing-data/integrations/google-adwords.md)、[[!DNL [Google Ecommerce]]](../importing-data/integrations/google-ecommerce.md) アカウントを接続し、追加のオンライン広告費データを取り込む必要があります。 この分析には、[高度な計算列](../data-warehouse-mgr/adv-calc-columns.md)が含まれています。

## 統合テーブル

**元のアーキテクチャ：** [!DNL Facebook Ads]や[!DNL Google Adwords]など、様々なソースからの支出をまとめるために、Adobeでは、すべての広告支出の&#x200B;**統合テーブル**&#x200B;を作成することをお勧めします。 このステップを完了するにはアナリストが必要です。 まだ使用していない場合は、[件名`[MARKETING ROI ANALYSIS]`でサポートリクエスト &#x200B;](../../guide-overview.md#Submitting-a-Support-Ticket)を提出し、アナリストがこのテーブルを作成します。

**新しいアーキテクチャ：** [このAnalysis Library](../../data-analyst/data-warehouse-mgr/create-dw-views.md)のトピックの例に従うことができます。 統合テーブルは、新しいアーキテクチャではData Warehouse ビューと呼ばれるようになりました。

## 予定列

作成する列

* **`Consolidated Digital Ad Spend`** テーブル
* **`Campaign name`**&#x200B;は、**[MARKETING ROI ANALYSIS]** チケットの一部として、Adobe アナリストによって作成されました

**元のアーキテクチャと新しいアーキテクチャ：**

* **`sales_flat_order`** テーブル
  * **`Order's GA campaign`**
    * 定義を選択：`Joined Column`
    * [!UICONTROL Create Path]:
    * &#x200B;
      [!UICONTROL Many]&#x200B;: `sales_flat_order.increment_id`
    * &#x200B;
      [!UICONTROL One]&#x200B;: `ecommerce####.transaction_id`

    * [!UICONTROL table]を選択：`ecommerce####`
    * [!UICONTROL column]を選択：`campaign`
    * [!UICONTROL Path]&#x200B;: `sales_flat_order.increment_id = ecommerce#####.transactionID`

  * **`Order's GA medium`**
    * 定義を選択：連結された列
    * [!UICONTROL table]を選択：`ecommerce####`
    * [!UICONTROL column]を選択：`medium`
    * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce#####.transactionId

  * **`Order's GA source`**
    * 定義を選択：連結された列
    * [!UICONTROL table]を選択：`ecommerce####`
    * [!UICONTROL column]を選択：`source`
    * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce#####.transactionId
^

* **`customer_entity`** テーブル
* **`Customer's first order GA campaign`**
  * 定義を選択：`Max`
  * [!UICONTROL table]を選択：`sales_flat_order`
  * [!UICONTROL column]を選択：`Order's GA campaign`
  * [!UICONTROL Path]&#x200B;: `sales_flat_order.customer_id = customer_entity.entity_id`
  * [!UICONTROL Filter]:
    * `Orders we count`
    * `Customer's order number = 1`

* **`Customer's first order GA source`**
  * 定義を選択：`Max`
  * [!UICONTROL table]を選択：`sales_flat_order`
  * [!UICONTROL column]を選択：`Order's GA source`
  * [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
  * [!UICONTROL Filter]:
    * `Orders we count`
    * `Customer's order number = 1`

* **`Customer's first order GA medium`**
  * 定義を選択：`Max`
  * [!UICONTROL table]を選択：`sales_flat_order`
  * [!UICONTROL column]を選択：`Order's GA medium`
  * [!UICONTROL Path]&#x200B;: `sales_flat_order.customer_id = customer_entity.entity_id`
  * [!UICONTROL Filter]:
    * `Orders we count`
    * `Customer's order number = 1`

* **`sales_flat_order`** テーブル
* **`Customer's first order GA campaign`**
  * 定義を選択：`Joined Column`
  * [!UICONTROL table]を選択：`customer_entity`
  * [!UICONTROL column]を選択：`Customer's first order GA campaign`
  * [!UICONTROL Path]&#x200B;: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
  * 定義を選択：連結された列
  * [!UICONTROL table]を選択：`customer_entity`
  * [!UICONTROL column]を選択：`Customer's first order GA source`
  * [!UICONTROL Path]&#x200B;: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
  * 定義を選択：`Joined Column`
  * [!UICONTROL table]を選択：`customer_entity`
  * [!UICONTROL column]を選択：`Customer's first order GA medium`
  * [!UICONTROL Path]&#x200B;: `sales_flat_order.customer_id = customer_entity.entity_id`

## 指標

* **広告費**
* **`Consolidated Digital Ad Spend`** テーブル内
* この指標は&#x200B;**合計**&#x200B;を実行します
* **`adCost`**&#x200B;列
* **`date`** タイムスタンプで注文

* **広告インプレッション**
* **`Consolidated Digital Ad Spend`** テーブル内
* この指標は&#x200B;**合計**&#x200B;を実行します
* **`Impressions`**&#x200B;列
* **`Month`** タイムスタンプで注文

* **広告クリック**
* **`Consolidated Digital Ad Spend`** テーブル内
* この指標は&#x200B;**合計**&#x200B;を実行します
* **`adClicks`**&#x200B;列
* **`Month`** タイムスタンプで注文

>[!NOTE]
>
>新しいレポートを作成する前に、必ず[すべての新しい列を指標](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md)にディメンションとして追加してください。

## レポート

* **広告費（すべての時間）**
  * [!UICONTROL Metric]：広告費

* 指標`A`：広告費
* [!UICONTROL Time period]&#x200B;: `All time`
* &#x200B;
  [!UICONTROL 間隔]&#x200B;: `None`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Scalar`

* **広告顧客獲得（常に）**
  * [!UICONTROL Metric]&#x200B;: `New customers`
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * フィルターロジック：（[`A`]または[`B`]または[`C`]）と[`D`]

* 指標`A`: `Ad customer acquisitions`
* [!UICONTROL Time period]&#x200B;: `All time`
* &#x200B;
  [!UICONTROL 間隔]&#x200B;: `None`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Scalar`

* **広告ROI**
  * [!UICONTROL Metric]：広告費

  * [!UICONTROL Metric]&#x200B;: `New customers`
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * フィルターロジック：（[`A`]または[`B`]または[`C`]）と[`D`]

  * [!UICONTROL Metric]：平均生涯売上
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * フィルターロジック：（[`A`]または[`B`]または[`C`]）と[`D`]

  * [!UICONTROL Formula]&#x200B;: `((C - (A / B)) / (A / B))`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `Percentage`

* 指標`A`: `Ad Spend (hide)`
* 指標`B`: `Ad customer acquisitions (hide)`
* 指標`C`: `Average LTV (hide)`
* [!UICONTROL Formula]&#x200B;: `Ads ROI`
* [!UICONTROL Time period]&#x200B;: `All time`
* &#x200B;
  [!UICONTROL 間隔]&#x200B;: `None`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Scalar`

* **GA中の注文**
  * &#x200B;
    [!UICONTROL 指標]&#x200B;: `Orders`

* 指標`A`: `Orders`
* [!UICONTROL Time period]&#x200B;: `All time`
* [!UICONTROL Interval]&#x200B;: `By Month`
* [!UICONTROL Group by]&#x200B;: `Order's medium`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Area`

* キャンペーン別&#x200B;**広告ROI**
  * [!UICONTROL Metric]&#x200B;: `Ad Spend`

  * [!UICONTROL Metric]&#x200B;:`New customers`
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * フィルターロジック：（[`A`]または[`B`]または[`C`]）と[`D`]

  * [!UICONTROL Metric]：平均生涯売上
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * フィルターロジック：（[`A`]または[`B`]または[`C`]）と[`D`]

  * [!UICONTROL Metric]：注文の平均生涯数
  * [!UICONTROL Filters]:
    * `User's first order's source LIKE %google%`
    * `User's first order's source LIKE %facebook%`
    * `User's first order's source LIKE %fb%`
    * `User's first order's medium IN cpc, ppc`
    * フィルターロジック：（[`A`]または[`B`]または[`C`]）と[`D`]

  * [!UICONTROL Formula]&#x200B;: `(A / B)`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `Currency`

  * [!UICONTROL Formula]&#x200B;: `(C - (A / B))`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `Currency`

  * [!UICONTROL Formula]&#x200B;: `((C - (A / B)) / (A / B))`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `Percentage`

  * [!UICONTROL Metric]&#x200B;: `Ad Clicks`

  * [!UICONTROL Metric]&#x200B;: `Ad Impressions`

  * [!UICONTROL Formula]&#x200B;: `(H / I)`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `Percentage`

  * [!UICONTROL Formula]&#x200B;: `(A / H)`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `Currency`

* 指標`A`: `Ad Spend` （非表示）
* 指標`B`: `Ad customer acquisitions`
* 指標`C`: `Average LTV`
* 指標`D`: `Average lifetime # of orders`
* &#x200B;
  [!UICONTROL 数式]&#x200B;: `CAC`
* [!UICONTROL Formula]&#x200B;: `Avg return`
* [!UICONTROL Formula]&#x200B;: `Ads ROI`
* 指標`H`: `adClicks`
* 指標`I`: `Impressions`
* &#x200B;
  [!UICONTROL 数式]&#x200B;: `CTR`
* &#x200B;
  [!UICONTROL 数式]&#x200B;: `CPC`
* [!UICONTROL Time period]&#x200B;: `All time`
* &#x200B;
  [!UICONTROL 間隔]&#x200B;: `None`
* &#x200B;
  [!UICONTROL グループ化：]: `campaign` (「顧客の最初の注文」キャンペーンを広告以外の費用テーブル指標に使用する)
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Table`

この分析の構築中に質問が発生した場合、または単にプロフェッショナルサービスチームに連絡したい場合は、[&#x200B; サポートにお問い合わせください](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies)。

### 関連

* [&#x200B; [!DNL Google Analytics]でのUTM タグ付けのベストプラクティス](../../best-practices/utm-tagging-google.md)
* [&#x200B; [!DNL Google Analytics] UTM アトリビューションの仕組み](../analysis/utm-attributes.md)
