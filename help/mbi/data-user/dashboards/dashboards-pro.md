---
title: 標準のダッシュボード
description: 標準のダッシュボードを使用して、ビジネスに関するインサイトを提供する方法を説明します。
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1950'
ht-degree: 0%

---

# 標準のダッシュボード

[!DNL Adobe Commerce Intelligence] には、標準のダッシュボードが含まれており、ビジネスに関するインサイトを提供します。 ダッシュボードを使用すると、ユーザーの生涯売上高、リピート購入数、特定の期間に購入された上位の製品など、重要な指標の状態を確認できます。 これらの事前設定済みのダッシュボードは、十分な情報に基づいたビジネス上の意思決定を支援するために作成されています。

>[!NOTE]
>
>これらのダッシュボードへのアクセスは、アカウントのタイプとアクセスレベルに応じて異なります。 これらのダッシュボードが表示されない場合は、[ サポート ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja) にお問い合わせください。

## レポートの可用性

`Customers` および `Executive Summary` ダッシュボードの場合、ストアのチェックアウト設定によっては、一部のレポートしか使用できません。 特に、ストアがゲストのチェックアウトを許可している場合、またはストアがゲストのチェックアウトを許可していない場合。

## 顧客（ゲストのチェックアウトが許可されています）

顧客（ゲストのチェックアウトが許可されています） ダッシュボードには、購入行動など、顧客ベースに関する情報が表示されます。 このダッシュボードは、顧客保持率を向上させ、最も高い売上高をもたらしている顧客を決定するのに役立ちます。

### レポート

| 名前 | 説明 |
|---|---|
| `Orders by New Customers (Past 30 Days)` | 過去に注文したことがない顧客からの過去 30 日間の注文。 |
| `Orders by Existing Customers (Past 30 Days)` | 過去 30 日間に 1 回以上の注文を行った顧客からの注文。 |
| `Total Unique Customers (Past 30 Days)` | 過去 30 日間に注文を行ったユニーク顧客の数。 |
| `Orders by New vs Existing Customers` | 以前の注文がない顧客と 1 つ以上の以前の注文がある顧客の注文数。 |
| `Subsequent Order Probability (All Time)` | 注文した顧客が別の顧客を配置する可能性。 |
| `% of Customers with Multiple Orders (All Time)` | 複数の注文を行ったすべての顧客の割合。 |
| `Median Time Between Orders (All Time)` | 各顧客が注文してから次の注文までにかかる時間の中央値。 |
| `Subsequent Order Probability` | 注文した顧客が別の注文を行う可能性（注文番号別に分類）。 つまり、1 つの注文で 2 番目を配置する顧客の割合、2 で 3 番目を配置する顧客の割合などです。 |
| `Time Between Orders` | 顧客が注文間に取る平均時間と中央値は、注文番号別に分類されます（つまり、注文から注文までの時間が 1 から 2 まで、2 から 3 までなど）。 |
| `Number of Customers - Lifetime Orders` | 顧客の全期間に行われた特定の注文数に対して、その多くの注文を行った顧客の数と、その数が表す顧客ベース全体の割合。 |
| `One-Time Customers who Bought 3-6 Months Ago` | 3 か月前から 6 か月前の間に初めて購入した顧客。 |
| `Avg LTV by First Order` | 複数のコホートをまたいで、顧客のライフタイム収益の累積平均を比較します。 コホートは、顧客が最初に購入を行った月によって定義されます。 例えば、ある `Jan 2020` コホートは、2020 年 1 月に初回購入を行った顧客の累積平均 LTV を表示します。 |
| `Customer's First 30 Day vs Lifetime Revenue` | 初回購入後 30 日間の顧客からの平均売上高と、全期間の平均売上高の比較。 各バブルは出荷地域に対応し、各バブルのサイズはその地域から取得した顧客の数を表します。 |

## 顧客（ゲストのチェックアウトは許可されていません）

