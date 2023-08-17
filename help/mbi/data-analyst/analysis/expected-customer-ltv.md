---
title: Pro 向けの期待されるライフタイム値 (LTV) 分析
description: 顧客のライフタイムバリューの増加と、顧客の予想されるライフタイムバリューを理解するのに役立つダッシュボードを設定する方法を説明します。
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# ライフタイム値の予測分析

このトピックでは、顧客のライフタイム値の増加と、顧客の予想されるライフタイム値を把握できるダッシュボードを設定する方法について説明します。

![](../../assets/exp-lifetim-value-anyalysis.png)

この分析は、Pro アカウントのお客様が新しいアーキテクチャでのみ利用できます。 アカウントが `Persistent Views` の下の特集 `Manage Data` サイドバーを使用すると、新しいアーキテクチャに移行し、ここに示す手順に従って自分でこの分析を構築できます。

使用を開始する前に、 [コホートレポートビルダー。](../dev-reports/cohort-rpt-bldr.md)

## 計算列

に作成する列 **注文件数** 使用する場合はテーブル **30 日間**:

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
* 定義： `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

に作成する列 **`orders`** 使用する場合はテーブル **カレンダー** 月：

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
* [!UICONTROL Column input]: A = `created_at`
* 
  [!UICONTROL Datatype]: `String`
* 定義： `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## 指標

### 指標の説明

作成する指標

* **初回注文日別のユニーク顧客**
   * ゲストによる注文を有効にする場合は、 `customer_email`

* Adobe Analytics の **`orders`** 表
* この指標では **個別の値をカウント**
* 次の日： **`customer_id`** 列
* 並べ替え元 **`Customer's first order date`** timestamp

>[!NOTE]
>
>必ず [すべての新しい列を指標のディメンションとして追加](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に。

## レポート

### レポートの手順

**月別の顧客あたりの予想収益**

* 指標 `A`: `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` （X の妥当な数を 24 か月などで選択）
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
* [!UICONTROL Group by]: `Calendar months between first order and this order`  — すべてを表示
* 次を変更： `group by` （の） `All time customers` 非依存指標は、 `group by`
* を編集します。 `Show top/bottom` フィールドには次の情報が含まれます。
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**コホート別の月別平均売上高**

* 指標 `A`: `Revenue`
* 
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**コホート別の月別の累積平均売上高**

* 指標 `A`: `Revenue`
* 
  [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

すべてのレポートをコンパイルした後、必要に応じてダッシュボードで整理できます。 結果は、ページ上部の画像のようになる場合があります。

この分析の構築中に質問が発生した場合、または単に Professional Services チームを引き付けたい場合は、 [連絡先サポート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
