---
title: QuickBooks データの期待値
description: 分析のための関連データフィールドを簡単に追跡する方法を説明します。
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/aMWa4wHUfzDfBSSRKAkqqnYBEp481pfULZjJJpbe-oI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
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
source-wordcount: 1090
ht-degree: 0%

---

# [!DNL QuickBooks] データが必要です

[&#128279;](../../../data-analyst/importing-data/integrations/quickbooks.md)&#x200B; アカウント  [!DNL QuickBooks] を接続した後、[Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)を使用して、分析用の関連データフィールドを簡単に追跡できます。 &#x200B;次の表は、Data Warehouseで作成されます。

トラッキングに使用できるすべてのフィールドを表示するには、テーブル名の列のリンクをクリックします。

## トランザクションエンティティ {#transactionentities}

| **テーブル名** | **説明** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | `bills` テーブルには、AP トランザクション、またはサードパーティからの支払い要求に関する情報が含まれています。 属性には、通貨タイプ、為替レート、合計金額、期日、残高などが含まれます。 |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment` エンティティは、ベンダーから受け取った請求書の支払いの最終取引です。 この表には、ベンダー情報、支払いタイプ、合計金額、取引日などが含まれます。 |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | `creditmemos` テーブルには、全額支払いと一部支払いの両方の返金またはクレジットであるトランザクションが記録されます。 属性には、顧客の名前、顧客の請求情報と配送情報、金額、日付などが含まれます。 |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits`には、`Undeposited Funds` アカウントに保持された後にアセット アカウントに移動した直接預金と顧客支払いが含まれます。 属性には、金額、入金ID、日付が含まれます。 |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates`は、商品またはサービスの価格の提案を含む顧客に与えられたトランザクションです。 このテーブルには、金額、割引情報、顧客情報、日付が記録されます。 |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices`は、顧客が後で支払う販売フォームです。 請求書テーブルには、入金情報、日付、行項目、税情報、顧客情報が記録されます。 |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | `journalentries` テーブルには、ジャーナルエントリ ID、トランザクション日、行項目情報を含むARおよびAP アカウント情報が記録されます。 |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | `payment` レコードには、支払ID、適用済みおよび未適用の金額、取引日、トランザクションタイプ、処理ステータスなどの属性が含まれます。 |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | `purchases` テーブルは経費を表し、購入ID、支払いタイプ、金額、および任意の行項目情報が含まれます。 |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | `purchaseorders` テーブルには、ベンダーに送信された商品のリクエストが保持されます。 この表には、仕入先情報、発注書ID、取引日、明細項目情報、合計金額およびAP アカウント情報が含まれます。 |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | `refundreceipts` テーブルには、顧客に対する返金が記録されています。 属性には、返金ID、行項目情報、合計金額、顧客情報、残高が含まれます。 |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | `salesreceipts` テーブルには、販売伝票ID、行項目情報、合計金額、顧客情報、取引日、および任意の預金など、顧客に与えられた販売伝票の情報が記録されます。 |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | `timeactivities` テーブルには、ベンダーや従業員の時間レコードが保持され、時間アクティビティ ID、従業員/ベンダー情報、時間ログ、アクティビティの説明、記録された日付が含まれます。 |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | `transfers` テーブルには、アカウント間で移動された資金に関する情報が記録されます。 属性には、転送ID、金額、アカウント情報、日付が含まれます。 |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | ベンダークレジットとは、ベンダーに提供される返金またはクレジットであるAP トランザクションのことです。 `vendorcredits` テーブルには、仕入先クレジット ID、行項目情報、仕入先情報、AP アカウント、合計金額、日付が含まれています。 |

{style="table-layout:auto"}

## 名前リストエンティティ {#namelistentities}

| **テーブル名** | **説明** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | このテーブルには、アカウント ID、名前、ステータス、タイプ、残高、通貨、作成時間が含まれます。 |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | この表には、予算ID、名前、開始日と終了日、タイプ、ステータスおよび詳細など、会社予算に関連するすべての情報が記録されます。 |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | トランザクションの詳細行に適用されるクラスを使用すると、クライアントまたはプロジェクトに関連付けられていないセグメントを追跡できます。 このテーブルには、クラス ID、名前、サブクラス、およびステータスが記録されます。 |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | `customers` テーブルには、お客様のID、名前、請求先住所と配送先住所、電話番号、電子メールアドレスなど、お客様に関連するすべての情報が格納されます。 |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | `departments` テーブルには、部署ID、名前、種類（下位部署と最上位の部署の比較）が含まれています。 |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | `employees` テーブルには、会社で働くユーザーに関する情報が記録されます。 属性には、会社が給与計算に対応している場合の従業員ID、名前、住所、電話番号、請求可能な情報が含まれます。 |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | `items` テーブルには、会社が販売する製品またはサービスの詳細が含まれています。 この表には、品目ID、名称、説明、単価、タイプ、購入情報、手持数量、収益および資産勘定情報が含まれます。 |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | `paymentmethods` テーブルには、商品とサービスに対して受け取った支払い方法が記録されます。 支払いID、タイプ、名前が含まれます。 |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | この表は、税務機関IDを含む税務機関に関する情報と、購買および販売の税金に関する追跡情報を示しています。 |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | 税コードは、製品、サービス、および顧客の税金ステータス（課税対象と非課税対象）を追跡するために使用されます。 `taxcodes` テーブルには、税コード ID、名前、説明、ステータス、課税状態、税率、および税グループが含まれています。 |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | 税率は、税負担を計算するために使用されます。 この表には、税率ID、名前、説明、税率、税務エージェントなどが含まれます。 |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | このエンティティは、販売が行われる条件を表します。 用語テーブルには、用語「ID」、「名前」、「タイプ」、「割引率」および「期限日」が含まれます。 |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | 「ベンダー」テーブルには、購入するベンダーに関する情報が含まれます。 テーブル属性には、ベンダーID、会社名、アカウント番号、アカウント残高、1099 ステータス、請求先住所、電話番号、メールアドレス、web アドレスが含まれます。 |

{style="table-layout:auto"}

## 関連：

* [接続中 [!DNL QuickBooks]](../integrations/quickbooks.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
