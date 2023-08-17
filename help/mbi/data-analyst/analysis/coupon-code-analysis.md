---
title: クーポン効果
description: クーポン効果の分析について説明します。
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# 高度なクーポンコード分析

ビジネスのクーポンパフォーマンスを理解することは、注文をセグメント化し、顧客をより深く理解するための興味深い方法です。 このトピックでは、分析を作成する手順を説明し、クーポンを使用して取得した顧客と、その顧客がどのように実行し、一般的なクーポン使用状況を追跡するかを把握します。

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

この分析に含まれる内容 [高度な計算列](../data-warehouse-mgr/adv-calc-columns.md).

## はじめに

最初の手順として、次の列がData Warehouseと同期されていることを確認する必要があります。 存在しない場合は、次の場所に移動して、それらを追跡します。 `Manage Data` > `Data Warehouse`、以下の同期：

* **sales\_flat\_order** 表
* **coupon\_code**
* **base\_discount\_amount**

## 計算列

ゲストによる注文ポリシーに関係なく作成する列：

* `sales\_flat\_order` 表
* **注文にクーポンが適用されていますか？**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`

   * 
     [!UICONTROL データ型]: `String`
   * [!UICONTROL Calculation]：次の場合のケース `A` が null の場合は `No coupon` else `Coupon` 終了

* **\[INPUT\] customer\_id — クーポンコード**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`

   * [!UICONTROL Datatype] 文字列
   * [!UICONTROL Calculation]: `concat(A,' - ',B)`

* **このクーポンを持つ注文の数**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * イベント所有者：`INPUT customer_id - coupon code`
   * イベントランク： `created\_at`
   * [!UICONTROL Filters]: `Orders we count` フィルターセット

ゲストによる注文がサポートされていない場合に作成する追加の列：

