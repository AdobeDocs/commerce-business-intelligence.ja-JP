---
title: enterprise_rma テーブル
description: 特定の返品リクエストに関する情報を分析する方法について説明します。
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/ofPlk5xNr8aspjFlpzEtDtjcOPm9DrQFYX9-vPDfK6w
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 0%

---

# enterprise_rma テーブル

`enterprise_rma` テーブルの各行（Adobe Commerce 2.xでは`magento_rma`と呼ばれることが多いですが、名前はカスタマイズできます）には、特定のリターンリクエストに関する情報が含まれています。

>[!NOTE]
>
>このテーブルは、`Enterprise Edition`または`Enterprise Cloud Edition`のお客様の場合にのみ、Adobe Commerce アカウントに標準で用意されています。

## 共通のネイティブ列

| **列名** | **説明** |
|---|---|
| `entity\_id` | テーブルの一意のID。 各`entity\_id`は返品要求を表します。 |
| `date\_requested` | 返品がリクエストされた日付。 |
| `status` | 返品のステータス。 値には、「received」、「pending」、「authorized」などがあります。 |
| `order\_id` | `sales\_flat\_order` テーブルに関連付けられている外部キー。 |
| `customer\_id` | `customer\_entity` テーブルに関連付けられている外部キー。 |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Order's created\_at` | これは元の注文の日付です。 これは、注文と返品要求の間の時間を取得するために使用できます。 |
| `Customer's order number` | これは、元の注文に関連付けられている顧客の注文番号です。 |
| `Seconds between order's created\_at and return's date\_requested` | 注文日から返品要求までの秒数。 |
| `Return's total value` | これは、返される金額の合計です。 これは、各返品項目の個々の返品額の合計です。 |

{style="table-layout:auto"}

## 共通指標

| **指標の名前** | **説明** | **建設** |
|---|---|---|
| `Number of returns` | リクエストされた返品数。 | `Operation`列：`entity id`<br>`Operation`: `Count`<br>`Timestamp`列：`date requested` |
| `Total returned amount` | 返された金額の合計。 | `Operation `列：`Return's total value`<br>`Operation`：合計<br>`Timestamp`列：要求日 |
| `Average returned amount` | 返された金額の平均。 | `Operation` ` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp`列：`date requested` |
| `Average time to return` | 注文から返品までの平均時間。 | `Operation`列：注文の作成日から返品日までの秒数が要求された日<br>`Operation`: `Average`<br>`Timestamp`列：`date requested` |

{style="table-layout:auto"}

## 他のテーブルへの接続

`sale_flat_order`

* 結合された列を作成して、次の結合を介して`enterprise_rma` テーブルの注文レベルの属性でセグメント化およびフィルタリングします。
   * Commerce 1.x: `enterprise_rma.order_id` （多数） => `sales_flat_order.entity_id` （1つ）
   * Commerce 2.x: `magento_rma.order_id` （多数） => `sales_order.entity_id` （1つ）

`enterprise_rma_item_entity`

* 次の結合を使用して、`Return's total value` テーブルの`enterprise_rma`などの多対一の列を作成します。
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` （多数） => `enterprise_rma.entity_id` （1つ）
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` （多数） => `magento_rma.entity_id` （1つ）