顧客（ゲストのチェックアウトは許可されていません）ダッシュボードには、購入行動や、アカウント登録から注文プレースメントへのコンバージョンなど、顧客ベースに関する情報が表示されます。 このダッシュボードは、顧客保持率を向上させ、最も高い売上高をもたらしている顧客を決定するのに役立ちます。

### レポート

| 名前 | 説明 |
|---|---|
| `Account Registration (Past 30 Days)` | 過去 30 日間にストアのアカウントに登録したユーザーの数。 |
| `Accounts Registered (Past 30 Days) with 1 or More Orders` | 過去 30 日間にストアでアカウントに登録し、さらに 1 つ以上の注文を行ったユーザーの数。 |
| `% Conversion from Registration to First Order (Past 30 Days)` | 過去 30 日間に登録され、注文したアカウントの割合。 |
| `% Conversion from Registration to First Order` | 注文済み登録済みアカウントの割合（登録月別）。 |
| `Orders by New vs Existing Customers` | 以前の注文がない顧客と 1 つ以上の以前の注文がある顧客の注文数。 |
| `Subsequent Order Probability (All Time)` | 注文した顧客が別の顧客を配置する可能性。 |
| `% of Customers with Multiple Orders (All Time)` | 複数の注文を行ったすべての顧客の割合。 |
| `Median Time Between Orders (All Time)` | 各顧客が注文してから次の注文までにかかる時間の中央値。 |
| `Subsequent Order Probability` | 注文した顧客が別の注文を行う可能性が、注文番号別に分類されます。 つまり、1 つの顧客が 2 番目を注文する場合の割合、2 人の顧客が 3 番目を注文する場合の割合などです。 |
| `Time Between Orders` | 顧客が注文間に取る平均時間と中央値は、注文番号別に分類されます（つまり、注文から注文までの時間が 1 から 2 まで、2 から 3 までなど）。 |
| `Number of Customers - Lifetime Orders` | 顧客の全期間に行われた特定の注文数に対して、その多くの注文を行った顧客の数と、その数が表す顧客ベース全体の割合。 |
| `One-Time Customers who Bought 3-6 Months Ago` | 3 か月前から 6 か月前の間に初めて購入した顧客。 |
| `Avg LTV by First Order` | 複数のコホートをまたいで、顧客のライフタイム収益の累積平均を比較します。 コホートは、顧客が最初に購入を行った月によって定義されます。 例えば、2020 年 1 月のコホートは、最初の購入が 2020 年 1 月だった顧客の累積平均 LTV を表示します。 |
| `Customer's First 30 Day vs Lifetime Revenue` | 初回購入後 30 日間の顧客からの平均売上高と、全期間の平均売上高の比較。 各バブルは出荷地域に対応し、各バブルのサイズはその地域から取得した顧客の数を表します。 |

## エグゼクティブサマリー（ゲストによるチェックアウトが許可されています）

エグゼクティブサマリー（ゲストのチェックアウトが許可されました）ダッシュボードを使用すると、注文と売上高の面でビジネスのパフォーマンスを簡潔に把握できます。 このダッシュボードは、経営幹部がビジネスのパフォーマンスを全体的に理解できるように設計されていますが、他の人にとっても洞察に富んでいます。

### レポート

