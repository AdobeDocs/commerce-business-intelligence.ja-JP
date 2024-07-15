---
title: 顧客集中度の定義
description: 合計売上高が顧客ベース間でどのように分配されるかを測定するのに役立つ、ダッシュボードの設定方法を説明します。
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# 顧客の集中

このトピックでは、合計売上高が顧客ベース間でどのように分配されるかを測定するのに役立つダッシュボードの設定方法を説明します。 顧客の何 % が売上高の何 % を貢献しているかを理解し、セグメント化されたリストを作成して最適なマーケットに送り、貢献の高い顧客を維持します。

この分析には [ 高度な計算列 ](../data-warehouse-mgr/adv-calc-columns.md) が含まれています。

## はじめに

まず、値が 1 のプライマリキーのみを含むファイルをアップロードする必要があります。 これにより、分析に必要な計算列を作成できます。

[ ファイルアップローダ ](../importing-data/connecting-data/using-file-uploader.md) と以下の画像を使用して、ファイルをフォーマットできます。

## 計算される列

元のアーキテクチャを使用している場合（例えば、`Manage Data` メニューに「`Data Warehouse Views`」オプションがない場合）、以下の列を作成するためにサポートチームに連絡します。 新しいアーキテクチャでは、`Manage Data > Data Warehouse` のページからこれらの列を作成できます。 詳細な手順は以下のとおりです。

ビジネスでゲストによる注文が許可されている場合は、さらに区別されます。 その場合は、`customer_entity` テーブルのすべてのステップを無視できます。 ゲストの注文が許可されていない場合は、`sales_flat_order` テーブルのすべてのステップを無視します。

作成する列

* `Sales_flat_order/customer_entity` テーブル
* （入力） `reference`
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `entity_id`
* [!UICONTROL Calculation]: - **A が null の場合は null、それ以外は 1 終了**
* [!UICONTROL Datatype]: - `Integer`

* `Customer concentration` テーブル （アップロードしたファイルに `1` という数字が付いています）
* 顧客の数
* [!UICONTROL Column type]: - `Many to One > Count Distinct`
* パス - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` または `customer_entity.(input)reference > Customer Concentration.Primary Key`
* 選択した列 – `sales_flat_order.customer_email` または `customer_entity.entity_id`

* `customer_entity` テーブル
* 顧客の数
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* パス - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* 選択した列 – `Number of customers`

* （入力） `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: - `Same table > Event Number`
* イベント所有者 – `Number of customers`
* イベントランク - `Customer's lifetime revenue`

* 顧客の売上高のパーセンタイル
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`、`Number of customers`
* [!UICONTROL Calculation]: - **A が null の場合は null、それ以外の場合は（A/B）* 100 end **
* [!UICONTROL Datatype]: - `Decimal`

* `Sales_flat_order` テーブル
* 顧客の数
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* パス - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* 選択した列 – `Number of customers`

* （入力）顧客の生涯売上高によるランキング
* [!UICONTROL Column type]: - `Same table > Event Number`
* イベント所有者 – `Number of customers`
* イベントのランク - `Customer's lifetime revenue`
* フィルター – `Customer's order number = 1`

* 顧客の売上高のパーセンタイル
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`、`Number of customers`
* [!UICONTROL Calculation]: - **A が null の場合は null、それ以外の場合は（A/B）* 100 end **
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>使用されるパーセンタイルは、顧客の偶数分割であり、顧客ベースの最大パーセンタイルを表します。 各顧客には 1 ～ 100 の整数が関連付けられており、これは生涯売上高 *ランク* と見なすことができます。 例えば、特定の顧客の売上高のパーセンタイルが **5** である場合、この顧客は、生涯売上高で見てすべての顧客の ***5 番目のパーセンタイル*** にあります。

## 指標

* **顧客のライフタイムバリューの合計**
* `customer_entity` のテーブル内
* このメトリックは **Sum** を実行します。
* `Customer's lifetime revenue` 列
* `Customer's first order date` タイムスタンプで並べ替え

## レポート

* **顧客集中度**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
  [!UICONTROL Group by]: `Independent`
* 指標 `A`: `Total customer lifetime revenue by percentile`
* 指標 `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* 上/下を表示：`100% of Customer's revenue percentile Name`
* 
  [!UICONTROL Chart type]: `Line`

* **上位 10% の濃度**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* 指標 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* グラフを非表示
* 
  [!UICONTROL Group by]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

* **1 回の購入で下位 50 % の集中**

* 指標 `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* グラフを非表示
* 
  [!UICONTROL Group by]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

* **下位 10% の濃度**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* 指標 `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL Interval]: `None`
* グラフを非表示
* 
  [!UICONTROL Group by]: `Email`
* 
  [!UICONTROL Chart type]: `Table`

すべてのレポートをコンパイルした後、必要に応じてダッシュボード上で整理できます。 結果は、上記のサンプルダッシュボードのようになります。

分析中に質問が発生した場合や、プロフェッショナルサービスチームに依頼したい場合は、[ サポートにお問い合わせください ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。
