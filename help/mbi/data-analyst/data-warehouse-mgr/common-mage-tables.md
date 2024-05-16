---
title: 一般的なCommerce テーブル
description: 次に示す、より一般的なテーブルの一部について説明します [!DNL Commerce Intelligence] 顧客はを使用します。
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# 一般的なCommerce テーブル

を初めて接続する場合 [!DNL Adobe Commerce] インスタンス先 [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md), [!DNL Commerce Intelligence] は、一部のコマーステーブル（通常は 4～6 つのテーブル）からデータを自動的に複製して、ダッシュボードとレポートの初期セットを設定します。 これは優れた出発点となりますが、ほとんどのストアインスタンスでは、追加のテーブルが数百ではなく数十も生成され、ビジネスのパフォーマンスに関する重要なインサイトが得られます。

次に、一般的なテーブルの一部を示します [!DNL Commerce Intelligence] 顧客はを使用します。 お先に [Commerce インスタンスをCommerce Intelligence に接続する](../../data-analyst/importing-data/integrations/magento.md)を使用する場合は、 [Data Warehouse管理者](../../data-analyst/data-warehouse-mgr/tour-dwm.md) 関連するデータフィールドを追跡します。

| テーブル名 | 説明 |
|---|---|
| `catalog_category_entity` | 各行 `catalog_category_entity` 表は、特定のカテゴリを示しています。 関連付けられたを使用 `catalog_category_entity_varchar` テーブルと `catalog_category_product` マッピングテーブルでは、各製品のカテゴリ情報を取得できます。 |
| `catalog_category_product` | 各行 `catalog_category_product` 表は、製品とカテゴリの組み合わせを示しています。 したがって、特定の製品が異なるカテゴリでこのテーブルに複数回存在する可能性があり、特定のカテゴリが異なる製品に関連付けられたこのテーブルに複数回存在する可能性があります。 このテーブルは、 `catalog_category_entity` テーブル （カテゴリレベルの詳細を格納）と `catalog_product_entity` テーブル（製品レベルの詳細を保持）。 |
| `catalog_product_entity` | 各行 `catalog_product_entity` 表は、特定の製品を表します。 これには、その商品がCommerce アカウントと SKU で作成された場合が含まれます。 |
| `customer_entity` | 各行 [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) 表は、Web サイト上の登録済みユーザーを表します。 登録日やメールアドレスなど、顧客レベルの基本的な詳細がこのテーブルに記載されています。 |
| `quote` | 各行 [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) テーブルは、チェックアウトプロセスで作成された買い物かごを表し、その買い物かごが最終的に注文に変換されたかどうかを示します。 このテーブルの潜在的なサイズにより、Adobeでは、60 日を超える未変換の買い物かごがある場合など、特定の条件を満たした場合に、レコードを定期的に削除することをお勧めします。 |
| `quote_item` | 各行 [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) テーブルは、買い物かごに追加された項目を表し、買い物かごが最終的に注文に変換されたかどうかを示します。 このテーブルの潜在的なサイズにより、Adobeでは、60 日を超える未変換の買い物かごがある場合など、特定の条件を満たした場合に、レコードを定期的に削除することをお勧めします。 |
| `sales_order` | 各行 [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) テーブルは、サイトでの注文を表します。 このテーブルには、注文の日付、注文を行った顧客、注文合計、割引およびクーポンコードの使用状況など、注文レベルの情報が含まれています。 |
| `sales_order_address` | 各行 `sales_order_address` 表には、特定の注文に関する出荷情報と請求情報が含まれています。 日 `sales_order` テーブル、 `billing_address_id` および `shipping_address_id` 特定の順序について、特定の行を参照します（で識別） `entity_id`） `sales_order_address` テーブル。 |
| `sales_order_item` | 各行 [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) テーブルは、特定の順序から特定の項目を識別します。 各行には、製品、購入数量、特定の品目が関連付けられている注文などの詳細が含まれています。 |

{style="table-layout:auto"}

## 関連ドキュメント

[エンティティ関係図](../data-warehouse-mgr/entity-rel-diag.md)
