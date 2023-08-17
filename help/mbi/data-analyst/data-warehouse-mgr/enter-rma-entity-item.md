---
title: Enterprise_Rma_Item_Entity テーブル
description: リクエストされた返品から特定の品目に関する情報を分析する方法を説明します。
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 1%

---

# enterprise_rma_item_entity 表

各行 ( `enterprise_rma_item_entity` テーブル ( `magento_rma_item_entity` Commerce 2.x では、名前はカスタマイズ可能です )。リクエストされた返品に関する特定の項目に関する情報が含まれます。

>[!NOTE]
>
>このテーブルは、ユーザーが `Enterprise Edition` または `Enterprise Cloud Edition` 顧客。

## 共通のネイティブ列

| **列名** | **説明** |
|---|---|
| `entity\_id` | テーブルの一意の ID。 各 `entity\_id` は、返却をリクエストされた項目を表します。 |
| `rma\_entity\_id` | に関連付けられた外部キー `enterprise\_rma` 表。 |
| `status` | 品目の返品のステータス。 値には、「received」、「pending」、「authorized」などが含まれます。 このステータスの値は、戻り値全体のステータスの値と一致しない場合があります。 |
| `qty\_requested` | 顧客が返品を要求する数量。 |
| `qty\_approved` | 返品の承認済み数量。 |
| `qty\_returned` | 返された数量。 |
| `order\_item\_id` | に関連付けられた外部キー `sales\_flat\_order\_item` 表。 |
| `product\_sku` | 返される sku。 |

{style="table-layout:auto"}

## 共通の計算列

| **列名** | **説明** |
|---|---|
| `Return date\_requested` | 顧客が返品をリクエストした日付です。 |
| `Item price` | 品目の価格。 |
| `Return item's total value (qty\_returned * price)` | これは、返される項目の合計金額です。 これは、 `enterprise\_rma` 表。 |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **構築** |
|---|---|---|
| `Number of items returned` | 返される項目の数。 | 工程列：返品数量<br>操作：合計<br>タイムスタンプ列：リクエストされた返却日 |
| `Returned items' total value` | 返された金額。 | 工程列：返品品目の合計値（返品数量*価格）<br>操作：合計<br>タイムスタンプ列：リクエストされた返却日 |

{style="table-layout:auto"}

## 他のテーブルへの接続

`enterprise_rma`

* 結合された列（例： ）を作成します。 `Return date\_requested` の `enterprise_rma_item_entity` 次の結合を使用したテーブル：
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` （多数） => `enterprise_rma.entity_id` (1)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` （多数） => `magento_rma.entity_id` (1)

`sales_flat_order_item`

* で結合された列を作成  `enterprise_rma_item_entity` 次の結合を使用したテーブル：

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` （多数） => `sales_flat_order_item.item_id` (1)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` （多数） => `sales_order_item.item_id` (1)
