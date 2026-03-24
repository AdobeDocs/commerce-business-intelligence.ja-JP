---
title: すぐに利用できるダッシュボード
description: Insightをすばやく提供するダッシュボードについて解説します。
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/niQ01gOnBCdufbZDpw0mcck3AWN-2gXR1QyWD8LHLBQ
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 1950
ht-degree: 0%

---

# すぐに利用できるダッシュボード

[!DNL Adobe Commerce Intelligence]には、insightをビジネスに提供するための、すぐに使えるダッシュボードが含まれています。 ダッシュボードでは、利用者の生涯売上、リピート購入数、一定期間に購入された製品の上位など、重要な指標の健全性を確認することができます。 これらの事前設定済みのダッシュボードは、情報にもとづいたビジネス上の意思決定に役立つように作成されています。

>[!NOTE]
>
>これらのダッシュボードへのアクセスは、アカウントの種類とアクセスレベルによって異なります。 これらのダッシュボードが表示されない場合は、[ サポート ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)にお問い合わせください。

## レポートの可用性

`Customers`および`Executive Summary` ダッシュボードの場合、一部のレポートは、ストアのチェックアウト設定によってのみ使用できます。 具体的には、ストアでゲストチェックアウトが許可されているか、ゲストチェックアウトが許可されていない場合です。

## 顧客（ゲストチェックアウト可能）

顧客（ゲストチェックアウト可能）ダッシュボードには、購入行動などの顧客基盤に関する情報が表示されます。 このダッシュボードは、顧客維持率を向上させ、どの顧客が最も高い売上をもたらすかを判断するのに役立ちます。

### レポート

| 名前 | 説明 |
|---|---|
| `Orders by New Customers (Past 30 Days)` | 過去30日間に、以前に注文したことがない顧客から注文しました。 |
| `Orders by Existing Customers (Past 30 Days)` | 過去30日間に少なくとも1回の注文を行った顧客からの注文。 |
| `Total Unique Customers (Past 30 Days)` | 過去30日間に注文したユニーク顧客の数。 |
| `Orders by New vs Existing Customers` | 前回の注文がない顧客と、少なくとも1回の前回の注文がある顧客の注文数。 |
| `Subsequent Order Probability (All Time)` | 注文した顧客が別の注文をおこなう可能性があります。 |
| `% of Customers with Multiple Orders (All Time)` | 1つ以上の注文を行ったすべての顧客の割合。 |
| `Median Time Between Orders (All Time)` | 各顧客が1回の注文から次の注文までの平均時間です。 |
| `Subsequent Order Probability` | 注文した顧客が別の注文を行う可能性（注文番号で分類）。 つまり、1つの注文で第2の注文を行う顧客の割合、2つの注文で第3の注文を行う顧客の割合などです。 |
| `Time Between Orders` | 顧客が注文間に要する平均時間と中央値を注文番号で示します（注文1と2の間、2と3の間などの時間）。 |
| `Number of Customers - Lifetime Orders` | 顧客のライフタイムにおける一定数の注文に対して、その数件の注文を行った顧客の数と、その数が表す顧客層全体のパーセンテージ。 |
| `One-Time Customers who Bought 3-6 Months Ago` | 3～6 ヶ月前に初めてのみ購入した顧客。 |
| `Avg LTV by First Order` | コホート間の累積平均顧客生涯売上を比較します。 コホートは、顧客が最初に購入した月によって定義されます。 例えば、`Jan 2020` コホートは、2020年1月に最初に購入した顧客の累積平均LTVを示しています。 |
| `Customer's First 30 Day vs Lifetime Revenue` | 最初の購入後30日間の顧客の平均売上と生涯価値の比較。 各バブルは配送地域に対応し、各バブルのサイズはその地域から獲得した顧客数を表します。 |

## 顧客（ゲストチェックアウトは許可されていません）

顧客（ゲストチェックアウトは許可されていません）ダッシュボードには、購入行動やアカウント登録から注文へのコンバージョンなど、顧客基盤に関する情報が表示されます。 このダッシュボードは、顧客維持率を向上させ、どの顧客が最も高い売上をもたらすかを判断するのに役立ちます。

### レポート

