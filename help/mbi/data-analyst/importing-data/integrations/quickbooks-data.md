---
title: 予想される QuickBooks データ
description: 分析に関連するデータフィールドを簡単に追跡する方法を説明します。
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# 予測 [!DNL QuickBooks] データ

![](../../../assets/Quickbooks.png)

後 [接続しました [!DNL QuickBooks] アカウント](../../../data-analyst/importing-data/integrations/quickbooks.md)を使用する場合、 [Data Warehouse管理](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 分析に関連するデータフィールドを容易に追跡する。 次のテーブルがData Warehouseに作成されます。

追跡に使用できるすべてのフィールドを表示するには、テーブル名列でリンクをクリックします。

## トランザクションエンティティ {#transactionentities}

| **テーブル名** | **説明** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | 請求テーブルには、AP トランザクションに関する情報、またはサードパーティからの支払い要求が含まれます。 属性には、通貨タイプ、為替レート、合計金額、期限、残高などが含まれます。 |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | BillPayment エンティティは、仕入先から受け取った手形の支払の最終トランザクションです。 このテーブルには、仕入先情報、支払いタイプ、合計金額、トランザクション日などが含まれます。 |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | クレジット・メモ・テーブルは、全支払いと一部支払いの両方の払い戻しまたはクレジットである取引を記録します。 属性には、顧客の名前、顧客の請求と配送に関する情報、金額、日付などがあります。 |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | 預金には、直接預金や顧客の支払いが含まれ、 `Undeposited Funds` アカウント 属性には、金額、預金 ID、日付が含まれます。 |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | 見積は、良品またはサービスの価格設定案を含む顧客に提供されるトランザクションです。 このテーブルには、金額、割引情報、顧客情報および日付が記録されます。 |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | 請求書とは、顧客が後で支払う販売フォームです。 請求書テーブルには、預金情報、日付、明細項目、税金情報および顧客情報が記録されます。 |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | journalentries テーブルには、仕訳 ID、取引日、行項目情報など、AR および AP アカウント情報が記録されます。 |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | 支払レコードには、支払 ID、適用済みおよび未適用の金額、トランザクション日、トランザクションタイプ、処理ステータスなどの属性が含まれます。 |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | 購入テーブルには、購入 ID、支払いタイプ、金額および行項目情報が含まれます。 |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | 発注とは、仕入先に送信される商品の要求です。 この表には、仕入先情報、発注 ID、取引日、品目情報、合計金額、AP アカウント情報が含まれます。 |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | このテーブルは、顧客に対して返金を記録します。 属性には、返金受領書 ID、明細品目情報、合計金額、顧客情報および残高が含まれます。 |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | Salesreceipts テーブルは、顧客に提供された売上レシートに情報を記録します。これには、売上レシート ID、品目情報、合計金額、顧客情報、取引日、預金などが含まれます。 |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | 時間活動は、ベンダーや従業員の時間記録です。 時間活動テーブルには、時間活動 ID、従業員/ベンダー情報、ログに記録された時間、活動の説明、記録された日付が含まれます。 |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | 移動テーブルには、口座間で移動された資金に関する情報が記録されます。 属性には、転送 ID、金額、アカウント情報および日付が含まれます。 |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | 仕入先クレジットとは、仕入先に与えられた返金またはクレジットである AP 取引です。 この `vendorcredits` この表には、仕入先クレジット ID、明細品目情報、仕入先情報、AP アカウント、合計金額および日付が含まれます。 |

{style="table-layout:auto"}

## 名前リストエンティティ {#namelistentities}

| **テーブル名** | **説明** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | この表には、アカウント ID、名前、ステータス、タイプ、残高、通貨、作成時間が含まれます。 |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | このテーブルには、予算 ID、名前、開始日と終了日、タイプ、ステータス、詳細など、会社予算に関するすべての情報が記録されます。 |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | クラスはトランザクションの詳細行に適用され、クライアントやプロジェクトに結び付けられていないセグメントを追跡できます。 このテーブルは、クラス ID、名前、サブクラス、およびステータスを記録します。 |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | customers テーブルには、顧客の ID、名前、請求先住所、配送先住所、電話番号、電子メールアドレスなど、顧客に関するすべての情報が格納されます。 |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | 部門テーブルには、部門 ID、名前、タイプ（部門と最上位レベルの部門）が含まれます。 |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | 従業員テーブルには、会社で働く人に関する情報が記録されます。 会社が給与対応の場合、属性には従業員 ID、名前、住所、電話番号、請求可能情報が含まれます。 |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | 品目テーブルには、会社が販売している製品やサービスの詳細が表示されます。 この表には、品目 ID、名称、説明、単価、タイプ、購入情報、手持数量、収入および資産勘定情報が含まれます。 |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | 支払い方法テーブルは、商品やサービスに対して受け取った支払い方法を記録します。 支払 ID、タイプ、名前が含まれます。 |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | このテーブルには、税務署に関する情報（税務署 ID を含む）と、購入および販売の税金に関する追跡情報が記録されます。 |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | 税コードは、製品、サービスおよび顧客の税ステータス（課税対非課税）を追跡するために使用されます。 税コード表には、税コード ID、名称、摘要、ステータス、課税ステータス、税率および税グループが含まれます。 |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | 税率は、税負債の計算に使用されます。 この表には、税率 ID、名前、説明、税率、税務署名などが含まれます。 |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | このエンティティは、販売が行われる条件を表します。 キーワードテーブルには、キーワード ID、名前、タイプ、割引率および期限が含まれます。 |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | 仕入先テーブルには、購入元の仕入先に関する情報が含まれます。 テーブル属性には、ベンダー ID、会社名、アカウント番号、アカウント残高、1099 ステータス、請求先住所、電話番号、電子メールアドレス、Web アドレスが含まれます。 |

{style="table-layout:auto"}

## 関連：

* [接続中 [!DNL QuickBooks]](../integrations/quickbooks.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
