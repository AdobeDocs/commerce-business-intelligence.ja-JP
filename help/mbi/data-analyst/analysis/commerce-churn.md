---
title: Commerceチャーン
description: Commerceのチャーンレートを生成して分析する方法を説明します。
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# チャーンレート

このトピックでは、**コマース顧客** の **チャーンレート** を計算する方法を説明します。 SaaS や従来のサブスクリプション企業とは異なり、コマース顧客は通常、アクティブな顧客をカウントすべきではないことを示すために **具体的な** 「チャーンイベント」を持っていません。 このため、以下の手順を使用すると、最後の注文以降に決定された経過時間に基づいて、顧客を「チャーン」として定義できます。

![](../../assets/Churn_rate_image.png)

多くのお客様は、データに基づいて、使用する **期間** を概念化し始める際に支援を必要としています。 過去の顧客の行動を使用してこの **チャーン期間** を定義する場合は、「チャーンの定義 [ に関するトピックを熟知してい ](../analysis/define-cust-churn.md) 必要があります。 次に、以下の手順で、チャーンレートの数式の結果を使用できます。

## 計算される列

作成する列

* **`customer_entity`** テーブル
* **`Customer's last order date`**
   * [!UICONTROL definition] を選択：`Max`
   * [!UICONTROL table] を選択：`sales_flat_order`
   * [!UICONTROL column] を選択：`created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * [!UICONTROL definition] を選択：`Age`
   * [!UICONTROL column] を選択：`Customer's last order date`

>[!NOTE]
>
>新しいレポートを作成する前に、必ず [ すべての新しい列をディメンションとして指標に追加する ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) ようにしてください。

## 指標

* **新規顧客（初回注文日別）**
   * カウントされる顧客

>[!NOTE]
>
>この指標は、お使いのアカウントに存在する可能性があります。

* **`customer_entity`** のテーブル内
* このメトリックは、**カウント** を実行します。
* **`entity_id`** 列
* **`Customer's first order date`** タイムスタンプで並べ替え
* [!UICONTROL Filter]:

* **新規顧客（最終注文日別）**
   * カウントされる顧客

  >[!NOTE]
  >
  >この指標は、お使いのアカウントに存在する可能性があります。

* **`customer_entity`** のテーブル内
* このメトリックは、**カウント** を実行します。
* **`entity_id`** 列
* **`Customer's last order date`** タイムスタンプで並べ替え
* [!UICONTROL Filter]:

>[!NOTE]
>
>新しいレポートを作成する前に、必ず [ すべての新しい列をディメンションとして指標に追加する ](../data-warehouse-mgr/manage-data-dimensions-metrics.md) ようにしてください。

## レポート

* **チャーンレート**
   * [!UICONTROL Metric]：新規顧客（初回注文日別）
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * &#x200B;

     [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * 顧客の最終注文日からの秒数 >= [ チャーンされた顧客の事前定義されたカットオフ ]&#x200B;**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * &#x200B;

     [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * &#x200B;

     [!UICONTROL Format]: Percentage

* *指標 `A`:`New customers cumulative`*
* *指標 `B`:`Churned customers by last order date`*
* *指標 `C`:`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

以下は、一般的な月/2 回目のコンバージョンの一部ですが、google では、探しているカスタム値の週/秒コンバージョンなど、他の値を提供しています。

| **月** | **秒** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

すべてのレポートをコンパイルした後、必要に応じてダッシュボード上で整理できます。 結果は、上記のサンプルダッシュボードのようになります。
