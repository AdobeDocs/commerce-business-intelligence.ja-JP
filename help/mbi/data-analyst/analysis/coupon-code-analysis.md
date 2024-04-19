---
title: クーポンのパフォーマンス
description: クーポンのパフォーマンス分析について説明します。
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: d8fc96a58b72c601a5700f35ea1f3dc982d76571
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# 高度なクーポンコード分析

あなたのビジネスのクーポンパフォーマンスを理解することは、注文をセグメント化するための興味深い方法であり、顧客をより深く理解することもできます。 このトピックでは、クーポンを使用して取得した顧客と、その顧客が一般的なクーポンの使用をどのように実行および追跡するかを理解するための分析を作成する手順を説明します。

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

この分析に含まれる内容 [高度な計算列](../data-warehouse-mgr/adv-calc-columns.md).

## はじめに

最初の手順として、次の列がData Warehouseに同期されていることを確認する必要があります。 存在しない場合は、に移動して、追跡に進みます。 `Manage Data` > `Data Warehouse`。次の項目を同期しています。

* **sales\_flat\_order** テーブル
* **coupon\_code**
* **base\_discount\_amount**

## 計算される列

ゲスト注文ポリシーに関係なく作成する列：

* `sales\_flat\_order` テーブル
* **注文にクーポンが適用されていますか？**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`

   * 
     [!UICONTROL データ型]: `String`
   * [!UICONTROL Calculation]：の場合 `A` が null の場合、 `No coupon` else `Coupon` 終了

* **\[INPUT\] customer\_id - クーポン コード**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`

   * [!UICONTROL Datatype] 文字列
   * [!UICONTROL Calculation]: `concat(A,' - ',B)`

* **このクーポンを使用した注文数**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * イベント所有者：`INPUT customer_id - coupon code`
   * イベントのランク： `created\_at`
   * [!UICONTROL Filters]: `Orders we count` フィルターセット

ゲストによる注文がサポートされていない場合に作成する追加列：

* `customer\_entity` テーブル
   * **顧客の最初の注文にクーポンが含まれていますか？ （クーポン/クーポンなし）**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * を選択 [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`

   * **顧客の初回注文クーポン**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * を選択 [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`

   * **顧客の生涯使用クーポン数**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`

   * **クーポン取得顧客または非クーポン取得顧客**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

      * 
        [!UICONTROL データ型]: `String`
      * [!UICONTROL Calculation]: **ケース A=&#39;クーポン&#39; then &#39;クーポン取得顧客&#39; else &#39;クーポン取得顧客&#39;終了**

   * **顧客のクーポン付き注文の割合**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`

      * 
        [!UICONTROL データ型]: `Decimal`
      * [!UICONTROL Calculation]: **a が null または B が null または B=0 の場合、null または A/B が終了した場合**

   * **顧客のクーポン使用状況**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`

      * 
        [!UICONTROL データ型]: `String`
      * [!UICONTROL Calculation]: **a が null で、次に null の場合 A=0 で「クーポンを使用しない」場合 A&lt;0.5、次に「ほぼ完全な価格」 A=0.5、次に「50/50」 A>0.5、次に「クーポンのみ」、次に「ほぼ完全なクーポン」、それ以外は「未定義」の場合**

* `sales\_flat\_order` テーブル
   * **顧客の最初の注文にクーポンが含まれていますか？ （クーポン/クーポンなし）**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * を選択 [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^

   * **顧客の初回注文クーポン**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * を選択 [!UICONTROL column]: `Customer's first order coupon?`

ゲストによる注文がサポートされていない場合に作成する追加列：

* `sales\_flat\_order` テーブル
   * **顧客の最初の注文にクーポンが含まれていますか？ （クーポン/クーポンなし）** **-** アナリストが\[ クーポン分析\] チケットの一部として作成しました
   * **顧客の初回注文クーポン**{::}**-** アナリストが\[ クーポン分析\] チケットの一部として作成しました

* **顧客の生涯使用クーポン数**{::}**-** アナリストが\[ クーポン分析\] チケットの一部として作成しました
* **クーポン取得顧客または非クーポン取得顧客**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

   * 
     [!UICONTROL データ型]: `String`
   * [!UICONTROL Calculation]: **ケース A=&#39;クーポン&#39; then &#39;クーポン取得顧客&#39; else &#39;クーポン取得顧客&#39;終了**

* **顧客のクーポン付き注文の割合**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`

   * 
     [!UICONTROL データ型]: `Decimal`
   * [!UICONTROL Calculation]: **a が null または B が null または B=0 の場合、null または A/B が終了した場合**

* **顧客のクーポン使用状況**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`

   * 
     [!UICONTROL データ型]: `String`
   * [!UICONTROL Calculation]: **a が null で、次に null の場合 A=0 で「クーポンを使用しない」場合 A&lt;0.5、次に「ほぼ完全な価格」 A=0.5、次に「50/50」 A>0.5、次に「クーポンのみ」、次に「ほぼ完全なクーポン」、それ以外は「未定義」の場合**

## 指標

* **クーポン割引金額**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* が含まれる `sales\_flat\_order` テーブル
* このメトリックは、 **合計**
* 日 `discount\_amount` 列
* による並べ替え `created\_at` timestamp
* [!UICONTROL Filter]:

* **使用されたクーポンの数**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* が含まれる `sales\_flat\_order` テーブル
* このメトリックは、 **カウント**
* 日 `entity\_id` 列
* による並べ替え `created\_at` timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>必ずしてください [すべての新規列をディメンションとして指標に追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に、

## レポート

* **クーポン取得済およびクーポン未取得顧客の割合（%）**
   * [!UICONTROL Metric]: `New customers`

* 指標 `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` または `Non coupon acquisition customer`
* 
  [!UICONTROL グラフ タイプ]: `Pie`

* **クーポンで取得された顧客とクーポンで取得されなかった顧客の数**
   * [!UICONTROL Metric]: `New customers`

* 指標 A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` または `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **平均生涯売上高：クーポン Acq. （90 日以上）**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポンが含まれている（クーポン/クーポンなし） = クーポン

* 指標 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL グラフ タイプ]: `Scalar`

* **平均生涯売上高：クーポン以外の Acq。 （90 日以上）**
   * [!UICONTROL Metric]：平均生涯売上高
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポン （クーポン/クーポンなし） = クーポンなし

* 指標 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL グラフ タイプ]: `Scalar`