* `customer\_entity` 表
   * **顧客の最初の注文にクーポンが含まれていたか。 （クーポン/クーポンなし）**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * を選択します。 [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`

   * **顧客の初回注文のクーポン**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * を選択します。 [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`

   * **使用した顧客のライフタイムクーポン数**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`

   * **クーポン獲得顧客またはクーポン獲得顧客**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

      * 
        [!UICONTROL データ型]: `String`
      * [!UICONTROL Calculation]: **A=&#39;クーポン&#39;、「クーポン獲得顧客」、「クーポン獲得顧客」の場合、それ以外の場合、「非クーポン獲得顧客」の終了**

   * **顧客の注文の割合（クーポンあり）**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`

      * 
        [!UICONTROL データ型]: `Decimal`
      * [!UICONTROL Calculation]: **A が null または B が null または B が 0 の場合は null を、それ以外の場合は A/B の終わり**

   * **顧客のクーポン使用状況**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`

      * 
        [!UICONTROL データ型]: `String`
      * [!UICONTROL Calculation]: **A が null の場合は null、Null の場合は null、A が 0 の場合は「クーポンを使用しない」、A が 0.5 の場合は「全体価格」、A が 0.5 の場合は「50/50」、A が 0.5 の場合は「クーポンのみ」、それ以外の場合は「未定義」の場合**

* `sales\_flat\_order` 表
   * **顧客の最初の注文にクーポンが含まれていますか？ （クーポン/クーポンなし）**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * を選択します。 [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^

   * **顧客の初回注文のクーポン**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * を選択します。 [!UICONTROL column]: `Customer's first order coupon?`

ゲストによる注文がサポートされていない場合に作成する追加の列：

* `sales\_flat\_order` 表
   * **顧客の最初の注文にクーポンが含まれていたか。 （クーポン/クーポンなし）** **-** \[COUPON ANALYSIS\] チケットの一部としてアナリストが作成しました
   * **顧客の初回注文のクーポン**{::}**-** \[COUPON ANALYSIS\] チケットの一部としてアナリストが作成しました

* **使用した顧客のライフタイムクーポン数**{::}**-** \[COUPON ANALYSIS\] チケットの一部としてアナリストが作成しました
* **クーポン獲得顧客またはクーポン獲得顧客**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

   * 
     [!UICONTROL データ型]: `String`
   * [!UICONTROL Calculation]: **A=&#39;クーポン&#39;、「クーポン獲得顧客」、「クーポン獲得顧客」の場合、それ以外の場合、「非クーポン獲得顧客」の終了**

* **顧客の注文の割合（クーポンあり）**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`

   * 
     [!UICONTROL データ型]: `Decimal`
   * [!UICONTROL Calculation]: **A が null または B が null または B が 0 の場合は null を、それ以外の場合は A/B の終わり**

* **顧客のクーポン使用状況**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`

   * 
     [!UICONTROL データ型]: `String`
   * [!UICONTROL Calculation]: **A が null の場合は null、Null の場合は null、A が 0 の場合は「クーポンを使用しない」、A が 0.5 の場合は「全体価格」、A が 0.5 の場合は「50/50」、A が 0.5 の場合は「クーポンのみ」、それ以外の場合は「未定義」の場合**

## 指標

* **クーポン割引額**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* Adobe Analytics の `sales\_flat\_order` 表
* この指標では **合計**
* 次の日： `discount\_amount` 列
* 並べ替え元 `created\_at` timestamp
* [!UICONTROL Filter]:

* **使用されたクーポン数**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* Adobe Analytics の `sales\_flat\_order` 表
* この指標では **カウント**
* 次の日： `entity\_id` 列
* 並べ替え元 `created\_at` timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>必ず [すべての新しい列を指標のディメンションとして追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に。

## レポート

* **クーポンを獲得した顧客と獲得していない顧客の割合**
   * [!UICONTROL Metric]: `New customers`

* 指標 `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` または `Non coupon acquisition customer`
* 
  [!UICONTROL グラフの種類]: `Pie`

* **クーポンを取得したおよびクーポンを取得しなかった顧客の数**
   * [!UICONTROL Metric]: `New customers`

* 指標 A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` または `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **平均全期間売上高：クーポン Acq. （生後 90 日以上）**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポンが含まれました（クーポン/クーポンなし） =クーポン

* 指標 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL グラフの種類]: `Scalar`

* **全期間平均売上高：非クーポン Acq. （生後 90 日以上）**
   * [!UICONTROL Metric]：全期間の平均売上高
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポンが含まれました（クーポン/クーポンなし） =クーポンなし

* 指標 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL グラフの種類]: `Scalar`

* **初回注文クーポン別の平均ライフタイム売上高**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 指標 `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* 
  [!UICONTROL グラフの種類]: `Column`

>[!NOTE]
>
>多くのクーポンコードがある場合、多くの顧客と同様に、トップ 10 を平均ライフタイム売上高で並べ替えた場合など、トップ/ボトムを適用する必要があります

* **リピート注文の可能性：クーポン獲得**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポンが含まれました（クーポン/クーポンなし） =クーポン

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポンが含まれました（クーポン/クーポンなし） =クーポン
      * 顧客の最後の注文は？ =いいえ
   * 
     [!UICONTROL 数式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 統計的に有意な数を次の中から選択 `Customer's by lifetime orders` グラフ。 グラフを見るとき、30 人以上の顧客がグループに含まれる注文番号を探すのが適切です。 データセットによっては、この数が多い場合があるので、1 ～ 10 を自由に追加できます。

