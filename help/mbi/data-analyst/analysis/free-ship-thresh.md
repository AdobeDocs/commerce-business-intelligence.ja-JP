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
>このトピックには、元のアーキテクチャと新しいアーキテクチャを使用しているクライアント向けの手順が含まれています。 メインのツールバーから `Data Warehouse Views` を選択した後で「`Manage Data`」セクションを使用できる場合は、新しいアーキテクチャを使用できます。

このトピックでは、送料無料のしきい値のパフォーマンスを追跡するダッシュボードの設定方法を示します。 このダッシュボードは、以下に示すように、2 つの送料無料しきい値を A/B テストするための優れた方法です。 例えば、会社によっては、送料無料を 50 ドルと 100 ドルのどちらで提供すべきか分からない場合があります。 顧客の 2 つのランダムサブセットに対して A/B テストを実行し、[!DNL Commerce Intelligence] で分析を実行する必要があります。

始める前に、ストアの送料無料しきい値の値が異なる 2 つの異なる期間を特定する必要があります。

![](../../assets/free_shipping_threshold.png)

この分析には [ 高度な計算列 ](../data-warehouse-mgr/adv-calc-columns.md) が含まれています。

## 計算される列

元のアーキテクチャを使用している場合（例えば、`Data Warehouse Views` メニューに「`Manage Data`」オプションがない場合）、サポートチームに連絡して、以下の列を作成します。 新しいアーキテクチャでは、`Manage Data > Data Warehouse` のページからこれらの列を作成できます。 詳細な手順は以下のとおりです。

* **`sales_flat_order`** テーブル
   * この計算では、通常の買い物かごサイズに応じた増分でバケットが作成されます。 値は、5、10、50、100 などの増分から選択できます

* **`Order subtotal (buckets)`** オリジナルアーキテクチャ：`[FREE SHIPPING ANALYSIS]` チケットの一部としてアナリストが作成します
* 新 **`Order subtotal (buckets)`** いアーキテクチャ：
   * 上記のように、この計算では、通常の買い物かごのサイズに応じた増分でバケットを作成します。 `base_subtotal` などのネイティブの小計列がある場合は、この新しい列の基礎として使用できます。 そうでない場合は、売上高から送料と割引を除外する計算列にすることができます。

  >[!NOTE]
  >
  >「バケット」のサイズは、クライアントとして適切な内容によって異なります。 `average order value` から始めて、その量より少ない、または多いバケットをいくつか作成できます。 以下の計算を見ると、クエリの一部を簡単にコピーして編集し、追加のバケットを作成する方法がわかります。 この例は、50 増分で実行されます。

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal` または `calculated column`、`Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
`A< 200` 時 `A <= 250` ら `201 - 250` 時
`A<251` 時 `A<= 300` ら `251 - 300` 時
`A<301` 時 `A<= 350` ら `301 - 350` 時
`A<351` 時 `A<=400` ら `351 - 400` 時
`A<401` 時 `A<=450` ら `401 - 450` 時
else &#39;over 450&#39;
終了


## 指標

新しい指標はありません！!!

>[!NOTE]
>
>新しいレポートを作成する前に、必ず [ すべての新しい列をディメンションとして指標に追加する ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) ようにしてください。

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
  >`X` ージに `sorted by` （バケット）の上 `Order subtotal` を表示して、尾 `Show top/bottom` 端を切り取ることができます。

* 指標 `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Column`

* **出荷ルール A を使用した小計による受注の割合**
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
