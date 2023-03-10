---
title: 予想される空きデータ
description: Spree から [!DNL MBI] アカウント
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# 予測 [!DNL Spree] データ

次の条件が満たされた後 [接続済み [!DNL Spree] ストア](../../../data-analyst/importing-data/integrations/spree.md)を使用する場合、 [Data Warehouse管理](../../data-warehouse-mgr/tour-dwm.md) 関連するデータフィールドを簡単に追跡するには [!DNL Spree] プラットフォームを使用して分析できます。

この記事では、読み込み元となる主なデータテーブルについて説明します。 [!DNL Spree] を [!DNL MBI] アカウント（次へのリンクを含む） [追加ドキュメント](https://guides.spreecommerce.org/developer/addresses.html#address) について [!DNL Spree] データ。

| **テーブル名** | **説明** |
|-----|-----|
| `Users` | この `users` この表には、個人の E メール、名前、登録日など、登録ユーザーのアカウントの詳細が含まれます。 これにより、様々な顧客セグメントとその購入行動を分析できます。 |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | この `orders` この表は、すべての注文レベルの指標の基礎となります。 ここには、お客様の購入の注文の詳細がすべて記録されます [!DNL Spree] ストア（次を含む） `completed\_at` （注文のタイムスタンプ）、 `user\_id` （注文した登録ユーザーの id）。 注文が登録ユーザーによって行われた場合、 `user\_id` リンクを `users` テーブルを使用して、ユーザーの購入行動を分析できます。 |
| `Line items` | この `line\_items` テーブルは、 `orders` テーブルまたは `subscriptions`. 注文または購読の品目の詳細を記録します。 複数の製品を含む注文の場合、この表には各製品に固有のデータ行があり、 `product\_id` それを結ぶ事が出来る `Products` 表。 |
| `Products` | この `products` テーブルには、Spree カタログの販売可能品目のすべての製品詳細が記録されます。 これにより、製品属性別に行項目レベルの指標をセグメント化できます。 |
| `Subscriptions` | 次の場合、 [!DNL Spree] subscriptions 拡張機能 `subscriptions` テーブルには、 `created\_at` （開始日） `cancelled\_at` （配信登録がキャンセルされた日付） `interval` 購読の |

{style="table-layout:auto"}

## 関連：

* [接続中 [!DNL Spree]](../integrations/spree.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
