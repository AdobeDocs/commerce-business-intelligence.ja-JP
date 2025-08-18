---
title: enterprise_rma 表
description: 特定の再来訪リクエストに関する情報を分析する方法を説明します。
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 0%

---

# enterprise_rma 表

`enterprise_rma` テーブルの各行（Adobe Commerce 2.x では `magento_rma` と呼ばれることが多いですが、名前はカスタマイズできます）には、特定の返しリクエストに関する情報が含まれます。

>[!NOTE]
>
>この表は、`Enterprise Edition` またはお客様の場合、お使いのAdobe Commerce アカウントに標準で付属して `Enterprise Cloud Edition` ます。

## 共通ネイティブ列

| **列名** | **説明** |
|---|---|
| `entity\_id` | テーブルの一意の識別子。 各リク `entity\_id` ストはリターンリクエストを表します。 |
| `date\_requested` | 返品がリクエストされた日付。 |
| `status` | 返品のステータス。 値には「received」、「pending」、「authorized」などがあります。 |
| `order\_id` | `sales\_flat\_order` テーブルに関連付けられている外部キー。 |
| `customer\_id` | `customer\_entity` テーブルに関連付けられている外部キー。 |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Order's created\_at` | これは元の注文の日付です。 これを使用して、注文から返品要求までの時間を取得できます。 |
| `Customer's order number` | これは、元の注文に関連付けられた顧客の注文番号です。 |
| `Seconds between order's created\_at and return's date\_requested` | 注文日から返品要求までの秒数。 |
| `Return's total value` | これは、返される合計金額です。 これは、各返品品目の個々の返品金額の合計です。 |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **建設** |
|---|---|---|
| `Number of returns` | リクエストされた戻り値の数。 | `Operation` 列：`entity id`<br>`Operation`: `Count`<br>`Timestamp` 列：`date requested` |
| `Total returned amount` | 返される合計金額。 | `Operation ` 列：`Return's total value`<br>`Operation`：合計 <br>`Timestamp` 列：リクエストされた日付 |
| `Average returned amount` | 返される平均金額。 | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` 列：`date requested` |
| `Average time to return` | 注文から返品までの平均時間。 | `Operation` 列：で作成された注文からリクエストされた返品日までの秒数 <br>`Operation`: `Average`<br>`Timestamp` 列：`date requested` |

{style="table-layout:auto"}

## その他のテーブルへの接続

`sale_flat_order`

* セグメント化する結合列を作成し、次の結合を使用して、`enterprise_rma` テーブルの注文レベルの属性でフィルタリングします。
   * Commerce 1.x: `enterprise_rma.order_id` （多） => `sales_flat_order.entity_id` （1）
   * Commerce 2.x: `magento_rma.order_id` （多） => `sales_order.entity_id` （1）

`enterprise_rma_item_entity`

* 次の結合を使用して、`Return's total value` テーブルに `enterprise_rma` などの多対 1 列を作成します。
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` （多） => `enterprise_rma.entity_id` （1）
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` （多） => `magento_rma.entity_id` （1）
