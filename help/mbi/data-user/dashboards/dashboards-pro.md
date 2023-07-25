---
title: 標準のダッシュボード
description: ビジネスを把握するための標準のダッシュボードについて説明します。
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 0%

---

# 標準のダッシュボード

[!DNL Adobe Commerce Intelligence] には、ビジネスを分析するための標準ダッシュボードが含まれています。 ダッシュボードを使用すると、ユーザーの全期間の売上高、再購入回数、特定の期間に購入された上位の製品など、重要な指標の状態を確認できます。 事前設定済みのこれらのダッシュボードは、十分な情報に基づいてビジネス上の意思決定をおこなえるように作成されています。

>[!NOTE]
>
>これらのダッシュボードへのアクセスは、アカウントのタイプとアクセスレベルによって異なります。 これらのダッシュボードが表示されない場合は、 [サポート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## レポートの可用性

の `Customers` および `Executive Summary` ダッシュボードの場合、一部のレポートは、ストアのチェックアウト設定によってのみ使用できます。 特に、ストアがゲストによるチェックアウトを許可している場合や、ゲストによるチェックアウトを許可していない場合は、

## 顧客（ゲストによるチェックアウトが許可されました）

「顧客（ゲストによるチェックアウトが許可されました） 」ダッシュボードには、購入行動など、顧客ベースに関する情報が表示されます。 このダッシュボードは、顧客維持を改善し、最も高い売上高をもたらす顧客を判断するのに役立ちます。

### レポート

| 名前 | 説明 |
|---|---|
| `Orders by New Customers (Past 30 Days)` | 過去 30 日間に一度も注文したことのない顧客からの注文。 |
| `Orders by Existing Customers (Past 30 Days)` | 過去 30 日間に 1 つ以上の注文をした顧客からの注文。 |
| `Total Unique Customers (Past 30 Days)` | 過去 30 日間に注文をしたユニーク顧客の数。 |
| `Orders by New vs Existing Customers` | 1 つ以上の前の注文を持つ顧客に対する、以前の注文を持たない顧客による注文数。 |
| `Subsequent Order Probability (All Time)` | 注文をした顧客が別の顧客を発注する可能性。 |
| `% of Customers with Multiple Orders (All Time)` | 複数の注文をしたすべての顧客の割合。 |
| `Median Time Between Orders (All Time)` | 各顧客が 1 回の注文から次の注文までに要する時間の中央値。 |
| `Subsequent Order Probability` | 注文をした顧客が別の注文を行う可能性。注文番号別に分類されます。 つまり、1 つの注文で 2 つ目の注文をした顧客の割合、2 つ目の注文で 3 つ目の注文をした顧客の割合などです。 |
| `Time Between Orders` | 顧客が注文間で取る平均時間と中央値（注文回数別に分類した、注文 1 ～ 2 、 2 、 3 などの間の時間）。 |
| `Number of Customers - Lifetime Orders` | 顧客の全期間において、所定の数の注文に対して、その数の注文をした顧客の数と、その数が表す顧客ベース全体の割合。 |
| `One-Time Customers who Bought 3-6 Months Ago` | 3 ～ 6 ヶ月前に初めて購入したお客様。 |
| `Avg LTV by First Order` | コホート全体での顧客のライフタイムの累積平均売上高を比較します。 コホートは、顧客が最初に購入した月によって定義されます。 例： `Jan 2020` コホートは、2020 年 1 月に初めて購入した顧客の累積平均 LTV を表示します。 |
| `Customer's First 30 Day vs Lifetime Revenue` | 初回購入後 30 日間の顧客の平均売上高と全期間の平均売上高の比較。 各バブルは出荷地域に対応し、各バブルのサイズはその地域から取得した顧客数を表します。 |

## 顧客（ゲストによるチェックアウトは許可されていません）

「顧客（ゲストによるチェックアウトは許可されていません） 」ダッシュボードは、購入行動や、アカウント登録から注文プレースメントへのコンバージョンなど、顧客ベースに関する情報を提供します。 このダッシュボードは、顧客維持を改善し、最も高い売上高をもたらす顧客を判断するのに役立ちます。

### レポート

| 名前 | 説明 |
|---|---|
| `Account Registration (Past 30 Days)` | 過去 30 日間にストアにアカウントで登録した人の数です。 |
| `Accounts Registered (Past 30 Days) with 1 or More Orders` | 過去 30 日間にストアにアカウントで登録し、少なくとも 1 回の注文を行った人の数です。 |
| `% Conversion from Registration to First Order (Past 30 Days)` | 過去 30 日間に登録され、注文をしたアカウントの割合。 |
| `% Conversion from Registration to First Order` | 注文をした登録口座の割合（登録月単位）。 |
| `Orders by New vs Existing Customers` | 1 つ以上の前の注文を持つ顧客に対する、以前の注文を持たない顧客による注文数。 |
| `Subsequent Order Probability (All Time)` | 注文をした顧客が別の顧客を発注する可能性。 |
| `% of Customers with Multiple Orders (All Time)` | 複数の注文をしたすべての顧客の割合。 |
| `Median Time Between Orders (All Time)` | 各顧客が 1 回の注文から次の注文までに要する時間の中央値。 |
| `Subsequent Order Probability` | 注文をした顧客が別の注文を配置する可能性（注文番号別）。 つまり、1 回の注文で 2 回目の注文をした顧客の割合、2 回目の注文で 3 回目の注文をした顧客の割合などです。 |
| `Time Between Orders` | 顧客が注文間で取る平均時間と中央値（注文回数別に分類した、注文 1 ～ 2 、 2 、 3 などの間の時間）。 |
| `Number of Customers - Lifetime Orders` | 顧客の全期間において、所定の数の注文に対して、その数の注文をした顧客の数と、その数が表す顧客ベース全体の割合。 |
| `One-Time Customers who Bought 3-6 Months Ago` | 3 ～ 6 ヶ月前に初めて購入したお客様。 |
| `Avg LTV by First Order` | コホート全体での顧客のライフタイムの累積平均売上高を比較します。 コホートは、顧客が最初に購入した月によって定義されます。 例えば、2020 年 1 月コホートでは、2020 年 1 月に初めて購入した顧客の累積平均 LTV が表示されます。 |
| `Customer's First 30 Day vs Lifetime Revenue` | 初回購入後 30 日間の顧客の平均売上高と全期間の平均売上高の比較。 各バブルは出荷地域に対応し、各バブルのサイズはその地域から取得した顧客数を表します。 |

## エグゼクティブサマリ（ゲストのチェックアウトが許可されます）

エグゼクティブサマリ（ゲストによるチェックアウトが許可された）ダッシュボードには、注文件数と売上高の観点でのビジネスの状況が簡単に表示されます。 このダッシュボードは、経営陣がビジネスパフォーマンスを全体的に把握できるように設計されていますが、他の人にとっても見識がある場合があります。

### レポート

| 名前 | 説明 |
|---|---|
| `Revenue (Current Month)` | 現在の月に対してストアが生み出した売上高。 この場合、売上高は、注文で顧客が支払う最終価格と定義されます。 |
| `Revenue (Past 6 Months by Day)` | 合計日別売上高。過去 7 日間の平均日別売上高が重ねて表示されます。 この場合、売上高は、注文で顧客が支払う最終価格と定義されます。 |
| `% Change in Revenue (MoM MTD)` | 今月（これまで）の売上高と前月の同じ部分の売上高の比較。 |
| `Revenue from New vs Existing Customers (Current Month)` | 新規（初回）の顧客と既存の顧客（2 回目以降の注文）との比較に基づく当月（現在まで）の売上高。 |
| `Average Order Value (Current Month)` | 今月（これまで）に発行された注文の日平均値。 注文額は、注文に関して顧客が支払う最終価格として定義されます。 |
| `Orders (Current Month)` | 今月（現在まで）にストアでおこなわれた注文数。 |
| `% Change in Orders (MoM MTD)` | 今月（これまで）と前月の同じ部分の注文件数の比較。 |
| `Orders by New Customers (Current Month)` | 以前に注文したことのない顧客からの今月の注文。 |
| `Orders by Existing Customers (Current Month)` | 以前に 1 つ以上の注文をした顧客からの今月の注文。 |
| `Orders by New vs Existing Customers (Current Year by Week)` | 現在の年の各週（現在まで）に対する、以前の注文がない顧客別の注文数と、前の注文が少なくとも 1 つある顧客別の注文数。 |

## エグゼクティブサマリ（ゲストによるチェックアウトは許可されていません）

エグゼクティブサマリ（ゲストによるチェックアウトは許可されていません）ダッシュボードには、注文件数、売上高、アカウント登録数の観点から、ビジネスがどのように行われているかを簡単に示します。 このダッシュボードは、経営陣がビジネスパフォーマンスを全体的に把握できるように設計されていますが、他の人にとっても見識がある場合があります。

### レポート

| 名前 | 説明 |
|---|---|
| `Revenue (Current Month)` | 今月にストアによって生み出された売上高。 この場合、売上高は、注文で顧客が支払う最終価格と定義されます。 |
| `Revenue (Past 6 Months by Day)` | 合計日別売上高。過去 7 日間の平均日別売上高が重ねて表示されます。 この場合、売上高は、注文で顧客が支払う最終価格と定義されます。 |
| `% Change in Revenue (MoM MTD)` | 今月までの売上高と前月の同じ部分の比較。 |
| `Revenue from New vs Existing Customers (Current Month)` | 新規（初回）の顧客と既存の顧客（2 回目以降の注文）との比較に基づく当月（現在まで）の売上高。 |
| `Average Order Value (Current Month)` | 今月（これまで）に発行された注文の日平均値。 注文額は、注文に関して顧客が支払う最終価格として定義されます。 |
| `Orders (Current Month)` | 今月（現在まで）にストアでおこなわれた注文数。 |
| `% Change in Orders (MoM MTD)` | 今月（これまで）と前月の同じ部分の注文件数の比較。 |
| `Account Registrations (Current Month)` | 今月までに新規登録されたアカウントの数。 |
| `% Conversion from Registration to First Order (Current Month)` | 今月までに登録し、注文をした口座の割合。 |
| `% Conversion from Registration to First Order (Current Year by Week)` | 今年に入って以来、毎週登録している、注文をした口座の割合。 |

## 注文

注文ダッシュボードは、注文のトランザクション数量、そのステータス、使用したクーポンコード、生成された売上高、使用した支払い方法に関するインサイトを提供します。 たとえば、達成プロセスを追跡し、問題やボトルネックの発生がないことを確認できます。

>[!NOTE]
>
>このダッシュボードのレポートは、どちらのタイプの設定（ゲストによるチェックアウト、ゲストによるチェックアウトなし）でも、ストアに接続されているアカウントで使用できます。

### レポート

| 名前 | 説明 |
|---|---|
| `Orders (Past 30 Days)` | 過去 30 日間に店舗で発行された注文の数。 |
| `Revenue (Past 30 Days)` | 過去 30 日間にストアによって生み出された売上高。 売上高は、注文で顧客が支払った最終価格と定義されます。 |
| `Average Order Value (Past 30 Days)` | 過去 30 日間におこなわれた注文の平均値。 注文額は、注文に関して顧客が支払う最終価格として定義されます。 |
| `Orders` | 各月に店舗で行われた注文数。 |
| `Revenue by Payment Method` | 店舗によって生み出された売上高。支払い方法で分割されます。 売上高は、注文で顧客が支払った最終価格と定義されます。 |
| `AOV by New vs Existing Customers` | 店舗での注文件数の月平均値。以前の注文がない顧客の注文件数と、1 つ以上の前の注文を持つ顧客数で分割します。 注文額は、注文に関して顧客が支払う最終価格として定義されます。 |
| `% Orders by Status (Past 30 Days)` | 過去 30 日間の各日からの、現在各注文ステータスの注文の割合。 |
| `Incomplete Orders (Created more than 1 Day Ago)` | 1 日以上前に配置された、未完了ステータス（キャンセルまたは完了ではない）のすべてのオーダーのリスト。 |
| `Orders Per Hour (Past 7 Days)` | 1 日ごとの注文量。 |
| `Revenue Details (Past 30 Days)` | 過去 30 日間の日別の売上高を、合計売上高値のすべてのコンポーネントに分類します。 |
| `Order Details by Coupon Code (Past 30 Days)` | 店舗が提供する各クーポンコードについて、そのクーポンコードの使用方法と、過去 30 日間にどのような利益をもたらしたかに関する詳細が表示されます。 |
| `% Orders with Coupon (Past 30 Days)` | 過去 30 日間にクーポンを使用した注文の割合と使用しなかった注文の割合。 |

## 製品

「製品」ダッシュボードには、注文した製品、GMV(Gross Murchandise Value)、購入および返金されたトップ製品に関する一般的な製品パフォーマンスが表示されます。 購入と返品のバランスを取り、製品の成功と人気度を判断するのに役立ちます。 ストアは [払い戻しを追跡するように設定されている](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html) を設定します。

>[!NOTE]
>
>このダッシュボードのレポートは、どちらのタイプの設定（ゲストによるチェックアウト、ゲストによるチェックアウトなし）でも、ストアに接続されているアカウントで使用できます。

### レポート

| 名前 | 説明 |
|---|---|
| `GMV (Past 30 Days)` | 過去 30 日間に販売されたすべての製品の総商品価値。 GMV は、注文された数量に各製品の基本価格を掛けた値として定義されます。 |
| `% GMV (Past 30 Days) Refunded` | 過去 30 日間に購入された製品の GMV の割合（返金に至った結果）。 |
| `Product Quantity Ordered (Past 30 Days)` | 過去 30 日間に注文された品目の合計数。 |
| `% Purchased Products (Past 30 Days) Refunded` | 過去 30 日間に購入された品目の割合（返金に至ったもの）。 |
| `Gross Merchandise Value` | 月別に販売されたすべての製品の総商品価格。 GMV は、注文された数量に各製品の基本価格を掛けた値として定義されます。 |
| `Purchases vs Refund Rate per Product (Past 30 Days)` | 各製品について、過去 30 日間に注文された合計数と、製品の払い戻し率の比較を示します。 各バブルのサイズは返金率を表します。 |
| `Product Performance Details (Past 30 Days)` | 過去 30 日間の売上高とその後の返金に関する詳細（製品 sku および製品名別）。 |
| `Top Purchased Products by GMV (Past 30 Days)` | 過去 30 日間に販売された製品で最も高い売上高（上位 10）をもたらした。 |
| `Top Refunded Products by GMV (Past 30 Days)` | 過去 30 日間に購入された製品は、払い戻し（上位 10 件）によって最も多くの GMV が失われました。 |
| `Top Purchased Products by Quantity (Past 30 Days)` | 過去 30 日間に最も多く販売された製品（上位 10）。 |
| `Top Refunded Products by Quantity (Past 30 Days)` | 過去 30 日間に購入した製品の払い戻し量が最も多い（上位 10）。 |
