---
title: 送料無料しきい値
description: 送料無料のしきい値のパフォーマンスを追跡するダッシュボードの設定方法を説明します。
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
role: Admin,  User
feature: Data Warehouse Manager, Dashboards, Reports
source-git-commit: 6bdbdbcc652d476fa2a22589ac99678d5855e6fe
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# 送料無料

>[!NOTE]
>
>このトピックには、元のアーキテクチャと新しいアーキテクチャを使用しているクライアント向けの手順が含まれています。 次の項目がある場合は、新しいアーキテクチャを使用します `Data Warehouse Views` セクションは選択後に使用可能です `Manage Data` メインツールバーから。

このトピックでは、送料無料のしきい値のパフォーマンスを追跡するダッシュボードの設定方法を示します。 このダッシュボードは、以下に示すように、2 つの送料無料しきい値を A/B テストするための優れた方法です。 例えば、会社によっては、送料無料を 50 ドルと 100 ドルのどちらで提供すべきか分からない場合があります。 顧客の 2 つのランダムサブセットに対して A/B テストを実行し、で分析を実行する必要があります。 [!DNL Commerce Intelligence].

始める前に、ストアの送料無料しきい値の値が異なる 2 つの異なる期間を特定する必要があります。

![](../../assets/free_shipping_threshold.png)

この分析に含まれる内容 [高度な計算列](../data-warehouse-mgr/adv-calc-columns.md).

## 計算される列

元のアーキテクチャを使用している場合（例えば、 `Data Warehouse Views` の下のオプション `Manage Data` メニュー）、サポートチームに連絡して、以下の列を作成します。 新しいアーキテクチャでは、これらの列は `Manage Data > Data Warehouse` ページ。 詳細な手順は以下のとおりです。

* **`sales_flat_order`** テーブル
   * この計算では、通常の買い物かごサイズに応じた増分でバケットが作成されます。 値は、5、10、50、100 などの増分から選択できます

* **`Order subtotal (buckets)`** オリジナルアーキテクチャ：の一部としてアナリストが作成します `[FREE SHIPPING ANALYSIS]` チケット
* **`Order subtotal (buckets)`** 新しいアーキテクチャ：
   * 上記のように、この計算では、通常の買い物かごのサイズに応じた増分でバケットを作成します。 次のようなネイティブの小計列がある場合： `base_subtotal`：この新しい列の基礎として使用できます。 そうでない場合は、売上高から送料と割引を除外する計算列にすることができます。

  >[!NOTE]
  >
  >「バケット」のサイズは、クライアントとして適切な内容によって異なります。 次から開始できます `average order value` そして、その量より少ない、または多いバケットをいくつか作成します。 以下の計算を見ると、クエリの一部を簡単にコピーして編集し、追加のバケットを作成する方法がわかります。 この例は、50 増分で実行されます。

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`、または `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
条件 `A< 200` および `A <= 250` その後 `201 - 250`
条件 `A<251` および `A<= 300` その後 `251 - 300`
条件 `A<301` および `A<= 350` その後 `301 - 350`
条件 `A<351` および `A<=400` その後 `351 - 400`
条件 `A<401` および `A<=450` その後 `401 - 450`
else &#39;over 450&#39;終了


## 指標

新しい指標はありません！!!

>[!NOTE]
>
>必ずしてください [すべての新規列をディメンションとして指標に追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に、

## レポート

* **出荷ルール A を使用した平均注文額**
   * [!UICONTROL Metric]: `Average order value`

* 指標 `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **出荷ルール A を使用した小計バケット別の受注数**
   * [!UICONTROL Metric]: `Number of orders`

  >[!NOTE]
  >
  >上部を表示することで、尾の端を切り取ることができます `X` `sorted by` `Order subtotal` （バケット）が `Show top/bottom`.

* 指標 `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Column`

* **出荷ルール A を使用した小計による受注率**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
     [!UICONTROL Group by]: `Independent`
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

* **小計が出荷ルール A を超えている受注の割合**
   * [!UICONTROL Metric]: `Number of orders`
   * 
     [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * 
     [!UICONTROL Group by]: `Independent`

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


出荷 B および出荷ルール B を含む期間について、前述のステップとレポートを繰り返します。

すべてのレポートをコンパイルした後、必要に応じてダッシュボード上で整理できます。 結果は、このページの上部の画像のようになります。
