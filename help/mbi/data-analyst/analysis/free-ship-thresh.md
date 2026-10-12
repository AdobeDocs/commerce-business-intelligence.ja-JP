---
title: 送料無料しきい値
description: 送料無料しきい値のパフォーマンスを追跡するダッシュボードを設定する方法について説明します。
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
role: Admin,  User
feature: Data Warehouse Manager, Dashboards, Reports
TQID: 'https://experienceleague.adobe.com/dh7Ep6xzBaaeO5LAnsUogg0jSCIXMjv-faBsPyGXpcg'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: 06e518d4-11ae-5c20-98b0-ce8ab05d7166
    internal-label: Dashboards
  - id: f842eedf-96a8-52c7-891d-4e56f7441a7e
    internal-label: Reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 17%
---
# 送料無料

>[!NOTE]
>
>このトピックには、元のアーキテクチャと新しいアーキテクチャを使用しているクライアントの手順が含まれています。 メインツールバーから「`Manage Data`」を選択した後に「`Data Warehouse Views`」セクションを使用できる場合は、新しいアーキテクチャを使用しています。

このトピックでは、送料無料しきい値のパフォーマンスを追跡するダッシュボードを設定する方法を示します。 このダッシュボードは、2つの送料無料しきい値をA/B テストするための優れた方法です。 例えば、送料無料を50 ドルと100 ドルのどちらで提供すべきか、判断できないことがあります。 顧客の2つのランダムサブセットのA/B テストを実行し、[!DNL Commerce Intelligence]で分析を実行する必要があります。

開始する前に、ストアの送料無料しきい値が異なる2つの期間を特定する必要があります。

![送料無料のしきい値分析と注文金額の分布を示すグラフ &#x200B;](../../assets/free_shipping_threshold.png)

この分析には、[高度な計算列](../data-warehouse-mgr/adv-calc-columns.md)が含まれています。

## 予定列

元のアーキテクチャを使用している場合（例えば、`Manage Data` メニューの下に`Data Warehouse Views` オプションがない場合）は、サポートチームに連絡して、以下の列を作成する必要があります。 新しいアーキテクチャでは、これらの列は`Manage Data > Data Warehouse` ページから作成できます。 詳細な手順は以下のとおりです。

* **`sales_flat_order`** テーブル
  * この計算では、一般的なカートのサイズに対してバケットを増分で作成します。 これには、5、10、50、100などの増分の範囲があります

* **`Order subtotal (buckets)`** Original Architecture: アナリストが`[FREE SHIPPING ANALYSIS]` チケットの一部として作成しました
* **`Order subtotal (buckets)`**&#x200B;新しいアーキテクチャ：
  * 前述のように、この計算では、一般的なカートサイズに対してバケットを増分で作成します。 `base_subtotal`のようなネイティブの小計カラムがある場合、この新しいカラムのベースとして使用できます。 そうでない場合は、送料と割引を収益から除外する計算列を使用できます。

  >[!NOTE]
  >
  >「バケット」のサイズは、クライアントとして適切なものによって異なります。 `average order value`から始めて、その金額より少ないバケットと大きいバケットを作成できます。 以下の計算を見ると、クエリの一部を簡単にコピーし、編集し、追加のグループを作成する方法が表示されます。 この例は、50単位で実行します。

  * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal`、または`calculated column`、`Datatype`: `Integer`
  * [!UICONTROL Calculation]&#x200B;: `case when A >= 0 and A<=200 then 0 - 200`
    `A< 200`と`A <= 250`のとき `201 - 250`
    `A<251`と`A<= 300`のとき `251 - 300`
    `A<301`と`A<= 350`のとき `301 - 350`
    `A<351`と`A<=400`のとき `351 - 400`
    `A<401`と`A<=450`のとき `401 - 450`
    else &#39;over 450&#39;
    終了


## 指標

新しい指標はありません！!!

>[!NOTE]
>
>新しいレポートを作成する前に、必ず[すべての新しい列を指標](../data-warehouse-mgr/manage-data-dimensions-metrics.md)にディメンションとして追加してください。

## レポート

* **配送ルール A**&#x200B;の平均注文額
  * [!UICONTROL Metric]&#x200B;: `Average order value`

* 指標`A`: `Average Order Value`
* [!UICONTROL Time period]&#x200B;: `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]&#x200B;: `None`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Scalar`

* **配送ルール A**&#x200B;を持つ小計バケット別の注文数
  * [!UICONTROL Metric]&#x200B;: `Number of orders`

  >[!NOTE]
  >
  >`Show top/bottom`にトップ `X` `sorted by` `Order subtotal` （バケット）を表示すると、テールエンドを切り取ることができます。

* 指標`A`: `Number of orders`
* [!UICONTROL Time period]&#x200B;: `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]&#x200B;: `None`
* [!UICONTROL Group by]&#x200B;: `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Column`

* **配送ルール A**&#x200B;を持つ小計による注文の割合
  * [!UICONTROL Metric]&#x200B;: `Number of orders`

  * [!UICONTROL Metric]&#x200B;: `Number of orders`
  * &#x200B;
    [!UICONTROL グループ化：]&#x200B;: `Independent`
  * [!UICONTROL Formula]&#x200B;: `(A / B)`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `%`

* 指標`A`: `Number of orders by subtotal (hide)`
* 指標`B`: `Total number of orders (hide)`
* [!UICONTROL Formula]&#x200B;: `% of orders`
* [!UICONTROL Time period]&#x200B;: `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]&#x200B;: `None`
* [!UICONTROL Group by]&#x200B;: `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Line`

* **小計が発送ルール A**&#x200B;を超える注文の割合
  * [!UICONTROL Metric]&#x200B;: `Number of orders`
  * &#x200B;
    [!UICONTROL Perspective]&#x200B;: `Cumulative`

  * [!UICONTROL Metric]&#x200B;: `Number of orders`
  * &#x200B;
    [!UICONTROL グループ化：]&#x200B;: `Independent`

  * [!UICONTROL Formula]&#x200B;: `1- (A / B)`
  * &#x200B;
    [!UICONTROL Format]&#x200B;: `%`

* 指標`A`: `Number of orders by subtotal`
* 指標`B`: `Total number of orders (hide)`
* [!UICONTROL Formula]&#x200B;: `% of orders`
* [!UICONTROL Time period]&#x200B;: `Time period with shipping rule A`
* &#x200B;
  [!UICONTROL Interval]&#x200B;: `None`
* [!UICONTROL Group by]&#x200B;: `Order subtotal (buckets)`
* &#x200B;
  [!UICONTROL Chart Type]&#x200B;: `Line`


上記の手順とレポートを繰り返して、配送Bと配送ルール Bの期間を確認します。

すべてのレポートをまとめた後、必要に応じてダッシュボード上でレポートを整理できます。 結果は、このページの上部の画像のように見えます。
