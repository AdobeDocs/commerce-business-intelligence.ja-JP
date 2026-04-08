---
title: Enterprise_Rma_Item_Entity テーブル
description: 特定の項目に関する情報を、リクエストされた返品から分析する方法を説明します。
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/jBMtEluq3XNIzItebuvDQ43PAuW6mAsyG7RkHn8URJ4
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 08a466710b782238003c6bdb8cefacd07134291c
workflow-type: tm+mt
source-wordcount: 269
ht-degree: 0%

---

# enterprise_rma_item_entity テーブル

`enterprise_rma_item_entity` テーブルの各行（Commerce 2.xでは`magento_rma_item_entity`と呼ばれることが多いですが、名前はカスタマイズできます）には、リクエストされたリターンの特定の項目に関する情報が含まれています。

>[!NOTE]
>
>このテーブルは、`Enterprise Edition`または`Enterprise Cloud Edition`のお客様の場合にのみ、Commerce アカウントに標準で用意されています。

## 共通のネイティブ列

| **列名** | **説明** |
|---|---|
| `entity_id` | テーブルの一意のID。 各`entity_id`は、返品をリクエストされたアイテムを表します。 |
| `rma_entity_id` | `enterprise_rma` テーブルに関連付けられている外部キー。 |
| `status` | アイテムの返品のステータス。 値には、「received」、「pending」、「authorized」などがあります。 このステータスの値は、全体的なリターンのステータスの値と一致しない場合があります。 |
| `qty_requested` | 顧客が返品を要求する数量。 |
| `qty_approved` | 返品用に承認された数量。 |
| `qty_returned` | 返された数量。 |
| `order_item_id` | `sales_flat_order_item` テーブルに関連付けられている外部キー。 |
| `product_sku` | 返されるSKU。 |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Return date_requested` | これは、お客様が返品をリクエストした日付です。 |
| `Item price` | 商品の価格。 |
| `Return item's total value (qty_returned * price)` | これは、返されるアイテムの合計金額です。 これは、`enterprise_rma` テーブルの合計返品額を計算するために使用されます。 |

{style="table-layout:auto"}

## 共通指標

| **指標の名前** | **説明** | **建設** |
|---|---|---|
| `Number of items returned` | 返されるアイテムの数。 | 操作列：返された数量<br>操作：合計<br> タイムスタンプ列：要求日 |
| `Returned items' total value` | 返済金額です。 | 操作列：返品品目の合計値（返品数*価格） <br>操作：合計<br> タイムスタンプ列：返品日がリクエストされました |

{style="table-layout:auto"}

## 他のテーブルへの接続

`enterprise_rma`

* 次の結合を使用して、`Return date_requested` テーブルの`enterprise_rma_item_entity`などの結合された列を作成します。
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` （多数） => `enterprise_rma.entity_id` （1つ）
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` （多数） => `magento_rma.entity_id` （1つ）

`sales_flat_order_item`

* 上に結合列を作成  次の結合を使用した`enterprise_rma_item_entity` テーブル：

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` （多数） => `sales_flat_order_item.item_id` （1つ）
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` （多数） => `sales_order_item.item_id` （1つ）