| 名前 | 説明 |
|---|---|
| `Account Registration (Past 30 Days)` | 過去30日間に店舗にアカウントを登録したユーザーの数。 |
| `Accounts Registered (Past 30 Days) with 1 or More Orders` | 過去30日間に店舗にアカウントを登録し、少なくとも1回の注文を行った人の数。 |
| `% Conversion from Registration to First Order (Past 30 Days)` | 過去30日間に登録され、注文したアカウントの割合。 |
| `% Conversion from Registration to First Order` | 登録されたアカウントのうち、注文したアカウントの割合（登録月別）。 |
| `Orders by New vs Existing Customers` | 前回の注文がない顧客と、少なくとも1回の前回の注文がある顧客の注文数。 |
| `Subsequent Order Probability (All Time)` | 注文した顧客が別の注文をおこなう可能性があります。 |
| `% of Customers with Multiple Orders (All Time)` | 1つ以上の注文を行ったすべての顧客の割合。 |
| `Median Time Between Orders (All Time)` | 各顧客が1回の注文から次の注文までの平均時間です。 |
| `Subsequent Order Probability` | 注文した顧客が別の顧客を注文する可能性を、注文番号で分類します。 つまり、1つの注文を持つ顧客の%が2番目に配置され、2つの顧客が3番目に配置される顧客の%などです。 |
| `Time Between Orders` | 顧客が注文間に要する平均時間と中央値を注文番号で示します（注文1と2の間、2と3の間などの時間）。 |
| `Number of Customers - Lifetime Orders` | 顧客のライフタイムにおける一定数の注文に対して、その数件の注文を行った顧客の数と、その数が表す顧客層全体のパーセンテージ。 |
| `One-Time Customers who Bought 3-6 Months Ago` | 3～6 ヶ月前に初めてのみ購入した顧客。 |
| `Avg LTV by First Order` | コホート間の累積平均顧客生涯売上を比較します。 コホートは、顧客が最初に購入した月によって定義されます。 例えば、2020年1月のコホートでは、初回購入が2020年1月の顧客の累積平均LTVを示しています。 |
| `Customer's First 30 Day vs Lifetime Revenue` | 最初の購入後30日間の顧客の平均売上と生涯価値の比較。 各バブルは配送地域に対応し、各バブルのサイズはその地域から獲得した顧客数を表します。 |

## エグゼクティブサマリー（ゲストチェックアウト可能）

エグゼクティブサマリー（ゲストチェックアウト可能）ダッシュボードでは、注文と収益の観点から、ビジネスの状況を簡潔に把握できます。 このダッシュボードは、経営陣がビジネスパフォーマンスを包括的に把握できるように設計されていますが、他の従業員にもインサイトを提供できます。

### レポート

| 名前 | 説明 |
|---|---|
| `Revenue (Current Month)` | 当月のストアによって生成された収益。 この場合、収益は、顧客が注文に対して支払った最終価格として定義されます。 |
| `Revenue (Past 6 Months by Day)` | 1日当たりの総売上。過去7日間の1日当たりの平均売上と重なります。 この場合、収益は、顧客が注文に対して支払った最終価格として定義されます。 |
| `% Change in Revenue (MoM MTD)` | 今月（現時点）と前月の同じ部分の収益の比較。 |
| `Revenue from New vs Existing Customers (Current Month)` | 新規顧客（初回訪問客）と既存顧客（2回目以降の注文）に対する当月（現時点）の売上。 |
| `Average Order Value (Current Month)` | 当月の注文の1日の平均金額（現時点）。 注文金額は、顧客が注文に対して支払った最終価格として定義されます。 |
| `Orders (Current Month)` | 現在の月にストアに入った注文数（現時点）。 |
| `% Change in Orders (MoM MTD)` | 当月の注文数（現時点）と前月の同じ部分の比較。 |
| `Orders by New Customers (Current Month)` | 以前に注文したことがない顧客からの当月の注文。 |
| `Orders by Existing Customers (Current Month)` | 以前に1つ以上の注文を行った顧客からの当月の注文。 |
| `Orders by New vs Existing Customers (Current Year by Week)` | 前回注文がない顧客による注文数と、少なくとも1回の前回注文がある顧客による、当年の各週（現在のところ）の注文数。 |

## エグゼクティブサマリー（ゲストチェックアウト不可）

エグゼクティブサマリー（ゲストチェックアウトは許可されていません）ダッシュボードでは、注文、売上、アカウント登録の観点から、ビジネスの状況を簡単に把握できます。 このダッシュボードは、経営陣がビジネスパフォーマンスを包括的に把握できるように設計されていますが、他の従業員にもインサイトを提供できます。

### レポート

| 名前 | 説明 |
|---|---|
| `Revenue (Current Month)` | 今月ストアによって生成された収益。 この場合、収益は、顧客が注文に対して支払った最終価格として定義されます。 |
| `Revenue (Past 6 Months by Day)` | 1日当たりの総売上。過去7日間の1日当たりの平均売上と重なります。 この場合、収益は、顧客が注文に対して支払った最終価格として定義されます。 |
| `% Change in Revenue (MoM MTD)` | 今月と前月の同じ部分との比較。 |
| `Revenue from New vs Existing Customers (Current Month)` | 新規顧客（初回訪問客）と既存顧客（2回目以降の注文）に対する当月（現時点）の売上。 |
| `Average Order Value (Current Month)` | 当月の注文の1日の平均金額（現時点）。 注文金額は、顧客が注文に対して支払った最終価格として定義されます。 |
| `Orders (Current Month)` | 現在の月にストアに入った注文数（現時点）。 |
| `% Change in Orders (MoM MTD)` | 当月の注文数（現時点）と前月の同じ部分の比較。 |
| `Account Registrations (Current Month)` | 今月の新規登録者数。 |
| `% Conversion from Registration to First Order (Current Month)` | 今月登録したアカウントのうち、注文したアカウントの割合。 |
| `% Conversion from Registration to First Order (Current Year by Week)` | 今年これまでに登録されたアカウントのうち、注文したアカウントの割合。 |

