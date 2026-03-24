---
title: 予想されるCommerce データ
description: Commerce ユーザーがCommerce Intelligenceに読み込む主なデータテーブルを調べます
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/D-GNfk1-kMscgF1xBKM5xG7wRV4IkIDh9wEBCMGb630
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 239
ht-degree: 0%

---

# [!DNL Adobe Commerce] データが必要です

[ ストアを接続した [!DNL Adobe Commerce] 後](../../../data-analyst/importing-data/integrations/magento.md)、Data Warehouse Managerを使用して、Commerce データベースから関連するデータ フィールドを簡単に追跡し、分析できます。

ここでは、Commerce ユーザーが[!DNL Commerce Intelligence]に読み込む主なデータ テーブルについて説明します。

| **テーブル名** | **説明** |
|-----|-----|
| `Customers` | `customer\_entity`および関連テーブルには、データベース内の各&#x200B;*登録済み顧客*&#x200B;に関連付けられている情報（電子メールアドレスや登録日など）が記載されています。 この情報により、顧客レベルの属性やコホートによるセグメンテーションを開始できます。 |
| `Orders` | `sales\_flat\_order` テーブルには、注文が行われた`created\_at` タイムスタンプと収益を合計する`base\_grand\_total` フィールドを含む、すべての注文が記録されます。 これらのフィールドは注文レベルの指標の基礎となります。 *登録済みの顧客*&#x200B;が注文を行った場合、`customer\_id` フィールドは`customer\_entity` テーブルにリンクして、顧客の購買行動に関する分析を許可します。 |
| `Order items` | `sales\_flat\_order\_item` テーブルには、注文に属する各項目が記録されます。 これには、`price`および`qty\_ordered` フィールド、および`order\_id` テーブルに接続する`sales\_flat\_order` フィールドが含まれます。 このテーブルは`Item sold`のような指標の基盤となり、`product`と`product type`でセグメント化できます。 |
| `Products` | `catalog\_product\_entity` テーブルには、カテゴリ、サイズ、カラーなど、製品レベルの属性に関する情報が格納されます。 |
| `Categories` | 製品は、Commerce ビルドの設定方法に応じて、1つまたは複数の異なる`product categories`に属しています。 `catalog\_category\_entity` テーブルには、これらのカテゴリの階層が保存され（例えば、アパレル/トップス/T シャツ）、`catalog\_category\_product` テーブルには、製品とそれらのカテゴリ間の接続が記録されます。 |

{style="table-layout:auto"}

## 関連

* [接続中 [!DNL Adobe Commerce]](../integrations/magento.md)
* [統合を再認証しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