| 名前 | 説明 |
|---|---|
| `Revenue (Current Month)` | 今月にストアで生成された売上高。 この場合において、売上高とは、注文に関して顧客が支払った最終的な価格をいう。 |
| `Revenue (Past 6 Months by Day)` | 日次合計売上高。過去 7 日間の日次平均売上高とオーバーレイされます。 この場合において、売上高とは、注文に関して顧客が支払った最終的な価格をいう。 |
| `% Change in Revenue (MoM MTD)` | 当月（これまで）の売上高と前月の同月部分の売上高の比較。 |
| `Revenue from New vs Existing Customers (Current Month)` | 今月（これまで）の収益で、新規（初回）顧客と既存の顧客に関連付けられていた（2 回目以降の注文を行っている）。 |
| `Average Order Value (Current Month)` | 当月（これまで）に発注された注文の 1 日当たりの平均値。 注文金額は、注文に対して顧客が支払う最終価格として定義されます。 |
| `Orders (Current Month)` | 当月（これまで）にストアで行われた注文の数。 |
| `% Change in Orders (MoM MTD)` | 当月（これまで）の注文数と前月の同月部分の比較。 |
| `Orders by New Customers (Current Month)` | 以前に注文したことがない顧客からの今月の注文。 |
| `Orders by Existing Customers (Current Month)` | 1 つ以上の注文を行った顧客からの今月の注文。 |
| `Orders by New vs Existing Customers (Current Year by Week)` | 前年の週ごとの、以前の注文がない顧客による注文と、1 回以上の以前の注文がある顧客による注文の数（これまで）。 |

## エグゼクティブサマリー（ゲストのチェックアウトは不可）

エグゼクティブサマリー（ゲストのチェックアウトは許可されていません）ダッシュボードを使用すると、注文、売上高、アカウント登録に関するビジネスの状況を簡潔に把握できます。 このダッシュボードは、経営幹部がビジネスのパフォーマンスを全体的に理解できるように設計されていますが、他の人にとっても洞察に富んでいます。

### レポート

| 名前 | 説明 |
|---|---|
| `Revenue (Current Month)` | 今月ストアで生み出された売上高。 この場合において、売上高とは、注文に関して顧客が支払った最終的な価格をいう。 |
| `Revenue (Past 6 Months by Day)` | 日次合計売上高。過去 7 日間の日次平均売上高とオーバーレイされます。 この場合において、売上高とは、注文に関して顧客が支払った最終的な価格をいう。 |
| `% Change in Revenue (MoM MTD)` | 今月のこれまでの売上高と前月の同部分の比較。 |
| `Revenue from New vs Existing Customers (Current Month)` | 今月（これまで）の収益で、新規（初回）顧客と既存の顧客に関連付けられていた（2 回目以降の注文を行っている）。 |
| `Average Order Value (Current Month)` | 当月（これまで）に発注された注文の 1 日当たりの平均値。 注文金額は、注文に対して顧客が支払う最終価格として定義されます。 |
| `Orders (Current Month)` | 当月（これまで）にストアで行われた注文の数。 |
| `% Change in Orders (MoM MTD)` | 当月（これまで）の注文数と前月の同月部分の比較。 |
| `Account Registrations (Current Month)` | 今月の新規登録済みアカウント数。 |
| `% Conversion from Registration to First Order (Current Month)` | 今月これまでに登録され、注文したアカウントの割合。 |
| `% Conversion from Registration to First Order (Current Year by Week)` | 今年これまでに登録された、注文したアカウントの割合。 |

## 注文件数

注文ダッシュボードでは、注文のトランザクション量、ステータス、使用されたクーポンコード、生成された売上高、使用された支払い方法に関するインサイトを提供します。 例えば、フルフィルメントプロセスを追跡し、問題やボトルネックが発生していないことを確認できます。

>[!NOTE]
>
>このダッシュボードのレポートは、いずれかのタイプの設定（ゲストのチェックアウト、ゲストのチェックアウトなし）でストアに接続されたアカウントで使用できます。

### レポート