## 注文

注文ダッシュボードには、取引注文数、ステータス、使用されたクーポンコード、生成された収益、使用された支払い方法に関するインサイトが表示されます。 例えば、フルフィルメントプロセスを追跡し、問題やボトルネックが発生していないことを確認できます。

>[!NOTE]
>
>このダッシュボードのレポートは、いずれかのタイプの設定（ゲストチェックアウト、ゲストチェックアウトなし）を持つストアに接続されているアカウントで使用できます。

### レポート

| 名前 | 説明 |
|---|---|
| `Orders (Past 30 Days)` | 過去30日間に店舗に行われた注文数。 |
| `Revenue (Past 30 Days)` | 過去30日間にストアによって生成された収益。 収益は、顧客が注文に対して支払った最終価格として定義されます。 |
| `Average Order Value (Past 30 Days)` | 過去30日間の平均注文額。 注文金額は、顧客が注文に対して支払った最終価格として定義されます。 |
| `Orders` | 毎月のストアでの注文数。 |
| `Revenue by Payment Method` | ストアによって生成された収益は、支払い方法で分割されます。 収益は、顧客が注文に対して支払った最終価格として定義されます。 |
| `AOV by New vs Existing Customers` | 店舗での注文の月間平均額。前回の注文がない顧客の注文と、少なくとも1回の前回の注文がある顧客の注文で割ります。 注文金額は、顧客が注文に対して支払った最終価格として定義されます。 |
| `% Orders by Status (Past 30 Days)` | 過去30日間の各日からの注文のうち、現在各注文状況にある注文の割合。 |
| `Incomplete Orders (Created more than 1 Day Ago)` | 1日以上前に発注された、まだ不完全なステータス（キャンセルまたは完了していない）のすべての注文のリスト。 |
| `Orders Per Hour (Past 7 Days)` | 日別の注文件数。 |
| `Revenue Details (Past 30 Days)` | 過去30日間の日次の売上の内訳を、売上総額のすべてのコンポーネントに表示します。 |
| `Order Details by Coupon Code (Past 30 Days)` | ストアが提供する各クーポンコードについて、そのクーポンコードの使用方法と、過去30日間における返品方法の詳細。 |
| `% Orders with Coupon (Past 30 Days)` | クーポンを使用した過去30日間の注文と使用しなかった注文の割合。 |

## 特定可能

「製品」ダッシュボードには、注文した製品、その総販売額（GMV）、および購入および返金された上位の製品の一般的な製品パフォーマンスが表示されます。 購入と返品のバランスを取り、商品の成功と人気を判断するのに役立ちます。 これらのグラフを入力するには、返金を追跡するように[ ストアを設定する必要があります](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html)。

>[!NOTE]
>
>このダッシュボードのレポートは、いずれかのタイプの設定（ゲストチェックアウト、ゲストチェックアウトなし）を持つストアに接続されているアカウントで使用できます。

### レポート

| 名前 | 説明 |
|---|---|
| `GMV (Past 30 Days)` | 過去30日間に販売されたすべての商品の総商品価値。 GMVとは、発注された数量に各製品の基準価格を掛けたものです。 |
| `% GMV (Past 30 Days) Refunded` | 過去30日間に購入し返金した製品のGMVの割合。 |
| `Product Quantity Ordered (Past 30 Days)` | 過去30日間に注文した商品の合計数量。 |
| `% Purchased Products (Past 30 Days) Refunded` | 過去30日間に購入し、返品した商品の割合。 |
| `Gross Merchandise Value` | 販売された全商品の総商品価値（月別）。 GMVとは、発注された数量に各製品の基準価格を掛けたものです。 |
| `Purchases vs Refund Rate per Product (Past 30 Days)` | 各製品について、過去30日間の注文総数と製品の返品率の比較。 各バブルのサイズは返金率を表します。 |
| `Product Performance Details (Past 30 Days)` | 過去30日間の販売とその後の返金に関する詳細情報（製品SKUと製品名による）。 |
| `Top Purchased Products by GMV (Past 30 Days)` | 過去30日間に販売された商品のうち、売上が最も多い商品（トップ 10）。 |
| `Top Refunded Products by GMV (Past 30 Days)` | 過去30日間に購入した商品のうち、返金によるGMVの損失が最も多かった商品（トップ 10）。 |
| `Top Purchased Products by Quantity (Past 30 Days)` | 過去30日間に販売された商品が最も多い（トップ 10）。 |
| `Top Refunded Products by Quantity (Past 30 Days)` | 過去30日間に購入した商品のうち、返品数が最も多かった商品（上位10件）。 |
