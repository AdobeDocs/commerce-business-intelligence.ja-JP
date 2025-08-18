---
title: 計算列のパスの作成または削除
description: 列を作成するテーブルと情報を取り込むテーブルとの関係を説明するパスの定義方法を説明します。
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# 計算列のパスの作成または削除

## 計算列の更新

Data Warehouseで [ 計算列の作成 ](../data-warehouse-mgr/creating-calculated-columns.md) を行う場合、列を作成するテーブルと情報を取り込むテーブルとの関係を説明するパスを定義するように求められます。 パスを正常に作成するには、次の 2 つの点を知っておく必要があります。

1. データベース内のテーブルの相互関係
1. この関係を定義する主キーと外部キー

この情報を知っていれば、このトピックの手順に従ってパスを簡単に作成できます。 所属する組織の技術エキスパートに問い合わせるか、[Professional Services チーム ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) にお問い合わせください。

## テーブルのリレーションシップとキーの種類に関する更新 {#refresher}

### テーブルの関係 {#relationships}

この概念については、[ テーブル関係の理解と評価 ](../../data-analyst/data-warehouse-mgr/table-relationships.md) の記事で説明していますが、簡単な概要では誰も傷つけないですよね？

テーブルは、次の 3 つの方法のいずれかで相互に関連付けることができます。

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | 人物と運転免許証番号の関係。 運転免許証番号は 1 人につき、1 つの運転免許証番号は 1 人の人に属します。 |
| **`one-to-many`** | 注文と品目の関係：注文には多数の品目を含めることができますが、1 つの品目は 1 つの注文に属します。 この場合、orders テーブルは一側、items テーブルは多側です。 |
| **`many-to-many`** | 製品とカテゴリの関係：製品は多数のカテゴリに属することができ、カテゴリには多数の製品を含めることができます。 |

{style="table-layout:auto"}

2 つのテーブル間の関係を理解したら、あるテーブルから別のテーブルに情報を移動するために作成するパスを決定するために使用できます。 次の手順では、テーブルの関係を容易にする主キーと外部キーを把握する必要があります。

### プライマリと外部キー {#keys}

`Primary Key` は、テーブル内に一意の値を生成する、変更されない列または列のセットです。 例えば、顧客が web サイトで注文を行うと、買い物かごの `orders` テーブルに新しい行が追加され、新しい `order_id` が追加されます。 これにより、顧客とビジネスの両方がその特定の注文の進行状況を追跡で `order_id` るようになります。 注文 ID は一意なので、通常は `Primary Key` テーブルの `orders` です。

`Foreign Key` は、テーブル内に作成された列で、別のテーブルの `Primary Key` の列にリンクします。 外部キーを使用するとテーブル間で参照を作成できるので、アナリストはレコードを簡単に検索してリンクできます。 例えば、どの注文が各顧客に属しているかを知りたいと思ったとします。 `customer id` 列（`Primary Key` テーブルの `customers`）と `order_id` 列（`Foreign Key` テーブルの `customers`、`Primary Key` テーブルの `orders` を参照）を使用すると、この情報をリンクして分析できます。 パスを作成する際は、`Primary Key` と `Foreign Key` の両方を定義するよう求められます。

## パスの作成 {#createpath}

Data Warehouseで列を作成する場合、あるテーブルから別のテーブルに情報を移動するパスを定義する必要があります。 テーブル間にパスが存在するので、パスが事前入力される場合がありますが、これが発生しない場合は、パスを作成する必要があります。

**顧客** と **注文** の関係を使用して、どのように行われるかを示します。 分類：

* 関係は `one-to-many` です。顧客は多数の注文を持つことができますが、1 つの注文は 1 つの顧客しか持つことができません。 これにより、関係の方向や、計算列を作成する場所がわかります。 この場合、`orders` テーブルの情報を `customers` テーブルに取り込むことができます。
* 使用する `primary key` は、`customers.customerid` または `customer ID` テーブルの `customers` 列です。
* 使用する `foreign key` は、`orders.customerid` または `customer ID` テーブルの `orders` 列です。

これで、パスを作成できます。

1. 「**[!UICONTROL Data > Data Warehouse]**」をクリックします。
1. [ テーブル ] ボックスの一覧で、列を作成するテーブルをクリックします。 この例では、`customers` のテーブルです。
1. テーブルスキーマが表示されます。 「**[!UICONTROL Create New Column]**」をクリックします。
1. 列に名前（例：`Customer's orders`）を付けます。
1. 列の定義を選択します。 便利なチートシートについては、[ 計算列ガイド ](../data-warehouse-mgr/creating-calculated-columns.md) を参照してください。
1. [!UICONTROL Select table and column] ドロップダウンで、「**[!UICONTROL Create new path]**」オプションをクリックします。

   ![ 計算列モーダルのパスの作成 ](../../assets/Creating_Paths_modal.png)

1. ドロップダウンを使用して、各テーブルのプライマリキーと外部キーを選択します。

   `Many` 側では、`orders.customerid` を選択します – 覚えておいて、顧客は多くの注文を持つことができます。

   `One` 側では、`customers.customerid` を選択します。1 つの注文に含めることができる顧客は 1 つだけです。

1. 「**[!UICONTROL Save]**」をクリックしてパスを保存し、列の作成を終了します。

### パス作成の制限 {#limits}

* 主キーと外部キーの関係を推測で **[!DNL Commerce Intelligence]ません**。 誤ったデータをアカウントに導入しないので、パスの作成は手動で行う必要があります。

* **現在、パスは 2 つの異なるテーブル間でのみ指定できます**。 再作成しようとしているロジックには、2 つ以上のテーブルが含まれていますか？ その後、（1）列をまず仲介テーブルに結合してから「最終的な宛先」テーブルに結合するか、（2） [ プロフェッショナルサービスチーム ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) に相談して、目標に対する最適なアプローチを見つけることが理にかなっている場合があります。

* **列は、一度に 1 つのパスの外部キー参照のみとすることができます**。 例えば、`order_items.order_id` が `orders.id` を指している場合、`order_items.order_id` はそれ以外を指すことはできません。

* パス **`Many-to-many`技術的には作成できますが、どちらの側も真の外部キーではないため、多くの場合、不正なデータが生成され `one-to-many` す**。 これらのパスにアプローチする最適な方法は、常に特定の望ましい分析によって異なります。 RJ アナリスト・チームに問い合わせて、最適なソリューションを見つけます。

上記の 1 つ以上の制限事項により計算列を作成できない場合は、現在の列の説明を添えてサポートにお問い合わせください

## 集計列のパスの削除 {#delete}

Data Warehouseで間違ったパスを作成しましたか？ または、多分あなたは少し春のクリーニングをやって、片付けたいですか？ アカウントからパスを削除する必要がある場合は、[Adobe サポートアナリストにチケットを送る ](../../guide-overview.md#Submitting-a-Support-Ticket) ことができます。 **パス名を必ず含めてください。**

## まとめ {#wrapup}

これで、Data Warehouseで計算列のパスを適切に作成できるようになりました。 特定のパスが不明な場合は、いつでも **[!UICONTROL Support]** アカウントの [!DNL Commerce Intelligence] をクリックしてサポートを受けることができます。

## 関連

* [テーブルの関係の理解と評価](../data-warehouse-mgr/table-relationships.md)
* [計算列のパスの作成](../data-warehouse-mgr/create-paths-calc-columns.md)
* [ 集計列の種類 ](../data-warehouse-mgr/calc-column-types.md) を作成しようとしています。
