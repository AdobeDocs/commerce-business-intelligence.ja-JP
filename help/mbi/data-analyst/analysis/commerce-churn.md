---
title: コマースチャーン
description: コマースチャーンレートを生成および分析する方法を説明します。
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# チャーンレート

このトピックでは、 **チャーンレート** の **コマース顧客**. SaaS や従来のサブスクリプション会社とは異なり、コマースの顧客は通常、具体的な **&quot;チャーンイベント&quot;** 顧客がアクティブな顧客にカウントされなくなることを示す このため、以下の手順では、最後の注文からの経過時間が決まったので、顧客を「チャーン」として定義できます。

![](../../assets/Churn_rate_image.png)

多くのお客様は、何を概念化し始める際に、支援を必要としています **期間** データに基づいてを使用する必要があります。 顧客の過去の行動を使用して、 **チャーン期間**&#x200B;を使用する場合、 [チャーンの定義](../analysis/define-cust-churn.md) トピック。 次の手順で、チャーンレートに対する式の結果を使用できます。

## 計算列

作成する列

* **`customer_entity`** 表
* **`Customer's last order date`**
   * を選択します。 [!UICONTROL definition]: `Max`
   * 選択 [!UICONTROL table]: `sales_flat_order`
   * 選択 [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * を選択します。 [!UICONTROL definition]: `Age`
   * 選択 [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>必ず [すべての新しい列を指標のディメンションとして追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に。

## 指標

* **新規顧客（初回注文日別）**
   * カウントされる顧客

>[!NOTE]
>
>この指標は、お使いのアカウントに存在する場合があります。

* Adobe Analytics の **`customer_entity`** 表
* この指標では **カウント**
* 次の日： **`entity_id`** 列
* 並べ替え元 **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **新規顧客（最終注文日別）**
   * カウントされる顧客

  >[!NOTE]
  >
  >この指標は、お使いのアカウントに存在する場合があります。

* Adobe Analytics の **`customer_entity`** 表
* この指標では **カウント**
* 次の日： **`entity_id`** 列
* 並べ替え元 **`Customer's last order date`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>必ず [すべての新しい列を指標のディメンションとして追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に。

## レポート

* **チャーンレート**
   * [!UICONTROL Metric]：新規顧客（初回注文日別）
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
     [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * 顧客の最終注文日以降の経過秒数 >= [チャーン顧客に対する自己定義の期限&#x200B;]**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
     [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * 
     [!UICONTROL Format]: Percentage

* *指標 `A`:`New customers cumulative`*
* *指標 `B`:`Churned customers by last order date`*
* *指標 `C`:`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

以下には一般的な月/秒のコンバージョンがいくつかありますが、Google では、探しているカスタム値に対する週/秒のコンバージョンなど、他の値を提供しています。

| **か月** | **秒** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

すべてのレポートをコンパイルした後、必要に応じてダッシュボードで整理できます。 結果は、上記のサンプルダッシュボードのようになります。
