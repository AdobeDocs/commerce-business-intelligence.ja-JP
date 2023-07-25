---
title: enterprise_rma 表
description: 特定のリターンリクエストに関する情報を分析する方法を説明します。
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# enterprise_rma 表

各行 ( `enterprise_rma` テーブル ( `magento_rma` Adobe Commerce 2.x では（名前はカスタマイズ可能）、特定の返却リクエストに関する情報が含まれます。

>[!NOTE]
>
>この表は、Adobe Commerceアカウントに標準で用意されている `Enterprise Edition` または `Enterprise Cloud Edition` 顧客。

## 共通のネイティブ列

| **列名** | **説明** |
|---|---|
| `entity\_id` | テーブルの一意の ID。 各 `entity\_id` は、戻り値のリクエストを表します。 |
| `date\_requested` | 返品がリクエストされた日付。 |
| `status` | リターンのステータス。 値には、「received」、「pending」、「authorized」などが含まれます。 |
| `order\_id` | に関連付けられた外部キー `sales\_flat\_order` 表。 |
| `customer\_id` | に関連付けられた外部キー `customer\_entity` 表。 |

{style="table-layout:auto"}

## 共通の計算列

| **列名** | **説明** |
|---|---|
| `Order's created\_at` | これは元の注文日です。 これは、注文から返品リクエストまでの時間を取得するために使用できます。 |
| `Customer's order number` | これは、元の注文に関連付けられた顧客の注文番号です。 |
| `Seconds between order's created\_at and return's date\_requested` | 注文日から返品リクエストまでの秒数。 |
| `Return's total value` | これは、返却される合計金額です。 各返品品目の個々の返品額の合計です。 |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **構築** |
|---|---|---|
| `Number of returns` | リクエストされた返品数。 | `Operation` 列： `entity id`<br>`Operation`: `Count`<br>`Timestamp` 列： `date requested` |
| `Total returned amount` | 返された金額の合計です。 | `Operation `列： `Return's total value`<br>`Operation`:合計<br>`Timestamp` 列：リクエスト日 |
| `Average returned amount` | 返された平均金額。 | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` 列： `date requested` |
| `Average time to return` | 注文から返品までの平均時間。 | `Operation` 列：注文が作成されてからリターンがリクエストされた日までの秒数<br>`Operation`: `Average`<br>`Timestamp` 列： `date requested` |

{style="table-layout:auto"}

## 他のテーブルへの接続

`sale_flat_order`

* 結合された列を作成して、 `enterprise_rma` 次の結合を使用したテーブル：
   * Commerce 1.x: `enterprise_rma.order_id` （多数） => `sales_flat_order.entity_id` (1)
   * Commerce 2.x: `magento_rma.order_id` （多数） => `sales_order.entity_id` (1)

`enterprise_rma_item_entity`

* 次のような多対 1 の列を作成 `Return's total value` の `enterprise_rma` 次の結合を使用したテーブル：
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` （多数） => `enterprise_rma.entity_id` (1)
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` （多数） => `magento_rma.entity_id` (1)