* **初回注文クーポン別の平均生涯売上高**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 指標 `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* 
  [!UICONTROL グラフ タイプ]: `Column`

>[!NOTE]
>
>多くのクライアントと同様に多くのクーポンコードがある場合は、上位/下位を適用します上位 10 を平均ライフタイム収益で並べ替えます

* **繰り返し注文の可能性：クーポンの取得**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポンが含まれている（クーポン/クーポンなし） = クーポン

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポンが含まれている（クーポン/クーポンなし） = クーポン
      * 顧客の最後の注文か =いいえ
   * 
     [!UICONTROL 数式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 統計的に有意な数を次から選択 `Customer's by lifetime orders` グラフ。 グラフを見る際の良いルールは、バケットに 30 以上の顧客がある注文番号を探すことです。 データセットによっては、この値が大きくなる場合があるので、自由に 1～10 を加算してください。

* 指標 `A`: `Number of orders`
* 指標 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **繰り返し注文の可能性：非クーポン取得**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポン （クーポン/クーポンなし） = クーポンなし

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポン （クーポン/クーポンなし） = クーポンなし
      * 顧客の最後の注文か =いいえ

   * 
     [!UICONTROL 数式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 統計的に有意な数を次から選択 `Customer's by lifetime orders` グラフまたは 1-5。

* 指標 `A`: `Number of orders`
* 指標 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **クーポン取得顧客のクーポン使用率（リピート注文）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * クーポン取得顧客または非クーポン取得顧客= クーポン取得

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * お客様の注文番号 > 1
      * 顧客の最初の注文にクーポンが含まれていますか？ （クーポン/クーポンなし） = クーポン

   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * お客様の注文番号 > 1
      * 顧客の最初の注文にクーポンが含まれていますか？ （クーポン/クーポンなし） = クーポン
      * 注文にクーポンが適用されていますか？ （クーポン/クーポンなし） = クーポン

   * 
     [!UICONTROL 数式]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* 指標 `A`: `Coupon-acquired customers`
* 指標 `B`: `Number of repeat orders`
* 指標 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL グラフ タイプ]: `Table` (ビジュアライゼーションを向上させるために、このテーブルを転置できます)