| 名前 | 説明 |
|---|---|
| `Orders (Past 30 Days)` | 過去 30 日間にストアで行われた注文の数。 |
| `Revenue (Past 30 Days)` | 過去 30 日間にストアで生成された売上高。 売上高は、注文に対して顧客が支払う最終価格として定義されます。 |
| `Average Order Value (Past 30 Days)` | 過去 30 日間に行われた注文の平均値。 注文金額は、注文に対して顧客が支払う最終価格として定義されます。 |
| `Orders` | 店舗で毎月行われた注文数。 |
| `Revenue by Payment Method` | ストアで生成された売上高を、支払い方法で分割します。 売上高は、注文に対して顧客が支払う最終価格として定義されます。 |
| `AOV by New vs Existing Customers` | ストアでの注文の月間平均金額。以前の注文がない顧客と 1 回以上の以前の注文がある顧客の注文で分割されます。 注文金額は、注文に対して顧客が支払う最終価格として定義されます。 |
| `% Orders by Status (Past 30 Days)` | 過去 30 日間の各日からの注文のうち、現在各注文ステータスにある注文の割合。 |
| `Incomplete Orders (Created more than 1 Day Ago)` | 1 日以上前に発注され、まだ未完了ステータス（取消または完了ではない）のすべての受注のリスト。 |
| `Orders Per Hour (Past 7 Days)` | 注文量（日/時間）。 |
| `Revenue Details (Past 30 Days)` | 過去 30 日間の毎日の収益を、合計収益値のすべてのコンポーネントに分類。 |
| `Order Details by Coupon Code (Past 30 Days)` | 店舗で提供されるクーポンコードごとに、そのクーポンコードの使用方法と、過去 30 日間に持ち込まれた戻り値に関する詳細を説明します。 |
| `% Orders with Coupon (Past 30 Days)` | 過去 30 日間に発注されたクーポンの使用比率と使用比率。 |

## 製品

製品ダッシュボードには、注文された製品、総商品価値（GMV）、購入および払い戻された上位の製品に関する一般的な製品パフォーマンスが表示されます。 購入と返品のバランスを取り、製品の成功と人気を判断するのに役立ちます。 これらのグラフを入力するには、ストアを [ 払戻をトラッキングするように設定 ](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html?lang=ja) する必要があります。

>[!NOTE]
>
>このダッシュボードのレポートは、いずれかのタイプの設定（ゲストのチェックアウト、ゲストのチェックアウトなし）でストアに接続されたアカウントで使用できます。

### レポート

| 名前 | 説明 |
|---|---|
| `GMV (Past 30 Days)` | 過去 30 日間に販売されたすべての製品の総商品価値。 GMV は、注文された数量に各製品の基本価格を掛けたものと定義されます。 |
| `% GMV (Past 30 Days) Refunded` | 過去 30 日間に購入され、払い戻しが行われた製品の GMV の割合。 |
| `Product Quantity Ordered (Past 30 Days)` | 過去 30 日間に注文された品目の合計数量。 |
| `% Purchased Products (Past 30 Days) Refunded` | 過去 30 日間に購入し、払い戻しにつながった品目の割合。 |
| `Gross Merchandise Value` | すべての販売製品の総商品価値（月別）。 GMV は、注文された数量に各製品の基本価格を掛けたものと定義されます。 |
| `Purchases vs Refund Rate per Product (Past 30 Days)` | 各製品について、過去 30 日間に注文された合計数と返金された割合の比較。 各バブルのサイズは払い戻し率を表します。 |
| `Product Performance Details (Past 30 Days)` | 過去 30 日間の売上高とその後の返金に関する詳細情報（製品 SKU および製品名別）。 |
| `Top Purchased Products by GMV (Past 30 Days)` | 過去 30 日間に販売された製品のうち、最も多くの売上高（上位 10 件）。 |
| `Top Refunded Products by GMV (Past 30 Days)` | 過去 30 日間に購入された製品で、払い戻しによって最も GMV が失われた製品（上位 10 位）。 |
| `Top Purchased Products by Quantity (Past 30 Days)` | 過去 30 日間に販売された製品が最も多い（上位 10 件）。 |
| `Top Refunded Products by Quantity (Past 30 Days)` | 過去 30 日間に購入され、最大の払い戻し数量（上位 10 件）になった製品。 |
