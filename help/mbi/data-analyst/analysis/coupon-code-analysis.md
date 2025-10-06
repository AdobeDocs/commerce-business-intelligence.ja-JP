---
title: クーポンのパフォーマンス
description: クーポンのパフォーマンス分析について説明します。
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1243'
ht-degree: 0%

---

# 高度なクーポンコード分析

あなたのビジネスのクーポンパフォーマンスを理解することは、注文をセグメント化するための興味深い方法であり、顧客をより深く理解することもできます。 このトピックでは、クーポンを使用して取得した顧客と、その顧客が一般的なクーポンの使用をどのように実行および追跡するかを理解するための分析を作成する手順を説明します。

![&#x200B; 主要指標を示す分析ライブラリからのクーポンコード分析 &#x200B;](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

この分析には [&#x200B; 高度な計算列 &#x200B;](../data-warehouse-mgr/adv-calc-columns.md) が含まれています。

## はじめに

まず、次の列がData Warehouseに同期されていることを確認する必要があります。 一致しない場合は、`Manage Data`/`Data Warehouse` に移動し、次の項目を同期して、問題を追跡します。

* **sales\_flat\_order** テーブル
* **coupon\_code**
* **base\_discount\_amount**

## 計算される列

ゲスト注文ポリシーに関係なく作成する列：

* `sales\_flat\_order` テーブル
* **クーポンの適用順序**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`

   * &#x200B;
     [!UICONTROL データ型]: `String`
   * [!UICONTROL Calculation]:`A` が null の場合は終了 `No coupon`、それ以外の場合 `Coupon` 終了

* **\[INPUT\] customer\_id - クーポンコード**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`

   * [!UICONTROL Datatype] 文字列
   * [!UICONTROL Calculation]: `concat(A,' - ',B)`

* **このクーポンの注文数**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * イベント所有者：`INPUT customer_id - coupon code`
   * イベントのランク：`created\_at`
   * [!UICONTROL Filters]: `Orders we count` フィルターセット

ゲストによる注文がサポートされていない場合に作成する追加列：

* `customer\_entity` テーブル
   * **顧客の最初の注文にはクーポンが含まれていますか？ （クーポン/クーポンなし）**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * [!UICONTROL column] を選択：`Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`

   * **顧客の初回注文クーポン**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL column] を選択：`coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`

   * **顧客が使用したクーポンのライフタイムナンバー**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`

   * **クーポン取得顧客又は非クーポン取得顧客**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

      * &#x200B;
        [!UICONTROL データ型]: `String`
      * [!UICONTROL Calculation]: **A=&#39;クーポン&#39; then &#39;クーポン取得顧客&#39; else &#39;クーポン取得顧客&#39;終了**

   * **顧客のクーポン付き注文の割合**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`

      * &#x200B;
        [!UICONTROL データ型]: `Decimal`
      * [!UICONTROL Calculation]: **A が null または B が null または B=0 の場合、null または A/B が終了した場合**

   * **顧客のクーポン使用状況**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`

      * &#x200B;
        [!UICONTROL データ型]: `String`
      * [!UICONTROL Calculation]: **A が null で、A=0 で「クーポンを使用しない」場合は null、A&lt;0.5、A=0.5、A=1 で「クーポンのみ」の場合は「50/50」、A>0.5、Most coupon」の場合は「未定義」の場合は「クーポンを使用しない」**

* `sales\_flat\_order` テーブル
   * **顧客の最初の注文にクーポンが含まれていますか？ （クーポン/クーポンなし）**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL column] を選択：`Customer's first order included a coupon? (Coupon/No coupon)`
^

   * **顧客の初回注文クーポン**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL column] を選択：`Customer's first order coupon?`

ゲストによる注文がサポートされていない場合に作成する追加列：

* `sales\_flat\_order` テーブル
   * **顧客の最初の注文にはクーポンが含まれていますか？ （クーポン/クーポンなし）** アナリストが\[COUPON ANALYSIS\] チケットの一部として作成した **-**
   * **顧客の最初の注文のクーポン&#x200B;**{::}**-** が、アナリストによって\[ クーポン分析\] チケットの一部として作成されました

* **アナリストがお客様の\[ クーポン分析\] チケットの一部として作成した&#x200B;**{::}**-** に使用されたクーポンの有効期間の数
* **クーポン取得顧客又は非クーポン取得顧客**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

   * &#x200B;
     [!UICONTROL データ型]: `String`
   * [!UICONTROL Calculation]: **A=&#39;クーポン&#39; then &#39;クーポン取得顧客&#39; else &#39;クーポン取得顧客&#39;終了**

* **顧客のクーポン付き注文の割合**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`

   * &#x200B;
     [!UICONTROL データ型]: `Decimal`
   * [!UICONTROL Calculation]: **A が null または B が null または B=0 の場合、null または A/B が終了した場合**

* **顧客のクーポン使用状況**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`

   * &#x200B;
     [!UICONTROL データ型]: `String`
   * [!UICONTROL Calculation]: **A が null で、A=0 で「クーポンを使用しない」場合は null、A&lt;0.5、A=0.5、A=1 で「クーポンのみ」の場合は「50/50」、A>0.5、Most coupon」の場合は「未定義」の場合は「クーポンを使用しない」**

## 指標

* **クーポン割引額**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* `sales\_flat\_order` のテーブル内
* このメトリックは **Sum** を実行します。
* `discount\_amount` 列
* `created\_at` タイムスタンプで並べ替え
* [!UICONTROL Filter]:

