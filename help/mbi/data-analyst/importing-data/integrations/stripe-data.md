---
title: 予想されるStripe データ
description: StripeからCommerce Intelligenceに読み込むことができる主なデータテーブルについて説明します。
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/dCiDusso9q9gvZOXKeHcDcuVK-jCXkqR3pQg6eTKzdo
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 323
ht-degree: 0%

---

# [!DNL Stripe] データが必要です

[&#x200B; アカウント  [!DNL Stripe] を接続した後、](../integrations/stripe.md)Data Warehouse Manager[を使用して、分析用の関連データフィールドを簡単に追跡できます。](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)

このトピックでは、[!DNL Stripe]から[!DNL Commerce Intelligence]に読み込むことができる主なデータ テーブルについて説明します。 設定が完了すると、次の表がData Warehouseに作成されます。 各テーブルの属性について詳しくは、テーブル名の列のリンクをクリックします。

| **テーブル名** | **説明** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | 顧客オブジェクトを使用すると、繰り返し請求を実行し、同じ顧客に関連付けられている複数の請求を追跡できます。 |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | この表には、金額、通貨、ステータス、顧客IDなど、クレジットカードおよびデビットカードへの請求に関する情報が含まれます。 |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | この表には、顧客に適用する割引率または割引率に関する情報が含まれています。 クーポンは請求書にのみ適用され、単発の請求には適用されません。 |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | この表には、未払い金額、サブスクリプション、請求書項目、自動配分調整など、請求書に関する情報が含まれます。 |
| [`Plans`](https://stripe.com/docs/api/plans/object) | この表には、サイトの様々な製品と機能レベルの価格情報が含まれています。 例えば、基本機能は月額10 ドル、プレミアム機能は月額20 ドルとします。 |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | この表には、顧客が属するサブスクリプションプランの詳細が含まれています。 属性には、顧客ID、ステータス、キャンセル日/終了日、税率、体験版情報などが含まれます。 |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | イベントは、アカウントで起こった興味深い出来事を知らせます。 [興味深いイベントが発生すると](https://stripe.com/docs/api/events/types)、新しいイベントオブジェクトが作成されます。 例えば、請求が`charge.succeeded` イベントの作成に成功した場合、または請求書を支払えない場合は`invoice.payment\_failed` イベントが作成されます。 |

{style="table-layout:auto"}

>[!NOTE]
>
>API リクエストの多くは、複数のイベントが作成される可能性があります。 例えば、顧客のサブスクリプションを作成すると、`customer.subscription.created` イベントと`charge.succeeded` イベントの両方が表示されます。

## 関連：

* [接続中 [!DNL Stripe]](../integrations/stripe.md)
* [統合を再認証しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
