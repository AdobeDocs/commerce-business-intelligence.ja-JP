---
title: MBI Essentials と Pro
description: MBI Essentials とMBI Proの違いを学ぶ
exl-id: 624a6285-8497-43d9-a56d-8ae503e0e2dd
source-git-commit: f358f11586e4b7c44e9192584ea0fdeff5526287
workflow-type: tm+mt
source-wordcount: '83'
ht-degree: 4%

---

# [!DNL MBI Essentials] vs [!DNL MBI Pro]

>[!NOTE]
>
>これは次のアーカイブドキュメントです： [!DNL MBI].

次の表に、Essentials と Pro に含まれる機能を示します。

|  | **`MBI Essentials`** | **`MBI Pro`** |
|-----|-----|-----|
| `Pre-Defined Reports` | 最大 100 | カスタム |
| `Pre-Defined Dashboards` | 5-6 | カスタム |
| `New Custom Report Creation` | はい | はい |
| `Commerce Tables` | 4-6 | 無制限 |
| `Log-ins/User Accounts` | 10 | 20 |
| `User Permissions` | はい | はい |
| `Data Warehouse Manager` | 使用不可 | 利用可能 |
| `Email Reports` | はい | はい |
| `Cohort Report Builder` | はい | はい |
| `Google Analytics Live Integration` | はい | 無制限 |
| `3rd Party Integrations` | 使用不可 | 利用可能 |
| `Full API Access` | いいえ | はい |
| `Access to CS, AM, or Analysts` | いいえ | はい |
| `Professional Services` | 利用可能 | 利用可能 |

{style="table-layout:auto"}

>[!NOTE]
>
>テーブルの数は、ゲストのチェックアウトによって異なります。

**含まれるテーブル**

* `sales\_order`
* `sales\_order\_item`
* `sales\_order\_address`
* `customer\_entity`
* `customer\_group`
* `store`

## Essentials に含まれる列

の項目 _斜体_ は計算フィールドです。

* `sales_order` 表
   * `entity_id`
   * `base_grand_total`
   * `customer_id`
   * `status`
   * `customer_email`
   * `store_id`
   * `base_currency_code`
   * `billing_address_id`
   * `shipping_address_id`
   * `base_shipping_amount`
   * `base_tax_amount`
   * `coupon_code`
   * `created_at`
   * `updated_at`
   * `base_subtotal`
   * `customer_group_id`
   * `base_discount_amount`
   * `base_discount_invoiced`
   * `increment_id`
   * `Customer's order number`
   * `Customer's first order date`
   * `Customer's lifetime number of orders`
   * `Is customer's last order?`
   * `Billing address region`
   * `Shipping address country`
   * `Customer's lifetime revenue`
   * `Seconds between customer's first order date and this order`
   * `Seconds since previous order`
   * `Store name`
   * `Customer's lifetime number of coupons`
   * `Customer's order number (previous-current)`
   * `Shipping address region`
   * `Number of items in order`
   * `Billing address city`
   * `Shipping address city`
   * `Customer's group code`
   * `Customer's first order's billing region`
   * `Customer's first order's coupon_code`
   * `Customer's creation date`
   * `Billing address country`

* `sales_order_item` 表
   * `item_id`
   * `qty_ordered`
   * `base_price`
   * `name`
   * `order_id`
   * `sku`
   * `product_type`
   * `product_id`
   * `created_at`
   * `updated_at`
   * `parent_item_id`
   * `store_id`
   * `base_discount_amount`
   * `base_discount_invoiced`
   * `Order's coupon_code`
   * `Order item total value (quantity * price)`
   * `Order's increment_id`
   * `Customer's email`
   * `Customer's lifetime number of orders`
   * `Store name`
   * `Customer's order number`
   * `Order's status`
   * `Customer's lifetime revenue`

* `sales_order_address` 表
   * `entity_id`
   * `city`
   * `region`
   * `country_id`

* `customer_entity` 表
   * `entity_id`
   * `email`
   * `group_id`
   * `created_at`
   * `updated_at`
   * `store_id`
   * `Customer's lifetime revenue`
   * `Customer's lifetime number of coupons`
   * `Customer's first order date`
   * `Customer's lifetime number of orders`
   * `Seconds since customer's first order date`
   * `Customer's first 30 day revenue`
   * `Customer's first order's billing region`
   * `Customer's first order's coupon_code`
   * `Customer's group code`
   * `Store name`

* `customer_group` 表
   * `customer_group_id`
   * `customer_group_code`

* `store` 表
   * `store_id`
   * `name`
