---
title: 共通コマーステーブル
description: より一般的なテーブルのいくつかを説明します。 [!DNL Commerce Intelligence] のお客様はを使用します。
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 共通コマーステーブル

最初に [!DNL Adobe Commerce] インスタンスから [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md), [!DNL Commerce Intelligence] 一部のコマーステーブル（通常は 4 ～ 6 個のテーブル）からデータを自動的にレプリケートして、ダッシュボードとレポートの初期セットを設定します。 これは非常に優れた出発点ですが、ほとんどのストアインスタンスでは、数百ものテーブルを追加しない場合に数十を生成し、ビジネスのパフォーマンスに関する重要なインサイトを提供できます。

以下に、より一般的なテーブルの一覧を示します。 [!DNL Commerce Intelligence] のお客様はを使用します。 後 [コマースインスタンスを Commerce Intelligence に接続](../../data-analyst/importing-data/integrations/magento.md)を使用する場合、 [Data Warehouse管理](../../data-analyst/data-warehouse-mgr/tour-dwm.md) をクリックして、関連するデータフィールドを追跡します。

| テーブル名 | 説明 |
|---|---|
| `catalog_category_entity` | 各行 ( `catalog_category_entity` 表は、特定のカテゴリを示しています。 を `catalog_category_entity_varchar` テーブルと `catalog_category_product` マッピングテーブルを使用すると、各製品のカテゴリ情報を取得できます。 |
| `catalog_category_product` | 各行 ( `catalog_category_product` 表に、製品とカテゴリの組み合わせを示します。 したがって、このテーブルには、異なるカテゴリを持つ特定の製品が複数回存在する場合があり、このテーブルには、異なる製品に関連付けられた複数回存在する場合があります。 次の表は、 `catalog_category_entity` テーブル（カテゴリレベルの詳細を格納）および `catalog_product_entity` テーブル（製品レベルの詳細を格納） |
| `catalog_product_entity` | 各行 ( `catalog_product_entity` テーブルは、特定の製品を表します。 これには、その製品が Commerce アカウントとその SKU で作成された日時も含まれます。 |
| `customer_entity` | 各行 ( [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) 表は、Web サイト上の登録ユーザーを表します。 登録日や E メールアドレスなど、基本的な顧客レベルの詳細がこのテーブルに記載されています。 |
| `quote` | 各行 ( [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) 「 」テーブルは、チェックアウトプロセスで作成された買い物かごを表し、その買い物かごが最終的に注文に変換されたかどうかを示します。 このテーブルの潜在的なサイズにより、Adobeでは、60 日を超える未変換の買い物かごがある場合など、特定の条件を満たした場合に、レコードを定期的に削除することをお勧めします。 |
| `quote_item` | 各行 ( [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) 「 」テーブルは、買い物かごが最終的に注文に変換されたかどうかに関わらず、買い物かごに追加された項目を表します。 このテーブルの潜在的なサイズにより、Adobeでは、60 日を超える未変換の買い物かごがある場合など、特定の条件を満たした場合に、レコードを定期的に削除することをお勧めします。 |
| `sales_order` | 各行 ( [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) 表は、サイトに配置される注文を表します。 このテーブルには、注文日、注文をした顧客、注文の合計、割引、クーポンコードの使用など、注文レベルの情報が含まれています。 |
| `sales_order_address` | 各行 `sales_order_address` テーブルには、特定の注文の発送と請求に関する情報が含まれます。 の `sales_order` テーブル `billing_address_id` そして `shipping_address_id` 特定の順序について、特定の行 ( `entity_id`) を `sales_order_address` 表。 |
| `sales_order_item` | 各行 ( [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) テーブルは、特定の順序の特定の項目を識別します。 各行には、製品、購入した数量、特定の品目が関連付けられている注文などの詳細が含まれます。 |

{style="table-layout:auto"}

## 関連ドキュメント

[エンティティ関係図](../data-warehouse-mgr/entity-rel-diag.md)
