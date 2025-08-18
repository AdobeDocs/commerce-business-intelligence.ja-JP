---
title: 期待される QuickBooks データ
description: 分析に関連するデータフィールドを簡単にトラッキングする方法を説明します。
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# 予期される [!DNL QuickBooks] データ

[ アカウントに接続  [!DNL QuickBooks]  た ](../../../data-analyst/importing-data/integrations/quickbooks.md) 後、[Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) を使用して、関連するデータフィールドを簡単に追跡して分析できます。 Data Warehouseでは、次のテーブルが作成されます。

トラッキングに使用できるすべてのフィールドを表示するには、テーブル名列のリンクをクリックします。

## トランザクションエンティティ {#transactionentities}

| **テーブル名** | **説明** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | `bills` の表には、AP 取引に関する情報、または第三者からの支払い要求が含まれています。 属性には、通貨タイプ、為替レート、合計金額、期限、残高などが含まれます。 |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment` のエンティティは、仕入先から受け取った請求書の支払の最終トランザクションです。 この表には、仕入先情報、支払タイプ、合計金額、取引日などが含まれます。 |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | `creditmemos` の表には、全額支払と一部支払の両方の払戻または貸方である取引が記録されます。 一部の属性には、顧客の名前、顧客の請求および配送情報、金額、日付が含まれます。 |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits` の中には、直接預金と顧客支払が `Undeposited Funds` の口座に保持された後に資産口座に移動された場合が含まれます。 属性には、金額、預金 ID、日付が含まれます。 |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | 商品やサービスの価格の提案を含む、顧客に付与されるトランザクションが `Estimates` ります。 このテーブルには、金額、割引情報、顧客情報および日付が記録されます。 |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | 顧客が後で支払う販売フォームが `Invoices` ります。 請求書テーブルには、入金情報、日付、明細項目、税金情報および顧客情報が記録されます。 |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | `journalentries` の表には、仕訳 ID、取引日、明細品目情報など、AR および AP 勘定科目情報が記録されます。 |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | `payment` レコードには、支払 ID、適用済み金額と未適用金額、取引日、取引タイプ、処理ステータスなどの属性が含まれます。 |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | `purchases` の表は費用を表し、購入 ID、支払いタイプ、金額、行項目情報が含まれます。 |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | `purchaseorders` テーブルには、仕入先に送信される商品の要求が保持されます。 この表には、仕入先情報、発注 ID、取引日、明細品目情報、合計金額および AP 勘定情報が含まれます。 |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | `refundreceipts` テーブルには、顧客に与えられた払い戻しが記録されます。 属性には、返品受入 ID、明細品目情報、合計金額、顧客情報および残高が含まれます。 |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | `salesreceipts` の表には、顧客に付与された営業入金の情報が記録されます。営業入金 ID、明細品目情報、合計金額、顧客情報、取引日および預金が含まれます。 |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | `timeactivities` テーブルには、仕入先または従業員（あるいはその両方）の時間レコードが保持され、時間アクティビティ ID、従業員/仕入先情報、記録された時間、アクティビティの説明および記録された日付が含まれます。 |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | `transfers` テーブルには、勘定間で移動された資金に関する情報が記録されます。 属性には、転送 ID、金額、口座情報、日付が含まれます。 |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | 仕入先貸方とは、仕入先に払い戻しまたは貸方が付与される AP 取引です。 `vendorcredits` テーブルには、仕入先貸方 ID、明細行品目情報、仕入先情報、AP 勘定、合計金額および日付が含まれます。 |

{style="table-layout:auto"}

## 名前リストエンティティ {#namelistentities}

| **テーブル名** | **説明** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | このテーブルには、アカウント ID、名前、ステータス、タイプ、残高、通貨、作成時間が含まれます。 |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | このテーブルには、予算 ID、名前、開始日と終了日、タイプ、ステータス、詳細など、会社の予算に関するすべての情報が記録されます。 |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | トランザクションの詳細行に適用されるクラスを使用すると、クライアントまたはプロジェクトに結び付けられていないセグメントを追跡できます。 このテーブルには、クラス ID、名前、サブクラス、およびステータスが記録されます。 |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | `customers` テーブルには、顧客 ID、名前、請求先住所、発送先住所、電話番号、メールアドレスなど、顧客に関するすべての情報が保持されます。 |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | `departments` テーブルには、部門 ID、名前、タイプ（サブ部門とトップレベル部門）が含まれます。 |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | `employees` テーブルには、会社で働く人々に関する情報が記録されます。 属性には、従業員 ID、名前、住所、電話番号、請求可能な情報（会社が給与に対応している場合）が含まれます。 |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | `items` の表には、会社が販売する製品またはサービスの詳細が含まれています。 この表には、品目 ID、名称、摘要、単価、タイプ、購買情報、手持数量および収益と資産の勘定科目情報が含まれます。 |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | `paymentmethods` の表には、商品およびサービスに対して受け取った支払い方法が記録されます。 支払い ID、タイプおよび名前が含まれます。 |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | このテーブルには、税務代理店 ID を含む税務代理店に関する情報と、購入および販売に対する税金に関するトラッキング情報が記録されます。 |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | 税金コードは、製品、サービスおよび顧客の税金ステータス（課税対象と非課税対象）を追跡するために使用されます。 `taxcodes` の表には、税金コード ID、名称、摘要、ステータス、課税対象ステータス、税率および税金グループが含まれます。 |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | 税率は、納税義務の計算に使用されます。 このテーブルには、税率 ID、名前、説明、税率、税務エージェンシーなどが含まれます。 |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | このエンティティは、販売が行われる条件を表します。 用語テーブルには、用語 ID、名前、タイプ、割引率、期限が含まれます。 |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | 仕入先テーブルには、購入元の仕入先に関する情報が含まれています。 テーブル属性には、ベンダー ID、会社名、口座番号、口座残高、1099 ステータス、請求先住所、電話番号、メールアドレス、web アドレスが含まれます。 |

{style="table-layout:auto"}

## 関連：

* [接続  [!DNL QuickBooks]](../integrations/quickbooks.md)
* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
