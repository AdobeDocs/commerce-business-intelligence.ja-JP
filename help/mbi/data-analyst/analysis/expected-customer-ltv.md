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

この分析は、新しいアーキテクチャの Pro アカウントのお客様のみが利用できます。 アカウントが `Persistent Views` サイドバーの `Manage Data` 機能にアクセスできる場合は、新しいアーキテクチャを使用しており、ここに記載されている手順に従って分析を自分で構築できます。

開始する前に、[ コホートレポートビルダー ](../dev-reports/cohort-rpt-bldr.md) を熟知しておく必要があります。

## 計算される列

**30 日の月** を使用する場合に、**orders** テーブルに作成する列：

* [!UICONTROL Column name]: `Months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `Seconds between customer's first order date and this order`
* 
  [!UICONTROL Datatype]: `Integer`
* **定義：**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]: `Months since order`
* [!UICONTROL Column type]: `Same Table`
* 
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* 
  [!UICONTROL Datatype]: `Integer`
* 定義：`case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

**`orders`** カレンダー **月を使用している場合、** テーブルに作成する列：

* [!UICONTROL Column name]: `Calendar months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
  [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs]:
   * `A` = `created_at`
   * `B` = `Customer's first order date`

* 
  [!UICONTROL Datatype]: `Integer`
* 定義：`case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

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
* [!UICONTROL Column input]: A = `created_at`
* 
  [!UICONTROL Datatype]: `String`
* 定義：`case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## 指標

### 指標の手順

作成する指標

* **初回注文日別のユニーク顧客**
   * ゲストによる注文を有効にする場合は、`customer_email` を使用します

* **`orders`** のテーブル内
* この指標は、「個別値のカウント **を実行します**
* **`customer_id`** 列
* **`Customer's first order date`** タイムスタンプで並べ替え

>[!NOTE]
>
>新しいレポートを作成する前に、必ず [ すべての新しい列をディメンションとして指標に追加する ](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) ようにしてください。

## レポート

### レポートの手順

**顧客ごとの月別収益予測**

* 指標 `A`: `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` （X に適した数値を選択してください。例：24 か月）
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
* 時間間隔：`None`
* [!UICONTROL Group by]: `Calendar months between first order and this order` – すべてを表示
* `group by` の横にある鉛筆アイコンを使用して、`All time customers` 指標の `group by` を「独立」に変更します
* `Show top/bottom` のフィールドを次のように編集します。
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

分析中に質問が発生した場合や、プロフェッショナルサービスチームに依頼したい場合は、[ サポートにお問い合わせください ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
