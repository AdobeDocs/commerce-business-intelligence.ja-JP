---
title: 予想されるSpree データ
description: Spreeから [!DNL Commerce Intelligence]  アカウントに読み込むことができる主なデータ テーブルを確認します。
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/DhJhNDqTEki-evyidC-9d08qq-XSDPRu1jJqG1lOijI
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 282
ht-degree: 0%

---

# [!DNL Spree] データが必要です

[ ストア  [!DNL Spree] を接続した後、[Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md)を使用して、分析のために[!DNL Spree] プラットフォームから関連するデータ フィールドを簡単に追跡できます。](../../../data-analyst/importing-data/integrations/spree.md)

このトピックでは、[!DNL Spree]から[!DNL Commerce Intelligence] アカウントに読み込むことができる主なデータテーブルについて説明します。これには、[!DNL Spree] データに関する[追加ドキュメント ](https://guides.spreecommerce.org/developer/addresses.html#address)へのリンクが含まれます。

| **テーブル名** | **説明** |
|-----|-----|
| `Users` | `users` テーブルには、個人の電子メール、名前、登録日など、登録済み顧客のアカウントの詳細が含まれています。 これにより、さまざまな顧客セグメントとその購買行動を分析できます。 |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | `orders` テーブルは、すべての注文レベル指標の基盤として機能します。 ここに記録されているのは、`completed\_at` （注文のタイムスタンプ）、`user\_id` （注文を行った登録ユーザーのID）を含む、[!DNL Spree] ストアからの購入のすべての注文詳細です。 登録ユーザーが注文を行った場合、`user\_id`は`users` テーブルにリンクして、ユーザーの購買行動に関する分析を許可します。 |
| `Line items` | `line\_items` テーブルは`orders` テーブルまたは`subscriptions`の子です。 注文またはサブスクリプションの行項目の詳細を記録します。 複数の製品を含む注文の場合、各製品には、このテーブルに独自のデータ行があり、これには`Products` テーブルに関連付けることができる`product\_id`が含まれます。 |
| `Products` | `products` テーブルには、スプレッドカタログ内の販売可能なアイテムに関するすべての製品詳細が記録されます。 これにより、製品属性ごとに行項目レベルの指標をセグメント化できます。 |
| `Subscriptions` | [!DNL Spree] サブスクリプション拡張機能がある場合、`subscriptions` テーブルには、各サブスクリプションの情報（`created\_at` （開始日）、`cancelled\_at` （サブスクリプションがキャンセルされた日付）、サブスクリプションの`interval`など）が格納されます。 |

{style="table-layout:auto"}

## 関連：

* [接続中 [!DNL Spree]](../integrations/spree.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
