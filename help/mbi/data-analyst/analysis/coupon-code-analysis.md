---
title: クーポンパフォーマンス
description: クーポンのパフォーマンス分析について詳しく見る。
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
role: Admin, User
feature: Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/uqVpwXs8XHpiPpXHmTgItkhDsHAGs-Ty5NSBK8KtO7s
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 1243
ht-degree: 0%

---

# 高度なクーポンコード分析

ビジネスのクーポンパフォーマンスを把握することは、注文をセグメンテーションし、顧客をより深く理解するための興味深い方法です。 このトピックでは、クーポンを使用して獲得した顧客、そのパフォーマンス、一般的なクーポンの使用状況の追跡を理解するための分析を作成する手順について説明します。

主要な指標を示す分析ライブラリの![ クーポンコード分析](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

この分析には、[高度な計算列](../data-warehouse-mgr/adv-calc-columns.md)が含まれています。

## はじめに

最初の手順として、次の列がData Warehouseに同期されていることを確認する必要があります。 まだの場合は、`Manage Data` > `Data Warehouse`に移動し、次の項目を同期して追跡します。

* **sales\_flat\_order** テーブル
* **クーポン\_code**
* **base\_discount\_amount**

## 予定列

ゲスト注文ポリシーに関係なく作成する列：

* `sales\_flat\_order` テーブル
* **注文でクーポンが適用されていますか？**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`

   * 
     [!UICONTROL データタイプ]: `String`
   * [!UICONTROL Calculation]: `A`がnullの場合、次に`No coupon` else `Coupon`が終了します

* **\[INPUT\] customer\_id - クーポンコード**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`

   * [!UICONTROL Datatype]文字列
   * [!UICONTROL Calculation]: `concat(A,' - ',B)`

* **このクーポンを使用した注文数**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * イベント所有者：`INPUT customer_id - coupon code`
   * イベントランク：`created\_at`
   * [!UICONTROL Filters]: `Orders we count` フィルターセット

ゲスト注文がサポートされていない場合に作成する追加の列：

* `customer\_entity` テーブル
   * **お客様の最初の注文にはクーポンが含まれていますか？ （クーポン/クーポンなし）**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * [!UICONTROL column]を選択：`Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`

   * **お客様の最初の注文のクーポン**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL column]を選択：`coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`

   * **お客様が使用したクーポンの生涯数**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`

   * **クーポン取得顧客またはクーポン以外の取得顧客**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

      * 
        [!UICONTROL データタイプ]: `String`
      * [!UICONTROL Calculation]: **A=&#39;クーポン&#39;から&#39;クーポン獲得のお客様&#39; else &#39;クーポン以外のお客様&#39; end**&#x200B;の場合

   * **クーポンを使用した顧客の注文の割合**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`

      * 
        [!UICONTROL データタイプ]: `Decimal`
      * [!UICONTROL Calculation]: **AがnullまたはBがnullまたはB=0の場合、その後nullの場合はA/B終了**

   * **お客様のクーポン使用状況**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`

      * 
        [!UICONTROL データタイプ]: `String`
      * [!UICONTROL Calculation]: **Aがnullの場合、A=0の場合はnull、A&lt;0.5の場合は「未使用のクーポン」、A=0.5の場合は「ほぼフルプライス」、A=1の場合は「50/50」、A>0.5の場合は「クーポンのみ」、その後「ほとんどクーポン」の場合は「未定義」の場合は**

* `sales\_flat\_order` テーブル
   * **お客様の最初のご注文にはクーポンが含まれていますか？ （クーポン/クーポンなし）**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL column]を選択：`Customer's first order included a coupon? (Coupon/No coupon)`
^

   * **お客様の最初の注文のクーポン**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL column]を選択：`Customer's first order coupon?`

ゲスト注文がサポートされていない場合に作成する追加の列：

* `sales\_flat\_order` テーブル
   * **お客様の最初の注文にはクーポンが含まれていますか？ （クーポン/クーポンなし）** **-**&#x200B;は、\[COUPON ANALYSIS\] チケットの一部としてアナリストによって作成されました
   * アナリストが\[COUPON ANALYSIS\] チケットの一部として作成した&#x200B;**お客様の最初の注文のクーポン&#x200B;**{::}**-**

* アナリストが\[COUPON ANALYSIS\] チケットの一部として作成した&#x200B;**お客様のクーポン使用回数&#x200B;**{::}**～**&#x200B;です
* **クーポン取得顧客またはクーポン以外の取得顧客**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

   * 
     [!UICONTROL データタイプ]: `String`
   * [!UICONTROL Calculation]: **A=&#39;クーポン&#39;から&#39;クーポン獲得のお客様&#39; else &#39;クーポン以外のお客様&#39; end**&#x200B;の場合

