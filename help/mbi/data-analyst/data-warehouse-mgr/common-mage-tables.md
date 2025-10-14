---
title: 一般的なCommerce テーブル
description: お客様が使用する一般的なテーブルのいくつか  [!DNL Commerce Intelligence]  ついて説明します。
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# 一般的なCommerce テーブル

[!DNL Adobe Commerce] インスタンスを [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md) に初めて接続すると、[!DNL Commerce Intelligence] では、一部のコマーステーブル（通常は 4～6 個のテーブル）からデータを自動的に複製して、ダッシュボードとレポートの初期セットを設定します。 これは優れた出発点となりますが、ほとんどのストアインスタンスでは、数百ではなく数十の追加テーブルが生成され、ビジネスのパフォーマンスに重要なinsightを提供できます。

以下に、お客様が使用する一般的なテーブルの一部 [!DNL Commerce Intelligence] 示します。 [Commerce インスタンスをCommerce Intelligenceに接続 &#x200B;](../../data-analyst/importing-data/integrations/magento.md) した後、[Data Warehouse Manager](../../data-analyst/data-warehouse-mgr/tour-dwm.md) を使用して関連するデータフィールドを追跡できます。

| テーブル名 | 説明 |
|---|---|
| `catalog_category_entity` | `catalog_category_entity` の表の各行は、特定のカテゴリを示しています。 関連する `catalog_category_entity_varchar` テーブルと `catalog_category_product` のマッピングテーブルを使用して、各製品のカテゴリ情報を取得できます。 |
| `catalog_category_product` | `catalog_category_product` テーブルの各行には、製品とカテゴリの組み合わせが一覧表示されます。 したがって、特定の製品が異なるカテゴリでこのテーブルに複数回存在する可能性があり、特定のカテゴリが異なる製品に関連付けられたこのテーブルに複数回存在する可能性があります。 このテーブルは、`catalog_category_entity` テーブル（カテゴリレベルの詳細を保持）と `catalog_product_entity` テーブル（製品レベルの詳細を保持）のインデックスを作成します。 |
| `catalog_product_entity` | `catalog_product_entity` テーブルの各行は、特定の製品を表します。 これには、その商品がCommerce アカウントと SKU で作成された場合が含まれます。 |
| `customer_entity` | [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) の表の各行は、Web サイトに登録されているユーザーを表します。 登録日やメールアドレスなど、顧客レベルの基本的な詳細がこのテーブルに記載されています。 |
| `quote` | [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) テーブルの各行は、チェックアウトプロセスで作成された買い物かごを表し、その買い物かごが最終的に注文に変換されたかどうかを示します。 Adobeこのテーブルの潜在的なサイズのため、60 日を超える未変換の買い物かごがある場合など、特定の条件を満たした場合は、レコードを定期的に削除することをお勧めします。 |
| `quote_item` | [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) テーブルの各行は、買い物かごに追加された項目を表し、最終的に買い物かごが注文に変換されたかどうかを示します。 Adobeこのテーブルの潜在的なサイズのため、60 日を超える未変換の買い物かごがある場合など、特定の条件を満たした場合は、レコードを定期的に削除することをお勧めします。 |
| `sales_order` | [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) テーブルの各行は、サイトに対する注文を表します。 このテーブルには、注文の日付、注文を行った顧客、注文合計、割引およびクーポンコードの使用状況など、注文レベルの情報が含まれています。 |
| `sales_order_address` | `sales_order_address` テーブルの各行には、特定の注文の配送情報と請求情報が含まれます。 `sales_order` テーブルでは、指定された注文の `billing_address_id` と `shipping_address_id` は、`entity_id` テーブルの特定の行（`sales_order_address` で識別）を参照します。 |
| `sales_order_item` | [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) テーブルの各行は、特定の順序から特定の項目を識別します。 各行には、製品、購入数量、特定の品目が関連付けられている注文などの詳細が含まれています。 |

{style="table-layout:auto"}

## 関連ドキュメント

[エンティティ関係図](../data-warehouse-mgr/entity-rel-diag.md)
