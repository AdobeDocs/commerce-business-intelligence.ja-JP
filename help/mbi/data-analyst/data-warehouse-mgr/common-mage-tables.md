---
title: 一般的なCommerce テーブル
description: ' [!DNL Commerce Intelligence] お客様が使用する一般的なテーブルの一部について説明します。'
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/uYdgYNMbJGRz8kQ3mCF2McpZpflHSAa37Lk-CLaDlBw
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 464
ht-degree: 0%

---

# 一般的なCommerce テーブル

[!DNL Adobe Commerce] インスタンスを最初に[[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md)に接続すると、[!DNL Commerce Intelligence]は、一部のコマーステーブル （通常は4 ～ 6 テーブル）からデータを自動的にレプリケートして、ダッシュボードとレポートの最初のセットを設定します。 これは優れた出発点となりますが、ほとんどのストアインスタンスは数十から数百のテーブルを生成し、重要なinsightをビジネスのパフォーマンスに提供できます。

以下は、[!DNL Commerce Intelligence]人のお客様が使用する一般的なテーブルの一部を示します。 Commerce インスタンスを[Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md)に接続した後、[Data Warehouse Manager](../../data-analyst/data-warehouse-mgr/tour-dwm.md)を使用して、関連するデータ フィールドをトラッキングできます。

| テーブル名 | 説明 |
|---|---|
| `catalog_category_entity` | `catalog_category_entity` テーブルの各行は、特定のカテゴリを表します。 関連付けられた`catalog_category_entity_varchar` テーブルと`catalog_category_product` マッピング テーブルを使用すると、各製品のカテゴリ情報を取得できます。 |
| `catalog_category_product` | `catalog_category_product` テーブルの各行には、製品とカテゴリの組み合わせが一覧表示されます。 したがって、特定の製品がこのテーブルに異なるカテゴリで複数回存在する可能性があり、特定のカテゴリがこのテーブルに異なる製品に関連付けられて複数回存在する可能性があります。 このテーブルには、`catalog_category_entity` テーブル （カテゴリーレベルの詳細を保持する）と`catalog_product_entity` テーブル （製品レベルの詳細を保持する）のインデックスが作成されます。 |
| `catalog_product_entity` | `catalog_product_entity` テーブルの各行は、特定の製品を表します。 これには、Commerce アカウントとそのSKUで商品が作成された時期が含まれます。 |
| `customer_entity` | [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) テーブルの各行は、web サイトの登録ユーザーを表します。 登録日やメールアドレスなどの基本的な顧客レベルの詳細を次の表に示します。 |
| `quote` | [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) テーブルの各行は、チェックアウトプロセスで作成されたカートを表します。そのカートが最終的に注文に変換されたかどうかを確認します。 この表のサイズが大きくなる可能性があるため、Adobeでは、60日を超える未変換のカートがある場合など、特定の条件を満たす場合は、レコードを定期的に削除することをお勧めします。 |
| `quote_item` | [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) テーブルの各行は、買い物かごに追加されたアイテム（買い物かごが最終的に注文に変換されたかどうか）を表します。 この表のサイズが大きくなる可能性があるため、Adobeでは、60日を超える未変換のカートがある場合など、特定の条件を満たす場合は、レコードを定期的に削除することをお勧めします。 |
| `sales_order` | [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) テーブルの各行は、サイトに配置された注文を表します。 このテーブルには、注文の日付、注文した顧客、注文合計、割引とクーポンコードの使用状況などの注文レベルの情報が含まれています。 |
| `sales_order_address` | `sales_order_address` テーブルの各行には、特定の注文の送料と請求情報が含まれています。 `sales_order` テーブルでは、特定の順序の`billing_address_id`と`shipping_address_id`は、`sales_order_address` テーブルの特定の行（`entity_id`で識別）を参照しています。 |
| `sales_order_item` | [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) テーブルの各行は、特定の順序から特定の項目を識別します。 各行には、商品、購入数量、特定の商品が関連付けられている注文などの詳細が含まれます。 |

{style="table-layout:auto"}

## 関連ドキュメント

[エンティティ関係図](../data-warehouse-mgr/entity-rel-diag.md)