* **非クーポン取得顧客のクーポン使用率（リピート注文）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * クーポン取得顧客または非クーポン取得顧客=非クーポン取得

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * お客様の注文番号 > 1
      * 顧客の最初の注文にクーポンが含まれていますか？ （クーポン/クーポンなし） = クーポンなし

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * お客様の注文番号 > 1
      * 顧客の最初の注文にクーポンが含まれていますか？ （クーポン/クーポンなし） =クーポンなし
      * 注文にクーポンが適用されていますか？ （クーポン/クーポンなし） = クーポン

   * 
     [!UICONTROL 数式]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* 指標 `A`: `Non-coupon-acquired customers`
* 指標 `B`: `Number of repeat orders`
* 指標 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL グラフ タイプ]: `Table` (ビジュアライゼーションを向上させるために、このテーブルを転置できます)

* **クーポンの使用状況の詳細（初回の注文）**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンを使用した注文数 > 10

   * 
     [!UICONTROL 指標]: `Revenue`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンを使用した注文数 > 10

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンを使用した注文数 > 10

   * [!UICONTROL Formula]: `B-C` （C が負の場合）; B+C （C が正の場合）
   * 
     [!UICONTROL 形式]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンを使用した注文数 > 10

* 指標 `A`: `First time orders (FTO)`
* 指標 `B`: `Revenue from FTO`
* 指標 `C`: `Discounts applied to FTO`
* [!UICONTROL Formula]: `Gross revenue from FTO`
* 指標 `E`: `Average order value for FTO`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
  [!UICONTROL グラフ タイプ]: `Table`
>[!NOTE]
>
>「このクーポンでの注文数」の数量 10 は任意です。 このフィルターに最適な量を自由に使用してください。

* **クーポンを使用した注文数（常に）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 指標 `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL グラフ タイプ]: `Scalar`

* **クーポン付き注文からの純売上高（常に）**
   * 
     [!UICONTROL 指標]: `Revenue`
   * [!UICONTROL Filter]:
      * 注文にクーポンが適用されていますか？ （クーポン/クーポンなし） = クーポン

* 指標 `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL グラフ タイプ]: `Scalar`

* **クーポンからの割引（常に）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 指標 `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL グラフ タイプ]: `Scalar`

* **クーポンの有無による注文の数**
   * [!UICONTROL Metric]: `Number of orders`

* 指標 `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **リピートユーザー間のクーポン使用**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 顧客の生涯注文数 > 1

* 指標 `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* 
  [!UICONTROL グラフ タイプ]: `Pie`

* **クーポン使用状況の詳細**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * このクーポンを使用した注文数 > 10

   * 
     [!UICONTROL 指標]: `Revenue`
   * [!UICONTROL Filter]:
      * このクーポンを使用した注文数 > 10

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * このクーポンを使用した注文数 > 10

   * [!UICONTROL Formula]: `B-C` （if `C` が負の数）; `B+C` （if `C` 正の数）
   * 
     [!UICONTROL 形式]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` （if `C` が負の数）; `C/(B+C)` （if `C` 正の数）
   * 
     [!UICONTROL 形式]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * このクーポンを使用した注文数 > 10

   * 
     [!UICONTROL 数式]: `C/A`
   * 
     [!UICONTROL 形式]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * このクーポンを使用した注文数 > 10

* 指標 `A`: `Number of orders`
* 指標 `B`: `Net revenue from orders`
* 指標 `C`: `Total discounts applied`
* [!UICONTROL Formula]: `Gross revenue`
* [!UICONTROL Formula]: `% discounted`
* 指標 `F`: `Average net order value`
* [!UICONTROL Formula]: `Average order discount`
* 指標 `H`: `Distinct buyers`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
  [!UICONTROL グラフ タイプ]: `Table`

>[!NOTE]
>
>「このクーポンでの注文数」の数量 10 は任意です。 このフィルターに最適な量を自由に使用してください。

すべてのレポートをコンパイルした後、必要に応じてダッシュボード上で整理できます。 結果は、ページ上部の画像のようになります。

分析中に質問が発生した場合、または単にプロフェッショナルサービスチームに依頼したい場合、 [サポートに連絡する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

>[!NOTE]
>
>Adobe Commerce 2.4.7 以降、のお客様は以下を使用できます **quote_coupons** および **sales_order_coupons** 顧客が複数のクーポンをどのように使用しているかに関するインサイトを取得するテーブル。

![](../../assets/multicoupon_relationship_tables.png)
