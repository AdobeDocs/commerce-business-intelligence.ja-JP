---
title: SQL 計算列の作成および使用
description: 新しいAdobe Commerce Intelligence アーキテクチャで SQL 計算列の形式で詳細列を作成する方法を説明します。
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, SQL Report Builder, Commerce Tables
source-git-commit: 8090c2e0f17f0e8d3bdec668ce546206bf024691
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# SQL 計算列の作成

このトピックでは、 `Calculation` 列タイプ（を使用してテーブルに追加できます） [Data Warehouse管理者](../data-warehouse-mgr/tour-dwm.md). 次に、SQL 計算の機能、使用する理由、SQL 計算を作成するプロセスを説明し、2 つの例を示します。

**説明**

以前は、と見なされる列 `advanced` は、カスタマーサクセスチームのアナリスト（）のみが実行できます。 [!DNL Adobe Commerce Intelligence]. これで、すべての機能がエンドユーザーの手に渡り、次の形式で高度な列を作成できます `SQL Calculation` 新規の列 [!DNL Commerce Intelligence] アーキテクチャ。

この `Calculation` カラム型は、Data Warehouseマネージャのオプションとして使用できるようになりましたが、PostgreSQL ロジックを使用してテーブル上のカラムを変換できる同じテーブル操作です。 で使用できる関数および演算子に関するドキュメント `Calculation` 列タイプは PostgreSQL の web サイトで確認できます。 [こちら](https://www.postgresql.org/docs/9.6/functions.html).

で作成できる様々な列 `Calculation` 列はほとんど無制限ですが、ほとんどの列は、以下の例で使用される IF-THEN 文と基本的な算術演算を使用して作成できます。

**例 1：顧客の最後の注文か**

ほとんどのアカウントには、という列があります `Is customer's last order?` ユーザーの `orders` リピート購入率とチャーン済み顧客の分析を実行するテーブル。 アカウントが新しいアーキテクチャ上にある場合、この列はを使用して構築されます。 `Calculation` 以下のスクリーンショットに示すように、列とは次の通りです。

![](../../assets/Is_customer_s_last_order.png)

この `Is customer's last order?` 列は入力を使用 `Customer's lifetime number of orders` および `Customer's order number` 別名 `A` および `B` それぞれ。

1 行ずつ、PostgreSQL の意味は次のとおりです。

* ケース：一連の If - Then ステートメントを開始します
* 条件 `A` is null または `B` is null then null：いずれかの入力が空の場合、出力も空にする必要があります。 これは SQL エラーを防ぐためです
* 条件 `A=B` その後 `Yes`：次の場合： `Customer's lifetime number of orders` 等しい `Customer's order number` この行に対して、を返します `Yes`. したがって、顧客が 4 件の注文を行った場合、4 番目の注文の行は次のようになります `Yes` （用） `Is customer's last order?`
* else `No`：ステートメントが満たされた場合に他のいずれも返さない場合は、が返されます `No`
* end: If - Then ステートメントが終了します

この列から返される可能性のある値（`NULL`, `Yes`, `No`）に数字以外の文字が含まれているので、ここでのデータタイプは文字列です。

**例 2：受注品目合計値（数量*価格）**

多くの顧客は、収益を項目レベルで分析し、次のようなフィールドでスライスすることを好んでいます `product name` または `category`. ほとんどのデータベースでは、実際には製品の売上高は注文で提供されるのではなく、注文で販売された数量と品目の価格が提供されます。

製品売上高分析を有効にするために、ほとんどのアカウントには列があります。 `Order item total value (quantity * price)` ユーザーの `Orders Items` テーブル。 アカウントが新しいアーキテクチャ上にある場合、この列もを使用して作成されます。 `Calculation` 以下のスクリーンショットに示すように、列とは次の通りです。

![](../../assets/Order_item_total_value.png)

Commerce スキーマでは、 `Order item total value (quantity * price)` 列は入力を使用 `qty ordered` および `base price` 別名 `A` および `B` それぞれ。

この新しい列から返される値は、ドルとセント単位なので、正しいデータタイプは次のようになります。 `Decimal(10,2)`.

**仕組み**

新品 `Calculation` に移動して、列をテーブルに追加できます。 **[!DNL Manage Data > Data Warehouse]** 次に示します。

![](../../assets/blobid2.png)

ここから、 `Calculation` 列を作成するには、次の手順に従います。

1. を追加するテーブルを選択 `Calculation` 列。
1. 正しいテーブルで、 **[!UICONTROL Create New Column]** をクリックします。
1. から `Select a definition` ドロップダウン、選択 `Same Table`.
1. を選択 `Calculation` as the `column definition equation`.
1. 列名を入力します。
1. を選択します。 `input` 新しい列のロジックで使用されるテーブルの列。 追加する各列には文字のエイリアスが割り当てられるので、最初の列はになります。 `A`2 つ目はです。 `B` その他。
1. ウィンドウで、入力の文字エイリアスを使用して、新しい列に対する PostgreSQL ロジックを入力します。 SQL 計算は、SQL 問合せの SELECT 文と FROM 文の間のすべてのロジックを含む、単一の列の定義に限定する必要があります。 SQL キーワードで任意の入力文字を使用する場合は、小文字にする必要があります。 例えば、 `CASE` ステートメント、小文字で記述する必要があります –  `case`. システムは大文字を想定します `A` 入力の 1 つを指します。
1. 適切なデータタイプを選択します。
   * `Integer`  – 整数
   * `Decimal(10,2)`  – 小数点の右側に 2 が表示される、合計 10 桁の 10 進数
   * `String`  – 数字以外を使用する任意のタイプのテキストまたは一連の文字
   * `Datetime` - `yyyy-MM-dd hh:mm:ss` 形式

1. クリック **[!UICONTROL test column]**. これにより、各入力に対して 5 つのテスト値のリストが生成され、各テスト値セットに対する手順 6 のロジックの結果が表示されます。 SQL のいずれかの部分でエラーが発生した場合は、適切なエラーメッセージが返されます。 サンプル結果は、すべての入力列がネイティブフィールドの場合にのみ生成できます。 入力列のいずれかが計算列の場合は、列を指標に追加し、ビジュアルReport Builderで表示して結果を検証する必要があります

1. 結果に満足したら、をクリックします **[!UICONTROL Save]**. この列は使用できます。
