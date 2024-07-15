---
title: Enterprise_Rma_Item_Entity 表
description: 要求された返品から特定の品目に関する情報を分析する方法を説明します。
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# enterprise_rma_item_entity 表

`enterprise_rma_item_entity` テーブルの各行（Commerce 2.x では `magento_rma_item_entity` と呼ばれることが多いですが、名前はカスタマイズできます）には、要求されたリターンからの特定のアイテムに関する情報が含まれます。

>[!NOTE]
>
>この表は、`Enterprise Edition` またはお客様の場合、お使いのCommerce アカウントに標準で付属して `Enterprise Cloud Edition` ます。

## 共通ネイティブ列

| **列名** | **説明** |
|---|---|
| `entity\_id` | テーブルの一意の識別子。 各 `entity\_id` は、返品を要求された品目を表します。 |
| `rma\_entity\_id` | `enterprise\_rma` テーブルに関連付けられている外部キー。 |
| `status` | 項目の返品状態。 値には「received」、「pending」、「authorized」などがあります。 このステータスの値は、リターン全体のステータスの値と一致しない場合があります。 |
| `qty\_requested` | 顧客が返品を要求する数量。 |
| `qty\_approved` | 返品が承認された数量。 |
| `qty\_returned` | 返される数量。 |
| `order\_item\_id` | `sales\_flat\_order\_item` テーブルに関連付けられている外部キー。 |
| `product\_sku` | 返される SKU。 |

{style="table-layout:auto"}

## 一般的な計算列

| **列名** | **説明** |
|---|---|
| `Return date\_requested` | これは、顧客が返品を要求した日付です。 |
| `Item price` | 商品の価格。 |
| `Return item's total value (qty\_returned * price)` | これは、返される項目の合計金額です。 これは、`enterprise\_rma` テーブルの合計返品金額の計算に使用されます。 |

{style="table-layout:auto"}

## 一般的な指標

| **指標名** | **説明** | **建設** |
|---|---|---|
| `Number of items returned` | 返される項目の数。 | 操作列：戻された数量 <br> 操作：合計 <br> タイムスタンプ列：戻り日が要求されました |
| `Returned items' total value` | 返される金額。 | 操作列：返品品目の合計値（戻された数量*価格） <br> 操作：合計 <br> タイムスタンプ列：要求された返品日 |

{style="table-layout:auto"}

## その他のテーブルへの接続

`enterprise_rma`

* 次の結合を使用して、`enterprise_rma_item_entity` テーブルに `Return date\_requested` などの結合された列を作成します。
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` （多） => `enterprise_rma.entity_id` （1）
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` （多） => `magento_rma.entity_id` （1）

`sales_flat_order_item`

* で結合された列を作成  次 `enterprise_rma_item_entity` 結合を使用してテーブルを作成します。

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` （多） => `sales_flat_order_item.item_id` （1）
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` （多） => `sales_order_item.item_id` （1）