* **クーポンを使用した顧客の注文の割合**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`

   * 
     [!UICONTROL データタイプ]: `Decimal`
   * [!UICONTROL Calculation]: **AがnullまたはBがnullまたはB=0の場合、その後nullの場合はA/B終了**

* **お客様のクーポン使用状況**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`

   * 
     [!UICONTROL データタイプ]: `String`
   * [!UICONTROL Calculation]: **Aがnullの場合、A=0の場合はnull、A&lt;0.5の場合は「未使用のクーポン」、A=0.5の場合は「ほぼフルプライス」、A=1の場合は「50/50」、A>0.5の場合は「クーポンのみ」、その後「ほとんどクーポン」の場合は「未定義」の場合は**

## 指標

* **クーポン割引額**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* `sales\_flat\_order` テーブル内
* この指標は&#x200B;**合計**&#x200B;を実行します
* `discount\_amount`列
* `created\_at` タイムスタンプで注文
* [!UICONTROL Filter]:

* **使用されたクーポンの数**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* `sales\_flat\_order` テーブル内
* この指標は&#x200B;**カウント**&#x200B;を実行します
* `entity\_id`列
* `created\_at` タイムスタンプで注文
* [!UICONTROL Filter]:

>[!NOTE]
>
>新しいレポートを作成する前に、必ず[すべての新しい列を指標](../data-warehouse-mgr/manage-data-dimensions-metrics.md)にディメンションとして追加してください。

## レポート

* クーポン取得済み顧客とクーポン取得済みでない顧客の&#x200B;**%**
   * [!UICONTROL Metric]: `New customers`

* 指標`A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer`または`Non coupon acquisition customer`
* 
  [!UICONTROL チャートタイプ]: `Pie`

* **クーポン取得済み顧客とクーポン取得済みでない顧客の数**
   * [!UICONTROL Metric]: `New customers`

* 指標A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer`または`Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **平均生涯売上：クーポン Acq。 （90日以上）**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にはクーポンが含まれています（クーポン/クーポンなし） = クーポン

* 指標`A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
  [!UICONTROL間隔]: `None`
* 
  [!UICONTROL チャートタイプ]: `Scalar`

* **平均生涯売上：非クーポン Acq。 （90日以上）**
   * [!UICONTROL Metric]：平均生涯売上
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にはクーポンが含まれています（クーポンなし） = クーポンなし

* 指標`A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
  [!UICONTROL間隔]: `None`
* 
  [!UICONTROL チャートタイプ]: `Scalar`

* **初回注文クーポンによる平均生涯売上**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 指標`A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* 
  [!UICONTROL チャートタイプ]: `Column`

>[!NOTE]
>
>多くの顧客と同じように多くのクーポンコードがある場合は、平均生涯収益でソートされたトップ 10などのトップ/ボトムを適用します

* **繰り返し注文の確率率：クーポン取得**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にはクーポンが含まれています（クーポン/クーポンなし） = クーポン

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にはクーポンが含まれています（クーポン/クーポンなし） = クーポン
      * お客様の最後の注文？ = No
   * 
     [!UICONTROL数式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * `Customer's by lifetime orders` グラフから統計的に有意な数値を選択します。 グラフを見る場合、良いルールは、バケットに30人以上の顧客を含む注文番号を探すことです。 データセットによっては膨大なデータ数になる場合もあるので、1～10を自由に追加してください。

* 指標`A`: `Number of orders`
* 指標`B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **繰り返し注文確率：クーポン以外の取得**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にはクーポンが含まれています（クーポンなし） = クーポンなし

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にはクーポンが含まれています（クーポンなし） = クーポンなし
      * お客様の最後の注文？ = No

   * 
     [!UICONTROL数式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * `Customer's by lifetime orders` グラフまたは1 ～ 5から統計的に有意な数値を選択します。

* 指標`A`: `Number of orders`
* 指標`B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **クーポン取得済み顧客のクーポン使用率（リピート注文）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * クーポン獲得顧客または非クーポン獲得顧客= クーポン獲得

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の注文番号> 1
      * 顧客の最初の注文にはクーポンが含まれていますか？ （クーポン/クーポンなし） = クーポン

   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の注文番号> 1
      * 顧客の最初の注文にはクーポンが含まれていますか？ （クーポン/クーポンなし） = クーポン
      * クーポンが適用された注文？ （クーポン/クーポンなし） = クーポン

   * 
     [!UICONTROL数式]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* 指標`A`: `Coupon-acquired customers`
* 指標`B`: `Number of repeat orders`
* 指標`C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL間隔]: `None`
* 
  [!UICONTROL チャートタイプ]: `Table` (このテーブルを置き換えて視覚化を向上できます)

