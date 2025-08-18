---
title: 予想されるStripe データ
description: StripeからCommerce Intelligenceに読み込むことができるメインデータテーブルについて説明します。
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# 予期される [!DNL Stripe] データ

[ アカウントに接続  [!DNL Stripe]  た ](../integrations/stripe.md) 後、[Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) を使用して、関連するデータフィールドを簡単に追跡して分析できます。

このトピックでは、[!DNL Stripe] から [!DNL Commerce Intelligence] に読み込むことができるメインのデータテーブルについて説明します。 セットアップが完了すると、Data Warehouseに次のテーブルが作成されます。 各テーブルの属性の詳細を確認するには、「テーブル名」列のリンクをクリックします。

| **テーブル名** | **説明** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | 顧客オブジェクトを使用すると、固定料金を実行し、同じ顧客に関連付けられた複数の料金を追跡できます。 |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | この表には、金額、通貨、ステータス、顧客 ID など、クレジット・カードおよびデビット・カードへの手数料に関する情報が含まれています。 |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | この表には、顧客に適用するパーセントまたは金額割引に関する情報が含まれています。 クーポンは請求書にのみ適用されます。1 回限りの料金には適用されません。 |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | この表には、未払金額、定期購読/購買、請求書項目、自動按分修正など、請求書に関する情報が含まれています。 |
| [`Plans`](https://stripe.com/docs/api/plans/object) | 次の表には、サイトの様々な製品および機能レベルの価格情報が含まれています。 例えば、基本的な機能に対して月額 10 ドルのプランがあり、プレミアム機能に対して月額 20 ドルのプランがあるとします。 |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | このテーブルには、顧客が属するサブスクリプションプランの詳細が含まれます。 属性には、顧客 ID、ステータス、キャンセル/終了日、税率、体験版情報などが含まれます。 |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | イベントは、アカウントで発生した興味深い出来事を知らせます。 [ 対象イベントが発生すると ](https://stripe.com/docs/api/events/types)、新しいイベントオブジェクトが作成されます。 例えば、請求が成功した場合 `charge.succeeded` イベントが作成される場合、または請求書に支払いが不可能な場合に `invoice.payment\_failed` 請求イベントが作成されます。 |

{style="table-layout:auto"}

>[!NOTE]
>
>多くの API リクエストにより、複数のイベントが作成される場合があります。 例えば、ある顧客の購読を作成した場合、`customer.subscription.created` イベントと `charge.succeeded` イベントの両方を受け取ります。

## 関連：

* [接続  [!DNL Stripe]](../integrations/stripe.md)
* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
