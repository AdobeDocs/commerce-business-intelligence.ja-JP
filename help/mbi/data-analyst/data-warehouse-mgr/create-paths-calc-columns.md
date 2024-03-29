---
title: 計算列のパスの作成または削除
description: 列を作成するテーブルと、情報を取り込むテーブルとの関連を示すパスを定義する方法を説明します。
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# 計算列のパスの作成または削除

## 計算列リフレッシャ

条件 [計算列の作成](../data-warehouse-mgr/creating-calculated-columns.md) Data Warehouseで、列を作成するテーブルが、情報を取り込むテーブルとどのように関連しているかを示すパスを定義するよう求められます。 パスを正しく作成するには、次の 2 つを理解する必要があります。

1. データベース内のテーブルの相互関係
1. この関係を定義するプライマリキーと外部キー

この情報がわかっている場合は、このトピックの手順に従って、簡単にパスを作成できます。 組織の技術エキスパートに問い合わせるか、 [Professional Services チーム](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## テーブルの関係とキーの種類に関するリファラー {#refresher}

### テーブルの関係 {#relationships}

この概念については、 [テーブルの関係についてと評価の記事](../../data-analyst/data-warehouse-mgr/table-relationships.md)でも簡単なまとめは誰も傷つけないでしょ？

テーブルは、次の 3 つの方法のいずれかで相互に関連付けることができます。

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | 人と運転免許証番号との関係。 1 人の人が持つ運転免許証番号は 1 つだけで、1 人の運転免許証番号は 1 人の人にしか属していません。 |
| **`one-to-many`** | 注文と品目の関係 — 注文に多数の品目を含めることができますが、品目は 1 つの注文に属します。 この場合、注文テーブルは一方の側で、項目テーブルは多方の側です。 |
| **`many-to-many`** | 製品とカテゴリ間の関係：製品は多くのカテゴリに属することができ、カテゴリは多くの製品を含むことができます。 |

{style="table-layout:auto"}

2 つのテーブル間の関係が理解されたら、どのパスを作成して情報をテーブル間に移すかを決定するために使用できます。 この次の手順では、テーブルの関係を容易にするプライマリキーと外部キーを知る必要があります。

### プライマリと外部キー {#keys}

A `Primary Key` は、テーブル内で一意の値を生成する、変更されない列または列のセットです。 例えば、顧客が Web サイトで注文をすると、新しい行が `orders` 買い物かごに新しい `order_id`. この `order_id` では、顧客とビジネスの両方が特定の注文の進行状況を追跡できます。 注文 ID は一意なので、通常は `Primary Key` の `orders` 表。

A `Foreign Key` は、 `Primary Key` 別のテーブルの列。 外部キーはテーブル間で参照を作成するので、アナリストは簡単にレコードを検索してリンクできます。 各顧客に属している注文を知りたがったとします。 The `customer id` 列 (`Primary Key` の `customers` 表 ) と `order_id` 列 (`Foreign Key` （内） `customers` テーブル、を参照 `Primary Key` の `orders` 表 ) では、この情報をリンクおよび分析できます。 パスを作成する際に、 `Primary Key` および `Foreign Key`.

## パスの作成 {#createpath}

Data Warehouseで列を作成する場合は、あるテーブルから別のテーブルに情報を取り込むためのパスを定義する必要があります。 テーブル間にパスが存在するので、パスが事前に設定される場合がありますが、パスが存在しない場合は、作成する必要があります。

A と B の関係を使用 **顧客** および **注文件数** どのように行われたかを示す 分類：

* 関係は `one-to-many` ：顧客は多数の注文を持つことができますが、1 つの注文には 1 つの顧客のみを持つことができます。 これにより、関係の方向、または計算列を作成する場所が示されます。 この場合、 `orders` テーブルを `customers` 表。
* The `primary key` 次を使用します。 `customers.customerid`、または `customer ID` 列の `customers` 表。
* The `foreign key` 次を使用します。 `orders.customerid`、または `customer ID` 列の `orders` 表。

次に、パスを作成できます。

1. クリック **[!UICONTROL Data > Data Warehouse]**.
1. 表の一覧で、列を作成する表をクリックします。 この例では、 `customers` 表。
1. テーブルスキーマが表示されます。 クリック **[!UICONTROL Create New Column]**.
1. 列に名前を付けます（例： ）。 `Customer's orders`.
1. 列の定義を選択します。 以下を確認します。 [計算列ガイド](../data-warehouse-mgr/creating-calculated-columns.md) 便利なチートシートのために
1. Adobe Analytics の [!UICONTROL Select table and column] ドロップダウンで、 **[!UICONTROL Create new path]** オプション。

   ![計算列モーダルのパスの作成](../../assets/Creating_Paths_modal.png)

1. ドロップダウンを使用して、各テーブルのプライマリキーと外部キーを選択します。

   次の日： `Many` 「 」で、「 」を選択します。 `orders.customerid`  — 顧客は多くの注文を受けることができます。

   次の日： `One` 「 」で、「 」を選択します。 `customers.customerid`  — 注文には 1 人の顧客のみを含めることができます。

1. クリック **[!UICONTROL Save]** パスを保存し、列の作成を終了します。

### パス作成の制限 {#limits}

* **[!DNL Commerce Intelligence]プライマリキーと外部キーの関係を推測できません**. アカウントに誤ったデータを導入したくないので、パスの作成は手動でおこなう必要があります。

* **現在、パスは 2 つの異なるテーブル間でのみ指定できます**. 再作成しようとしているロジックには、2 つ以上のテーブルが含まれていますか？ (1) 最初に列を中間テーブルに結合し、次に「最終宛先」テーブルに結合する、または (2) [Professional Services チーム](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) をクリックして、目標に対する最適なアプローチを見つけます。

* **列は、一度に 1 つのパスの外部キー参照のみにすることができます**. 例えば、 `order_items.order_id` ポイント `orders.id`を、 `order_items.order_id` 他のものを指すことはできません。

* **`Many-to-many`パスは技術的に作成できますが、どちらも真でないので、多くの場合、不正なデータを生成します `one-to-many` 外部キー**. これらのパスに最も近い方法は、常に、特定の分析に依存します。 RJ アナリストチームに相談して、最適なソリューションを明らかにしてください。

上記の 1 つ以上の制限により計算列を作成できない場合は、サポートに連絡して、現在の列の説明を確認してください

## 計算列のパスを削除する {#delete}

Data Warehouse内に間違ったパスを作成しましたか？ 春の掃除をして片付けたいのか？ アカウントからパスを削除する必要がある場合は、 [チケットをAdobe・サポート・アナリストに送る](../../guide-overview.md#Submitting-a-Support-Ticket). **必ずパスの名前を含めてください。**

## 折り返し {#wrapup}

これで、Data Warehouse内の計算列のパスを作成することに慣れました。 それでも特定のパスが不明な場合は、常に「 **[!UICONTROL Support]** の [!DNL Commerce Intelligence] アカウントを使用してサポートを受けてください。

## 関連

* [テーブルの関係の理解と評価](../data-warehouse-mgr/table-relationships.md)
* [計算列のパスの作成](../data-warehouse-mgr/create-paths-calc-columns.md)
* [計算列のタイプ](../data-warehouse-mgr/calc-column-types.md) を作成しようとしています。
