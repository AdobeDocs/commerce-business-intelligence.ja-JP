---
title: Pro の期待生涯価値（LTV）分析
description: 顧客の生涯価値の成長と顧客の生涯期待値を理解するのに役立つ、ダッシュボードの設定方法を説明します。
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# ライフタイム値の期待分析

このトピックでは、顧客の生涯価値の成長と顧客の生涯期待値を理解するのに役立つ、ダッシュボードの設定方法を説明します。

![](../../assets/exp-lifetim-value-anyalysis.png)

この分析は、新しいアーキテクチャの Pro アカウントのお客様のみが利用できます。 アカウントがへのアクセス権を持っている場合 `Persistent Views` の下の機能 `Manage Data` サイドバーは、新しいアーキテクチャを使用しており、ここに記載されている手順に従って分析を自分で構築できます。

開始する前に、について理解しておく必要があります [コホート report builder.](../dev-reports/cohort-rpt-bldr.md)

## 計算される列

に作成する列 **注文件数** を使用している場合はテーブル **30 日間の月**:

* [!UICONTROL Column name]: `Months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]:A = `Seconds between customer's first order date and this order`
* 
  [!UICONTROL Datatype]: `Integer`
* **定義：**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]: `Months since order`
* [!UICONTROL Column type]: `Same Table`
* 
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]:A = `created_at`
* 
  [!UICONTROL Datatype]: `Integer`
* 定義： `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

に作成する列 **`orders`** を使用している場合はテーブル **カレンダー** 月数：

* [!UICONTROL Column name]: `Calendar months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs]:
   * `A` = `created_at`
   * `B` = `Customer's first order date`

* 
  [!UICONTROL Datatype]: `Integer`
* 定義： `case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

* [!UICONTROL Column name]: `Calendar months since order`
* [!UICONTROL Column type]: `Same Table`
* 
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: `A` = `created_at`
* 
  [!UICONTROL Datatype]: `Integer`
* **定義：**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name]: `Is in current month? (Yes/No)`
* [!UICONTROL Column type]: `Same Table`
* 
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]:A = `created_at`
* 
  [!UICONTROL Datatype]: `String`
* 定義： `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## 指標

### 指標の手順

作成する指標

* **初回注文日別のユニーク顧客**
   * ゲストによる注文を有効にする場合は、 `customer_email`

* が含まれる **`orders`** テーブル
* このメトリックは、 **個別の値をカウント**
* 日 **`customer_id`** 列
* による並べ替え **`Customer's first order date`** timestamp

>[!NOTE]
>
>必ずしてください [すべての新規列をディメンションとして指標に追加](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に、

## レポート

### レポートの手順

**顧客ごとの月別収益の予測**

* 指標 `A`: `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` （X に妥当な数を選択します。例：24 か月）
   * `Is in current month?` = `No`

* 
  [!UICONTROL 指標]: `Revenue`
* [!UICONTROL Filter]:

* 指標 `B`: `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* 指標 `C`: `All time customers by month since first order (hide)`
   * `Calendar months since order` `<= X`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Expected revenue`
* [!UICONTROL Formula]: `A / (B - C)`
* 
  [!UICONTROL Format]: `Currency`

その他のグラフの詳細

* [!UICONTROL Time period]: `All time`
* 時間間隔： `None`
* [!UICONTROL Group by]: `Calendar months between first order and this order`  – すべてを表示
* 変更： `group by` の場合 `All time customers` の横にある鉛筆アイコンを使用して、指標を「独立」に設定します。 `group by`
* を編集する `Show top/bottom` フィールドを次に示します。
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**コホート別の 1 か月あたりの平均売上高**

* 指標 `A`: `Revenue`
* 
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**コホート別の 1 か月あたりの累積平均売上高**

* 指標 `A`: `Revenue`
* 
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

すべてのレポートをコンパイルした後、必要に応じてダッシュボード上で整理できます。 結果は、ページ上部の画像のようになります。

分析中に質問が発生した場合、または単にプロフェッショナルサービスチームに依頼したい場合、 [サポートに連絡する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
