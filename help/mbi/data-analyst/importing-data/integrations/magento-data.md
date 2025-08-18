---
title: 予想されるCommerce データ
description: Commerce ユーザーがCommerce Intelligenceに読み込むメインデータテーブルを調べます
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# 予期される [!DNL Adobe Commerce] データ

[ ストアに接続  [!DNL Adobe Commerce]  した後は、Data Warehouse Manager を使用して、](../../../data-analyst/importing-data/integrations/magento.md) 析のためにCommerce データベースから関連するデータフィールドを簡単に追跡できます。

このトピックでは、Commerce ユーザーが [!DNL Commerce Intelligence] に読み込むメインデータテーブルについて説明します。

| **テーブル名** | **説明** |
|-----|-----|
| `Customers` | `customer\_entity` と関連テーブルには、メールアドレスや登録日など、データベース内の各 *登録済みの顧客* に関連付けられた情報が記述されます。 この情報を使用して、顧客レベルの属性およびコホートでセグメント化を開始できます。 |
| `Orders` | `sales\_flat\_order` テーブルは、注文が行われた `created\_at` タイムスタンプと、売上高を合計する `base\_grand\_total` フィールドを含む、すべての注文を記録します。 これらのフィールドは、注文レベルの指標の基礎となります。 注文が *登録済みの顧客* によって行われた場合、`customer\_id` フィールドは `customer\_entity` テーブルにリンクして戻り、顧客の購入行動を分析できるようにします。 |
| `Order items` | `sales\_flat\_order\_item` テーブルには、注文に属する各品目が記録されます。 これには、`price` フィールドと `qty\_ordered` フィールド、および `order\_id` テーブルに接続する `sales\_flat\_order` フィールドが含まれます。 このテーブルは、`Item sold` などの指標の基礎となり、`product` と `product type` でセグメント化できます。 |
| `Products` | `catalog\_product\_entity` のテーブルには、カテゴリ、サイズ、色など、製品レベルの属性に関する情報が格納されます。 |
| `Categories` | 商品は、Commerce ビルドの設定方法に応じて、1 つまたは複数の異なる `product categories` に属します。 `catalog\_category\_entity` テーブルには、これらのカテゴリの階層（例：アパレル/トップス/T シャツ）が格納され、`catalog\_category\_product` テーブルには、製品とそれらのカテゴリ間の接続がログに記録されます。 |

{style="table-layout:auto"}

## 関連

* [接続  [!DNL Adobe Commerce]](../integrations/magento.md)
* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