* **使用クーポン数**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* `sales\_flat\_order` のテーブル内
* このメトリックは、**カウント** を実行します。
* `entity\_id` 列
* `created\_at` タイムスタンプで並べ替え
* [!UICONTROL Filter]:

>[!NOTE]
>
>新しいレポートを作成する前に、必ず [&#x200B; すべての新しい列をディメンションとして指標に追加する &#x200B;](../data-warehouse-mgr/manage-data-dimensions-metrics.md) ようにしてください。

## レポート

* クーポン取得済み顧客とクーポン未取得顧客の **%**
   * [!UICONTROL Metric]: `New customers`

* 指標 `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` または `Non coupon acquisition customer`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Pie`

* **クーポンで取得した顧客と取得していない顧客の数**
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
* &#x200B;
  [!UICONTROL 間隔]: `None`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Scalar`

* **平均生涯売上高：クーポン以外の Acq。 （90 日以上）**
   * [!UICONTROL Metric]：平均生涯売上高
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポン （クーポン/クーポンなし） = クーポンなし

* 指標 `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Scalar`

* **初回注文クーポン別の平均生涯売上高**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* 指標 `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* &#x200B;
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
   * &#x200B;
     [!UICONTROL 数式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * グラフから統計的に有意な数 `Customer's by lifetime orders` 選択します。 グラフを見る際の良いルールは、バケットに 30 以上の顧客がある注文番号を探すことです。 データセットによっては、この値が大きくなる場合があるので、自由に 1～10 を加算してください。

* 指標 `A`: `Number of orders`
* 指標 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **リピート注文確率：非クーポン取得**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポン （クーポン/クーポンなし） = クーポンなし

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の最初の注文にクーポン （クーポン/クーポンなし） = クーポンなし
      * 顧客の最後の注文か =いいえ

   * &#x200B;
     [!UICONTROL 数式]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * グラフまたは 1～5 から統計的 `Customer's by lifetime orders` 有意な数を選択します。

* 指標 `A`: `Number of orders`
* 指標 `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **クーポン取得顧客のクーポン利用率（リピート注文）**
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

   * &#x200B;
     [!UICONTROL 数式]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* 指標 `A`: `Coupon-acquired customers`
* 指標 `B`: `Number of repeat orders`
* 指標 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Table` (ビジュアライゼーションを向上させるために、このテーブルを転置できます)

* **クーポン未獲得顧客のクーポン使用率（リピート注文）**
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

   * &#x200B;
     [!UICONTROL 数式]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* 指標 `A`: `Non-coupon-acquired customers`
* 指標 `B`: `Number of repeat orders`
* 指標 `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Table` (ビジュアライゼーションを向上させるために、このテーブルを転置できます)

* **クーポン使用状況の詳細（初回注文）**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンを使用した注文数 > 10

   * &#x200B;
     [!UICONTROL 指標]: `Revenue`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンを使用した注文数 > 10

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * 顧客の注文番号= 1
      * このクーポンを使用した注文数 > 10

   * [!UICONTROL Formula]: `B-C` （C が負の場合）; B+C （C が正の場合）
   * &#x200B;
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
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `coupon code`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Table`
>[!NOTE]
>
>「このクーポンでの注文数」の数量 10 は任意です。 このフィルターに最適な量を自由に使用してください。

* **クーポンを使用した注文数（常に）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 指標 `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Scalar`

* **クーポン付き注文による純売上高（常に）**
   * &#x200B;
     [!UICONTROL 指標]: `Revenue`
   * [!UICONTROL Filter]:
      * 注文にクーポンが適用されていますか？ （クーポン/クーポンなし） = クーポン

* 指標 `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Scalar`

* **割引券による割引（常時）**
   * [!UICONTROL Metric]: `Number of coupons used`

* 指標 `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Scalar`

* **クーポンの有無による注文数**
   * [!UICONTROL Metric]: `Number of orders`

* 指標 `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **リピートユーザー間のクーポン使用状況**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * 顧客の生涯注文数 > 1

* 指標 `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Pie`

* **クーポンの使用状況の詳細**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * このクーポンを使用した注文数 > 10

   * &#x200B;
     [!UICONTROL 指標]: `Revenue`
   * [!UICONTROL Filter]:
      * このクーポンを使用した注文数 > 10

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * このクーポンを使用した注文数 > 10

   * [!UICONTROL Formula]: `B-C` （`C` が負の場合）; `B+C` （`C` が正の場合）
   * &#x200B;
     [!UICONTROL 形式]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` （`C` が負の場合）; `C/(B+C)` （`C` が正の場合）
   * &#x200B;
     [!UICONTROL 形式]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * このクーポンを使用した注文数 > 10

   * &#x200B;
     [!UICONTROL 数式]: `C/A`
   * &#x200B;
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
* &#x200B;
  [!UICONTROL 間隔]: `None`
* [!UICONTROL Group by]: `coupon code`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Table`

>[!NOTE]
>
>「このクーポンでの注文数」の数量 10 は任意です。 このフィルターに最適な量を自由に使用してください。

すべてのレポートをコンパイルした後、必要に応じてダッシュボード上で整理できます。 結果は、ページ上部の画像のようになります。

分析中に質問が発生した場合や、プロフェッショナルサービスチームに依頼したい場合は、[&#x200B; サポートにお問い合わせください &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)。

>[!NOTE]
>
>Adobe Commerce 2.4.7 の時点では、お客様は **quote_coupons** および **sales_order_coupons** テーブルを使用して、複数のクーポンの使用方法に関するインサイトを取得できます。

![&#x200B; マルチクーポン分析用のテーブル関係図 &#x200B;](../../assets/multicoupon_relationship_tables.png)
