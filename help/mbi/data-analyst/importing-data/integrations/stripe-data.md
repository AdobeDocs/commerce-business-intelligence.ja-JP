---
title: 予期されるストライプ・データ
description: Stripe からにインポートできる主なデータ・テーブルの参照 [!DNL MBI].
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# 予測 [!DNL Stripe] データ

後 [接続しました [!DNL Stripe] アカウント](../integrations/stripe.md)を使用する場合、 [Data Warehouse管理](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 分析に関連するデータフィールドを容易に追跡する。

この記事では、インポート元となる主なデータテーブルを確認します。 [!DNL Stripe] into [!DNL MBI]. 設定が完了すると、次のテーブルが Data Warehouse で作成されます。 各テーブルの属性の詳細を表示するには、「テーブル名」列のリンクをクリックします。

| **テーブル名** | **説明** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/api/curl#customer_object) | 顧客オブジェクトを使用すると、繰り返し請求を実行し、同じ顧客に関連付けられた複数の請求を追跡できます。 |
| [`Charges`](https://stripe.com/docs/api/curl#charge_object) | このテーブルには、クレジットカードとデビットカードに対する料金に関する情報（金額、通貨、ステータス、顧客 ID など）が含まれます。 |
| [`Coupons`](https://stripe.com/docs/api/curl#coupon_object) | このテーブルには、顧客に適用する割引または金額割引に関する情報が含まれます。 クーポンは請求書にのみ適用されることに注意してください。1 回限りの料金には適用されません。 |
| [`Invoices`](https://stripe.com/docs/api/curl#invoice_object) | このテーブルには、請求書に関する情報が含まれます。請求書には、支払額、購読、請求書項目、自動按分調整などが含まれます。 |
| [`Plans`](https://stripe.com/docs/api/curl#plan_object) | この表には、サイト上の様々な製品および機能レベルの価格情報が含まれています。 例えば、基本機能に対して 10 ドル/月のプランを用意し、プレミアム機能に対しては 20 ドル/月のプランを用意するとします。 |
| [`Subscriptions`](https://stripe.com/docs/api/curl#subscription_object) | このテーブルには、顧客が属するサブスクリプションプランの詳細が含まれます。 属性には、顧客 ID、ステータス、キャンセル日/終了日、税率、試用情報などが含まれます。 |
| [`Events`](https://stripe.com/docs/api/curl#event_object) | イベントを使用すると、アカウントで発生した興味深いことがわかります。 [興味深いイベントが発生した場合](https://stripe.com/docs/api/curl#event_types)に設定すると、新しいイベントオブジェクトが作成されます。 例えば、チャージが成功した場合などです。 `charge.succeeded` イベントが作成された。または、請求書を支払えない場合は `invoice.payment\_failed` イベントが作成されました。 |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>多くの API リクエストで、複数のイベントが作成される場合があります。 例えば、ある顧客の新しいサブスクリプションを作成した場合、 `customer.subscription.created` イベントと  `charge.succeeded` イベント。

## 関連：

* [接続中 [!DNL Stripe]](../integrations/stripe.md)
* [統合の再認証](https://support.magento.com/hc/en-us/articles/360016733151)
