---
title: Commerce Intelligence Essentials と Pro の比較
description: Commerce Intelligence Essentials とCommerce Intelligence Pro の違いについて説明します。
exl-id: 624a6285-8497-43d9-a56d-8ae503e0e2dd
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 2%

---

# [!DNL Commerce Intelligence Essentials] と [!DNL Commerce Intelligence Pro]

次の表に、従来のCommerce Intelligence アカウントと現在の `Essentials` アカウントの比較に含まれる要素を示します。 Adobeでは、`Essentials` を提供しなくなりました。

|   | **`Commerce Intelligence Essentials`** | **`Commerce Intelligence Pro`** |
|-----|-----|-----|
| `Pre-Defined Reports` | 最大 100 | カスタム |
| `Pre-Defined Dashboards` | 5-6 | カスタム |
| `New Custom Report Creation` | はい | はい |
| `Commerce Tables` | 4-6 | 制限なし |
| `Log-ins/User Accounts` | 10 | 20 |
| `User Permissions` | はい | はい |
| `Data Warehouse Manager` | 利用不可 | 利用可能 |
| `Email Reports` | はい | はい |
| `Cohort Report Builder` | はい | はい |
| `Google Analytics Live Integration` | はい | 制限なし |
| `3rd Party Integrations` | 利用不可 | 利用可能 |
| `Full API Access` | 不可 | はい |
| `Access to CS, AM, or Analysts` | 不可 | はい |
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

<!---
## Columns Included in Essentials

Items in _italics_ are calculated fields.

* `sales_order` table
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

* `sales_order_item` table
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

* `sales_order_address` table
  * `entity_id`
  * `city`
  * `region`
  * `country_id`

* `customer_entity` table
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

* `customer_group` table
  * `customer_group_id`
  * `customer_group_code`

* `store` table
  * `store_id`
  * `name`
-->
