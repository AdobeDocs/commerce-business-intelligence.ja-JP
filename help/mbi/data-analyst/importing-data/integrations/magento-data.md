---
title: 予想されるCommerce データ
description: Commerce ユーザーがCommerce Intelligence に読み込むメインデータテーブルを調べます
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 予測 [!DNL Adobe Commerce] データ

次の手順を実行した後 [さんがに接続しました [!DNL Adobe Commerce] store](../../../data-analyst/importing-data/integrations/magento.md)では、分析マネージャーを使用して、Data WarehouseのためにCommerce データベースから関連するデータフィールドを簡単に追跡できます。

このトピックでは、Commerce ユーザーがに読み込むメインデータテーブルについて説明します [!DNL Commerce Intelligence].

| **テーブル名** | **説明** |
|-----|-----|
| `Customers` | この `customer\_entity` および関連テーブルは、各に関連付けられた情報を記述します *登録済みの顧客* データベース内（メールアドレスや登録日など）。 この情報を使用して、顧客レベルの属性およびコホートでセグメント化を開始できます。 |
| `Orders` | この `sales\_flat\_order` テーブルには、を含むすべての注文が記録されます `created\_at` 注文のタイムスタンプと `base\_grand\_total` 収益を合計するフィールド。 これらのフィールドは、注文レベルの指標の基礎となります。 注文がによって行われた場合 *登録済みの顧客*, `customer\_id` フィールドは、  `customer\_entity` 顧客の購入行動に関する分析を可能にする表。 |
| `Order items` | この `sales\_flat\_order\_item` テーブルには、オーダーに属する各項目が記録されます。 これには以下が含まれます `price` および `qty\_ordered` フィールドと `order\_id` に接続するフィールド `sales\_flat\_order` テーブル。 この表は、以下のような指標の基盤となります。 `Item sold`、および次の基準でセグメント化できます `product` および `product type`. |
| `Products` | この `catalog\_product\_entity` テーブルには、カテゴリ、サイズ、色など、製品レベルの属性に関する情報が格納されます。 |
| `Categories` | 製品が 1 つ以上の異なる項目に属している `product categories`Commerce ビルドの設定方法に応じて調整します。 この `catalog\_category\_entity` テーブルには、これらのカテゴリ（例：アパレル/トップス/T シャツ）の階層と、 `catalog\_category\_product` テーブルには、製品とそれらのカテゴリ間の接続が記録されます。 |

{style="table-layout:auto"}

## 関連

* [接続中 [!DNL Adobe Commerce]](../integrations/magento.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
