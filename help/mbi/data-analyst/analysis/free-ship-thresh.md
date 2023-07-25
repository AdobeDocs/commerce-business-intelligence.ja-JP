---
title: 送料無料しきい値
description: 送料無料しきい値のパフォーマンスを追跡するダッシュボードを設定する方法を説明します。
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
role: Admin,  User
feature: Data Warehouse Manager, Dashboards, Reports
source-git-commit: 6bdbdbcc652d476fa2a22589ac99678d5855e6fe
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# 送料無料

>[!NOTE]
>
>このトピックでは、元のアーキテクチャと新しいアーキテクチャを使用しているお客様向けの手順について説明します。 新しいアーキテクチャを使用している場合、 `Data Warehouse Views` 選択後に使用可能なセクション `Manage Data` を選択します。

このトピックでは、送料無料しきい値のパフォーマンスを追跡するダッシュボードを設定する方法を説明します。 このダッシュボードは、A/B テストで 2 つの無料配送しきい値を確認するのに最適です。 例えば、50 ドルと 100 ドルの送料を無料で提供するかどうかが不明な場合があります。 顧客の 2 つのランダムサブセットの A/B テストを実行し、 [!DNL Commerce Intelligence].

開始する前に、2 つの異なる期間を指定し、店舗の送料無料しきい値の値が異なっています。

![](../../assets/free_shipping_threshold.png)

この分析に含まれる内容 [高度な計算列](../data-warehouse-mgr/adv-calc-columns.md).

## 計算列

元のアーキテクチャを使用している場合 ( 例えば、 `Data Warehouse Views` オプションを `Manage Data` メニュー ) を使用する場合は、サポートチームに連絡して、以下の列を構築する必要があります。 新しいアーキテクチャでは、これらの列は `Manage Data > Data Warehouse` ページ。 詳細な手順は以下のとおりです。

* **`sales_flat_order`** 表
   * この計算では、通常の買い物かごサイズに対する増分でグループが作成されます。 5、10、50、100 を含む増分から範囲を指定できます

* **`Order subtotal (buckets)`** 元のアーキテクチャ：アナリストが、 `[FREE SHIPPING ANALYSIS]` チケット
* **`Order subtotal (buckets)`** 新しいアーキテクチャ：
   * 前述のように、この計算では通常の買い物かごサイズに対する増分でグループが作成されます。 ネイティブの小計列 ( `base_subtotal`（この新しい列の基礎として使用できます） そうでない場合は、送料と割引を売上高から除外する計算列を指定できます。

  >[!NOTE]
  >
  >「バケット」のサイズは、クライアントとして適したサイズによって異なります。 まず、 `average order value` そして、その量より少なく、大きい数のバケットを作成します。 以下の計算を見ると、クエリの一部を簡単にコピーし、編集し、追加のバケットを作成する方法がわかります。 例は 50 単位で増分されます。

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`または `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
when `A< 200` および `A <= 250` その後 `201 - 250`
when `A<251` および `A<= 300` その後 `251 - 300`
when `A<301` および `A<= 350` その後 `301 - 350`
when `A<351` および `A<=400` その後 `351 - 400`
when `A<401` および `A<=450` その後 `401 - 450`
それ以外の場合は「450 を超える」で終了


## 指標

新しい指標がありません!!!

>[!NOTE]
>
>必ず [すべての新しい列を指標のディメンションとして追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に

## レポート

* **出荷ルール A を含む平均注文額**
   * [!UICONTROL Metric]: `Average order value`

* 指標 `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **出荷ルール A を含む小計グループ別の注文数**
   * [!UICONTROL Metric]: `Number of orders`

  >[!NOTE]
  >
  >上部を表示することで、尾の端を切り落とすことができます `X` `sorted by` `Order subtotal` （バケット） `Show top/bottom`.

* 指標 `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Column`

* **出荷ルール A による小計別の注文の割合**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
     [!UICONTROL グループ化基準]: `Independent`
   * [!UICONTROL Formula]: `(A / B)`
   * 
     [!UICONTROL Format]: `%`

* 指標 `A`: `Number of orders by subtotal (hide)`
* 指標 `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Line`

* **小計が出荷ルール A を超える注文の割合**
   * [!UICONTROL Metric]: `Number of orders`
   * 
     [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * 
     [!UICONTROL グループ化基準]: `Independent`

   * [!UICONTROL Formula]: `1- (A / B)`
   * 
     [!UICONTROL Format]: `%`

* 指標 `A`: `Number of orders by subtotal`
* 指標 `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Line`


上記の手順とレポートを、出荷 B と出荷ルール B の期間に対して繰り返します。

すべてのレポートをコンパイルした後、必要に応じてダッシュボードで整理できます。 結果は、このページの上部にある画像のようになります。