* **クーポン取得済みでない顧客のクーポン使用率（リピート注文）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * クーポン獲得顧客または非クーポン獲得顧客= クーポン以外の獲得

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の注文番号> 1
      * 顧客の最初の注文にはクーポンが含まれていますか？ （クーポン/クーポンなし） = クーポンなし

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の注文番号> 1
      * 顧客の最初の注文にはクーポンが含まれていますか？ （クーポン/クーポンなし） = クーポンなし
      * クーポンが適用された注文？ （クーポン/クーポンなし） = クーポン

   * 
     [!UICONTROL数式]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* 指標`A`: `Non-coupon-acquired customers`
* 指標`B`: `Number of repeat orders`
* 指標`C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL間隔]: `None`
* 
  [!UICONTROL チャートタイプ]: `Table` (このテーブルを置き換えて視覚化を向上できます)

* **クーポン使用状況の詳細（初回注文）**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンが10を超える注文数

   * 
     [!UICONTROL指標]: `Revenue`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンが10を超える注文数

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンが10を超える注文数

   * [!UICONTROL Formula]: `B-C` （Cが負の場合）、B+C （Cが正の場合）
   * 
     [!UICONTROL形式]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンが10を超える注文数

* 指標`A`: `First time orders (FTO)`
* 指標`B`: `Revenue from FTO`
* 指標`C`: `Discounts applied to FTO`
* [!UICONTROL Formula]: `Gross revenue from FTO`
* 指標`E`: `Average order value for FTO`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
  [!UICONTROL チャートタイプ]: `Table`
>[!NOTE]
>
>「このクーポンを使用した注文数」の10の数量は任意です。 このフィルターに最適な量を使用してください。

* **クーポン付き注文数（常時）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 指標`A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL間隔]: `None`
* 
  [!UICONTROL チャートタイプ]: `Scalar`

* **クーポン付きの注文の純収益（常に）**
   * 
     [!UICONTROL指標]: `Revenue`
   * [!UICONTROL Filter]:
      * クーポンが適用された注文？ （クーポン/クーポンなし） = クーポン

* 指標`A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL間隔]: `None`
* 
  [!UICONTROL チャートタイプ]: `Scalar`

* **クーポンからの割引（常に）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 指標`A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL間隔]: `None`
* 
  [!UICONTROL チャートタイプ]: `Scalar`

* **クーポンの有無に関する注文数**
   * [!UICONTROL Metric]: `Number of orders`

* 指標`A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
  [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **リピートユーザー間のクーポン使用率**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 顧客のライフタイム注文数> 1

* 指標`A`: `New customers`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* 
  [!UICONTROL チャートタイプ]: `Pie`

* **クーポン使用状況の詳細**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * このクーポンが10を超える注文数

   * 
     [!UICONTROL指標]: `Revenue`
   * [!UICONTROL Filter]:
      * このクーポンが10を超える注文数

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * このクーポンが10を超える注文数

   * [!UICONTROL Formula]: `B-C` （`C`が負の場合）、`B+C` （`C`が正の場合）
   * 
     [!UICONTROL形式]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` （`C`が負の場合）、`C/(B+C)` （`C`が正の場合）
   * 
     [!UICONTROL形式]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * このクーポンが10を超える注文数

   * 
     [!UICONTROL数式]: `C/A`
   * 
     [!UICONTROL形式]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * このクーポンが10を超える注文数

* 指標`A`: `Number of orders`
* 指標`B`: `Net revenue from orders`
* 指標`C`: `Total discounts applied`
* [!UICONTROL Formula]: `Gross revenue`
* [!UICONTROL Formula]: `% discounted`
* 指標`F`: `Average net order value`
* [!UICONTROL Formula]: `Average order discount`
* 指標`H`: `Distinct buyers`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL間隔]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
  [!UICONTROL チャートタイプ]: `Table`

>[!NOTE]
>
>「このクーポンを使用した注文数」の10の数量は任意です。 このフィルターに最適な量を使用してください。

すべてのレポートをまとめた後、必要に応じてダッシュボード上でレポートを整理できます。 その結果、ページの上部に画像が表示されます。

この分析の構築中に質問が発生した場合、または単にプロフェッショナルサービスチームに連絡したい場合は、[ サポートにお問い合わせください](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

>[!NOTE]
>
>Adobe Commerce 2.4.7以降、お客様は&#x200B;**quote_coupons**&#x200B;および&#x200B;**sales_order_coupons**&#x200B;のテーブルを使用して、お客様が複数のクーポンをどのように使用しているかについてのインサイトを取得できます。

![ マルチクーポン分析のテーブル関係図](../../assets/multicoupon_relationship_tables.png)
