---
title: 予想されるコマースデータ
description: Commerce ユーザーが Commerce Intelligence にインポートするメインデータテーブルを調べる
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# 予測 [!DNL Adobe Commerce] データ

次の条件が満たされた後 [接続済み [!DNL Adobe Commerce] ストア](../../../data-analyst/importing-data/integrations/magento.md)を使用すると、Data Warehouseマネージャーを使用して、コマースデータベースから関連するデータフィールドを簡単に追跡し、分析することができます。

このトピックでは、Commerce ユーザーが読み込む主なデータテーブルを調べます。 [!DNL Commerce Intelligence].

| **テーブル名** | **説明** |
|-----|-----|
| `Customers` | この `customer\_entity` 関連する表では、各 *登録顧客* をデータベースに追加します。 この情報を使用して、顧客レベルの属性とコホートによるセグメント化を開始できます。 |
| `Orders` | この `sales\_flat\_order` テーブルには、 `created\_at` 注文がおこなわれたタイムスタンプと `base\_grand\_total` 売上高を合計するフィールド。 これらのフィールドは、注文レベルの指標の基礎となります。 注文が *登録顧客*、 `customer\_id` フィールドリンクを  `customer\_entity` テーブルを使用して、顧客の購入行動を分析できます。 |
| `Order items` | この `sales\_flat\_order\_item` テーブルは、注文に属する各項目を記録します。 これには、 `price` および `qty\_ordered` フィールドと `order\_id` 接続するフィールド `sales\_flat\_order` 表。 このテーブルは、 `Item sold`を使用し、 `product` および `product type`. |
| `Products` | この `catalog\_product\_entity` テーブルには、カテゴリ、サイズ、色など、製品レベルの属性に関する情報が格納されます。 |
| `Categories` | 製品が 1 つまたは複数の異なる `product categories`（コマースの構築の設定に応じて）。 この `catalog\_category\_entity` テーブルには、これらのカテゴリの階層（アパレル/トップス/T シャツなど）と `catalog\_category\_product` テーブルには、製品とそのカテゴリ間の接続が記録されます。 |

{style="table-layout:auto"}

## 関連

* [接続中 [!DNL Adobe Commerce]](../integrations/magento.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
