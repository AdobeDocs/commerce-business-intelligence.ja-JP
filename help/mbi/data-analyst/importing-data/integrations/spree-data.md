---
title: 予期される Spree データ
description: Spree からにインポートできるメインのデータテーブルを調べます [!DNL Commerce Intelligence] アカウント。
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 予測 [!DNL Spree] データ

次の手順を実行した後 [さんがに接続しました [!DNL Spree] store](../../../data-analyst/importing-data/integrations/spree.md)を使用する場合は、 [Data Warehouse管理者](../../data-warehouse-mgr/tour-dwm.md) を使用して関連するデータフィールドを簡単に追跡できます [!DNL Spree] 分析用のプラットフォーム。

このトピックでは、インポート元となるメインのデータ テーブルについて説明します [!DNL Spree] を自分の [!DNL Commerce Intelligence] リンク先を含むアカウント [その他のドキュメント](https://guides.spreecommerce.org/developer/addresses.html#address) について [!DNL Spree] データ。

| **テーブル名** | **説明** |
|-----|-----|
| `Users` | この `users` 表には、登録顧客のアカウントの詳細（個人のメールアドレス、名前、登録日など）が含まれます。 これにより、様々な顧客セグメントとその購入行動を分析できます。 |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | この `orders` テーブルは、注文レベルのすべての指標の基盤となります。 以下に、様からの購入に関するすべての注文詳細を記録します [!DNL Spree] 含むストア `completed\_at` （注文のタイムスタンプ）、 `user\_id` （注文した登録ユーザーの id）。 登録ユーザーが注文した場合は、 `user\_id` リンクはに戻る `users` ユーザーの購入行動を分析できるテーブル。 |
| `Line items` | この `line\_items` テーブルは、次のいずれかの子です `orders` テーブルまたは `subscriptions`. 注文または購読の行項目の詳細が記録されます。 複数の商品を含む注文の場合、各商品には、このテーブル内に次のような独自のデータ行があります `product\_id` を使用すると、に関連付けることができます `Products` テーブル。 |
| `Products` | この `products` 表には、Spree カタログ内の販売可能品目のすべての製品詳細が記録されます。 これにより、ライン品目レベルの指標を製品属性別にセグメント化できます。 |
| `Subscriptions` | 次がある場合： [!DNL Spree] subscriptions 拡張機能、 `subscriptions` テーブルには、以下を含む個々のサブスクリプションの情報が格納されます `created\_at` （開始日）、 `cancelled\_at` （サブスクリプションがキャンセルされた日付）、 `interval` サブスクリプション。 |

{style="table-layout:auto"}

## 関連：

* [接続中 [!DNL Spree]](../integrations/spree.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
