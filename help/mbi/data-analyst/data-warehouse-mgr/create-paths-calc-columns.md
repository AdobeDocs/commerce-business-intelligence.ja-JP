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

条件 [計算列の作成](../data-warehouse-mgr/creating-calculated-columns.md) Data Warehouseでは、列を作成するテーブルと情報を取り込むテーブルとの関係を示すパスを定義するように求められます。 パスを正常に作成するには、次の 2 つの点を知っておく必要があります。

1. データベース内のテーブルの相互関係
1. この関係を定義する主キーと外部キー

この情報を知っていれば、このトピックの手順に従ってパスを簡単に作成できます。 組織の技術エキスパートに問い合わせるか、 [プロフェッショナルサービスチーム](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## テーブルのリレーションシップとキーの種類に関する更新 {#refresher}

### テーブルの関係 {#relationships}

この概念については、を参照してください [テーブルの関係に関する記事の理解と評価](../../data-analyst/data-warehouse-mgr/table-relationships.md)でも簡単にまとめると誰も傷つけないでしょ？

テーブルは、次の 3 つの方法のいずれかで相互に関連付けることができます。

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | 人物と運転免許証番号の関係。 運転免許証番号は 1 人につき、1 つの運転免許証番号は 1 人の人に属します。 |
| **`one-to-many`** | 注文と品目の関係：注文には多数の品目を含めることができますが、1 つの品目は 1 つの注文に属します。 この場合、orders テーブルは一側、items テーブルは多側です。 |
| **`many-to-many`** | 製品とカテゴリの関係：製品は多数のカテゴリに属することができ、カテゴリには多数の製品を含めることができます。 |

{style="table-layout:auto"}

2 つのテーブル間の関係を理解したら、あるテーブルから別のテーブルに情報を移動するために作成するパスを決定するために使用できます。 次の手順では、テーブルの関係を容易にする主キーと外部キーを把握する必要があります。

### プライマリと外部キー {#keys}

A `Primary Key` は、テーブル内で一意の値を生成する、変更されない列または列のセットです。 例えば、顧客が web サイトで注文を行うと、新しい行がに追加されます。 `orders` 新しいが入った、買い物かごのテーブル `order_id`. この `order_id` を使用すると、顧客と企業の両方が特定の注文の進行状況を追跡できます。 注文 ID は一意なので、通常はです `Primary Key` の `orders` テーブル。

A `Foreign Key` は、テーブル内に作成された、 `Primary Key` 別のテーブルの列。 外部キーを使用するとテーブル間で参照を作成できるので、アナリストはレコードを簡単に検索してリンクできます。 例えば、どの注文が各顧客に属しているかを知りたいと思ったとします。 この `customer id` 列（`Primary Key` の `customers` 表）および `order_id` 列（`Foreign Key` が含まれる `customers` テーブル、を参照 `Primary Key` の `orders` table）を使用すると、この情報をリンクして分析できます。 パスの作成時に、次の両方を定義するよう求められます `Primary Key` および `Foreign Key`.

## パスの作成 {#createpath}

Data Warehouseで列を作成する場合、あるテーブルから別のテーブルに情報を移動するパスを定義する必要があります。 テーブル間にパスが存在するので、パスが事前入力される場合がありますが、これが発生しない場合は、パスを作成する必要があります。

A と B の関係を利用する **顧客** および **注文件数** やり方を説明します。 分類：

* 関係はです `one-to-many`  – 顧客は多数の注文を持つことができますが、1 つの注文には 1 人の顧客のみを持つことができます。 これにより、関係の方向や、計算列を作成する場所がわかります。 この場合、以下からの情報を意味します。 `orders` テーブルは以下に取り込むことができます。 `customers` テーブル。
* この `primary key` を使用する `customers.customerid`、または `customer ID` 列： `customers` テーブル。
* この `foreign key` を使用する `orders.customerid`、または `customer ID` 列： `orders` テーブル。

これで、パスを作成できます。

1. クリック **[!UICONTROL Data > Data Warehouse]**.
1. [ テーブル ] ボックスの一覧で、列を作成するテーブルをクリックします。 この例では、です。 `customers` テーブル。
1. テーブルスキーマが表示されます。 クリック **[!UICONTROL Create New Column]**.
1. 列に名前を付けます（例：） `Customer's orders`.
1. 列の定義を選択します。 を確認してください。 [集計列ガイド](../data-warehouse-mgr/creating-calculated-columns.md) 便利なチートシートのために。
1. が含まれる [!UICONTROL Select table and column] ドロップダウンで、 **[!UICONTROL Create new path]** オプション。

   ![計算列モーダルのパスの作成](../../assets/Creating_Paths_modal.png)

1. ドロップダウンを使用して、各テーブルのプライマリキーと外部キーを選択します。

   日 `Many` 側で、を選択します `orders.customerid`  – 覚えておいて、顧客は多くの注文を持つことができます。

   日 `One` 側で、を選択します `customers.customerid`  – 注文には 1 人の顧客のみを含めることができます。

1. クリック **[!UICONTROL Save]** をクリックしてパスを保存し、列の作成を終了します。

### パス作成の制限 {#limits}

* **[!DNL Commerce Intelligence]プライマリ/外部キーの関係を推測できない**. 誤ったデータをアカウントに導入しないので、パスの作成は手動で行う必要があります。

* **現在、パスは 2 つの異なるテーブル間でのみ指定できます**. 再作成しようとしているロジックには、2 つ以上のテーブルが含まれていますか？ その後、（1）最初に列を中間テーブルに結合してから「最終宛先」テーブルに結合する、または（2）で [プロフェッショナルサービスチーム](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 目標に対する最適なアプローチを見つける。

* **列は、一度に 1 つのパスの外部キー参照のみにすることができます**. 例えば、 `order_items.order_id` 参照先 `orders.id`、次に `order_items.order_id` 他を指すことはできません。

* **`Many-to-many`パスは技術的には作成できますが、どちらの側も true ではないため、多くの場合、不正なデータが生成されます `one-to-many` 外部キー**. これらのパスにアプローチする最適な方法は、常に特定の望ましい分析によって異なります。 RJ アナリスト・チームに問い合わせて、最適なソリューションを見つけます。

上記の 1 つ以上の制限事項により計算列を作成できない場合は、現在の列の説明を添えてサポートにお問い合わせください

## 集計列のパスの削除 {#delete}

Data Warehouseで間違ったパスを作成しましたか？ または、多分あなたは少し春のクリーニングをやって、片付けたいですか？ アカウントからパスを削除する必要がある場合は、 [Adobeサポートアナリストにチケットを送信](../../guide-overview.md#Submitting-a-Support-Ticket). **パス名を必ず含めてください。**

## まとめ {#wrapup}

これで、Data Warehouseで計算列のパスを簡単に作成できるようになりました。 特定のパスが不明な場合は、いつでもクリックできます **[!UICONTROL Support]** が含まれる [!DNL Commerce Intelligence] お問い合わせください。

## 関連

* [テーブルの関係の理解と評価](../data-warehouse-mgr/table-relationships.md)
* [計算列のパスの作成](../data-warehouse-mgr/create-paths-calc-columns.md)
* [集計列の種類](../data-warehouse-mgr/calc-column-types.md) を作成しようとしています。
