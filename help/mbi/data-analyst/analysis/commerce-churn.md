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

このトピックでは、の計算方法を示します **チャーンレート** の場合 **コマース顧客**. SaaS や従来のサブスクリプション企業とは異なり、コマース顧客は通常、具体的な情報を持っていません **&quot;チャーンイベント&quot;** アクティブな顧客にカウントされなくなったことを示します。 このため、以下の手順を使用すると、最後の注文以降に決定された経過時間に基づいて、顧客を「チャーン」として定義できます。

![](../../assets/Churn_rate_image.png)

多くのお客様は、何を概念化し始めるうえで支援を必要としています。 **期間** データに基づいてを使用する必要があります。 過去の顧客行動を使用してこれを定義する場合 **チャーン期間**&#x200B;を参照してください。次のことをよく理解している必要があります [チャーンの定義](../analysis/define-cust-churn.md) トピック。 次に、以下の手順で、チャーンレートの数式の結果を使用できます。

## 計算される列

作成する列

* **`customer_entity`** テーブル
* **`Customer's last order date`**
   * を選択 [!UICONTROL definition]: `Max`
   * を選択 [!UICONTROL table]: `sales_flat_order`
   * を選択 [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * を選択 [!UICONTROL definition]: `Age`
   * を選択 [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>必ずしてください [すべての新規列をディメンションとして指標に追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に、

## 指標

* **新規顧客（初回注文日別）**
   * カウントされる顧客

>[!NOTE]
>
>この指標は、お使いのアカウントに存在する可能性があります。

* が含まれる **`customer_entity`** テーブル
* このメトリックは、 **カウント**
* 日 **`entity_id`** 列
* による並べ替え **`Customer's first order date`** timestamp
* [!UICONTROL Filter]:

* **新規顧客（前回の注文日別）**
   * カウントされる顧客

  >[!NOTE]
  >
  >この指標は、お使いのアカウントに存在する可能性があります。

* が含まれる **`customer_entity`** テーブル
* このメトリックは、 **カウント**
* 日 **`entity_id`** 列
* による並べ替え **`Customer's last order date`** timestamp
* [!UICONTROL Filter]:

>[!NOTE]
>
>必ずしてください [すべての新規列をディメンションとして指標に追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に、

## レポート

* **チャーンレート**
   * [!UICONTROL Metric]：新規顧客（初回注文日別）
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
     [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * 顧客の最終注文日からの経過時間（秒） >= [チャーンされた顧客に対する自己定義のカットオフ&#x200B;]**`^`**
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

以下は、一般的な月/2 回目のコンバージョンの一部ですが、google では、探しているカスタム値の週/秒コンバージョンなど、他の値を提供しています。

| **か月** | **秒** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

すべてのレポートをコンパイルした後、必要に応じてダッシュボード上で整理できます。 結果は、上記のサンプルダッシュボードのようになります。