* 指標 `A`: `Number of orders`
* 指標 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **繰り返し注文の確率：非クーポン獲得**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポンが含まれました（クーポン/クーポンなし） =クーポンなし

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポンが含まれました（クーポン/クーポンなし） =クーポンなし
      * 顧客の最後の注文は？ =いいえ

   * 
     [!UICONTROL 数式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * 統計的に有意な数を次の中から選択 `Customer's by lifetime orders` グラフまたは 1 ～ 5。

* 指標 `A`: `Number of orders`
* 指標 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **クーポン取得済み顧客のクーポン使用率（リピート注文）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * クーポン獲得顧客または非クーポン獲得顧客=クーポン獲得

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の注文番号 > 1
      * 顧客の最初の注文にクーポンが含まれていたか。 （クーポン/クーポンなし） =クーポン

   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の注文番号 > 1
      * 顧客の最初の注文にクーポンが含まれていたか。 （クーポン/クーポンなし） =クーポン
      * 注文にクーポンが適用されていますか？ （クーポン/クーポンなし） =クーポン

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
  [!UICONTROL グラフの種類]: `Table` (このテーブルを置き換えて、より良いビジュアライゼーションを実現できます)

* **クーポンを獲得していない顧客のクーポン使用率（リピート注文）**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * クーポン獲得顧客または非クーポン獲得顧客=クーポン獲得

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の注文番号 > 1
      * 顧客の最初の注文にクーポンが含まれていたか。 （クーポン/クーポンなし） =クーポンなし

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の注文番号 > 1
      * 顧客の最初の注文にクーポンが含まれていたか。 （クーポン/クーポンなし） =クーポンなし
      * 注文にクーポンが適用されていますか？ （クーポン/クーポンなし） =クーポン

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
  [!UICONTROL グラフの種類]: `Table` (このテーブルを置き換えて、より良いビジュアライゼーションを実現できます)

* **クーポン使用状況の詳細（初回注文）**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンが 10 を超える注文の数

   * 
     [!UICONTROL 指標]: `Revenue`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンが 10 を超える注文の数

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンが 10 を超える注文の数

   * [!UICONTROL Formula]: `B-C` （C が負の場合）; B+C （C が正の場合）
   * 
     [!UICONTROL 形式]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンが 10 を超える注文の数

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
  [!UICONTROL グラフの種類]: `Table`
>[!NOTE]
>
>「このクーポンを使用した注文数」の数量 10 は任意です。 このフィルターに最も適した数量を自由に使用できます。

* **クーポン付きの注文数（常時）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 指標 `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL グラフの種類]: `Scalar`

* **クーポンを含む注文からの純売上高（全期間）**
   * 
     [!UICONTROL 指標]: `Revenue`
   * [!UICONTROL Filter]:
      * 注文にクーポンが適用されていますか？ （クーポン/クーポンなし） =クーポン

* 指標 `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL グラフの種類]: `Scalar`

* **クーポンからの割引（常時）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 指標 `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* 
  [!UICONTROL グラフの種類]: `Scalar`

* **クーポンのある注文の数とない注文の数**
   * [!UICONTROL Metric]: `Number of orders`

* 指標 `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **リピートユーザー間のクーポン使用状況**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 顧客の全期間の注文件数 > 1

* 指標 `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* 
  [!UICONTROL グラフの種類]: `Pie`

* **クーポン使用状況の詳細**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * このクーポンが 10 を超える注文の数

   * 
     [!UICONTROL 指標]: `Revenue`
   * [!UICONTROL Filter]:
      * このクーポンが 10 を超える注文の数

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * このクーポンが 10 を超える注文の数

   * [!UICONTROL Formula]: `B-C` ( `C` は負 )。 `B+C` ( `C` は正の数 )
   * 
     [!UICONTROL 形式]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` ( `C` は負 )。 `C/(B+C)` ( `C` は正の数 )
   * 
     [!UICONTROL 形式]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * このクーポンが 10 を超える注文の数

   * 
     [!UICONTROL 数式]: `C/A`
   * 
     [!UICONTROL 形式]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * このクーポンが 10 を超える注文の数

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
  [!UICONTROL グラフの種類]: `Table`

>[!NOTE]
>
>「このクーポンを使用した注文数」の数量 10 は任意です。 このフィルターに最も適した数量を自由に使用できます。

すべてのレポートをコンパイルした後、必要に応じてダッシュボードで整理できます。 結果は、ページ上部の画像のようになる場合があります。

この分析の構築中に質問が発生した場合、または単に Professional Services チームを引き付けたい場合は、 [連絡先サポート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
