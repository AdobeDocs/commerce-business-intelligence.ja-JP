---
title: Proの期待生涯価値（LTV）分析
description: 顧客の生涯価値の増加と顧客の期待生涯価値を把握するためのダッシュボードの設定方法を説明します。
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: 4e01225a6bd285afbe988b9c24e07e2ea34649fc
workflow-type: tm+mt
source-wordcount: 318
ht-degree: 0%

---

# 期待される生涯価値分析

このトピックでは、顧客生涯価値の増加と顧客の期待生涯価値を把握するためのダッシュボードを設定する方法を示します。

![顧客価値の予測を表示する期待生涯価値分析ダッシュボード ](../../assets/exp-lifetim-value-anyalysis.png)

この分析は、新しいアーキテクチャのPro アカウントのお客様のみが利用できます。 アカウントが`Persistent Views` サイドバーの下の`Manage Data`機能にアクセスできる場合、新しいアーキテクチャに属しており、ここに記載されている手順に従ってこの分析を自分で構築できます。

開始する前に、[ コホートレポートビルダーについて理解しておきましょう。](../dev-reports/cohort-rpt-bldr.md)

## 予定列

**30日の月**&#x200B;を使用する場合に&#x200B;**orders** テーブルに作成する列：

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

**`orders`** カレンダー&#x200B;**か月を使用する場合に** テーブルに作成する列：

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

### 指標命令

作成する指標

* **最初の注文日別に顧客を区別**
   * ゲスト注文を有効にする場合は、`customer_email`を使用します

* **`orders`** テーブル内
* この指標は、**個の個体数**&#x200B;を実行します
* **`customer_id`**&#x200B;列
* **`Customer's first order date`** タイムスタンプで注文

>[!NOTE]
>
>新しいレポートを作成する前に、必ず[すべての新しい列を指標](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md)にディメンションとして追加してください。

## レポート

### レポートの手順

**1か月の顧客当たりの予想売上**

* 指標`A`: `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` （Xの妥当な数値（例：24か月）を選択してください）
   * `Is in current month?` = `No`

* 
  [!UICONTROL指標]: `Revenue`
* [!UICONTROL Filter]:

* 指標`B`: `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* 指標`C`: `All time customers by month since first order (hide)`
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
* [!UICONTROL Group by]: `Calendar months between first order and this order` – すべて表示
* `group by`の横にある鉛筆アイコンを使用して、`All time customers`指標の`group by`を「独立」に変更します
* `Show top/bottom` フィールドを次のように編集します。
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**コホート別の月間平均売上**

* 指標`A`: `Revenue`
* 
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**コホート別の月間累積平均売上高**

* 指標`A`: `Revenue`
* 
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

すべてのレポートをまとめた後、必要に応じてダッシュボード上でレポートを整理できます。 その結果、ページの上部に画像が表示されます。

この分析の構築中に質問が発生した場合、または単にプロフェッショナルサービスチームに連絡したい場合は、[ サポートにお問い合わせください](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
