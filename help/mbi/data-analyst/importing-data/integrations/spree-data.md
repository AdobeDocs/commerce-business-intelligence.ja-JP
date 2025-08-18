---
title: 予期される Spree データ
description: Spree から自分のアカウントにインポートできるメインのデータテ  [!DNL Commerce Intelligence]  ブルを調べます。
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 予期される [!DNL Spree] データ

[ ストアに接続  [!DNL Spree]  した後、&lbrace;3](../../../data-analyst/importing-data/integrations/spree.md)Data Warehouse Manager[ を使用すると、](../../data-warehouse-mgr/tour-dwm.md) Platform から関連するデータフィールドを簡単に追跡して分析できます。[!DNL Spree]

このトピックでは、データに関する [!DNL Spree] 追加ドキュメント [!DNL Commerce Intelligence] へのリンクを含め、[ から ](https://guides.spreecommerce.org/developer/addresses.html#address) アカウントに読み込むことができるメインのデータテーブル [!DNL Spree] ついて説明します。

| **テーブル名** | **説明** |
|-----|-----|
| `Users` | `users` の表には、登録済みの顧客のアカウントの詳細（個人のメールアドレス、名前、登録日など）が含まれています。 これにより、様々な顧客セグメントとその購入行動を分析できます。 |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | `orders` テーブルは、注文レベルのすべての指標の基盤となります。 [!DNL Spree] （注文のタイムスタンプ）、`completed\_at` （注文を行った登録ユーザーの ID）など、`user\_id` ストアからの購入に関するすべての注文詳細がここに記録されます。 注文が登録ユーザーによって行われた場合、`user\_id` は `users` テーブルにリンクして戻り、ユーザーの購入行動を分析できるようにします。 |
| `Line items` | `line\_items` テーブルは、`orders` テーブルまたは `subscriptions` の子です。 注文または購読の行項目の詳細が記録されます。 複数の商品を含む注文の場合、各商品には、`product\_id` のテーブルに関連付けることができる `Products` を含む、このテーブルの独自のデータ行があります。 |
| `Products` | `products` の表には、Spree カタログ内の販売可能な品目のすべての製品詳細が記録されます。 これにより、ライン品目レベルの指標を製品属性別にセグメント化できます。 |
| `Subscriptions` | [!DNL Spree] サブスクリプション拡張機能がある場合、`subscriptions` テーブルには、`created\_at` （開始日）、`cancelled\_at` （サブスクリプションがキャンセルされた日付）、サブスクリプションの `interval` など、個々のサブスクリプションの情報が保持されます。 |

{style="table-layout:auto"}

## 関連：

* [接続  [!DNL Spree]](../integrations/spree.md)
* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
