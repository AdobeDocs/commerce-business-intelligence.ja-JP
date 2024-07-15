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

ここでは、[Data Warehouseマネージャー ](../data-warehouse-mgr/tour-dwm.md) を使用してテーブルに追加できる `Calculation` 列タイプの目的と使用方法の概要を説明します。 次に、SQL 計算の機能、使用する理由、SQL 計算を作成するプロセスを説明し、2 つの例を示します。

**説明**

以前は、[!DNL Adobe Commerce Intelligence] でカスタマーサクセスチームのアナリストのみが、`advanced` と見なされた列を実行できました。 これで、すべての機能がエンドユーザーの手に委ねられ、新しい [!DNL Commerce Intelligence] アーキテクチャ上に `SQL Calculation` 列の形式で高度な列を作成できます。

Data Warehouseマネージャのオプションとして使用できるようになった `Calculation` 列タイプは、テーブル上の列を PostgreSQL ロジックを使用して変換できる同じテーブル操作です。 `Calculation` 列タイプで使用できる関数と演算子に関するドキュメントは、PostgreSQL の web サイト [ こちら ](https://www.postgresql.org/docs/9.6/functions.html) にあります。

`Calculation` 列を使用して作成できる列にはほとんど制限はありませんが、ほとんどの列は、以下の例で使用される IF-THEN 文と基本算術式を使用して作成できます。

**例 1：顧客の最後の注文か？**

ほとんどのアカウントには、`orders` テーブルに `Is customer's last order?` という列があり、リピート購入率とチャーンされた顧客に関する分析を実行します。 アカウントが新しいアーキテクチャ上にある場合、この列は `Calculation` の列を使用して作成され、次のスクリーンショットで確認できます。

![](../../assets/Is_customer_s_last_order.png)

`Is customer's last order?` の列では、入力 `Customer's lifetime number of orders` と `Customer's order number` のエイリアスをそれぞれ `A` と `B` として使用します。

1 行ずつ、PostgreSQL の意味は次のとおりです。

* ケース：一連の If - Then ステートメントを開始します
* `A` が null または `B` が null の場合は null：いずれかの入力が空の場合、出力も空にする必要があります。 これは SQL エラーを防ぐためです
* `A=B` の場合 `Yes`:`Customer's lifetime number of orders` がこの行の `Customer's order number` と等しい場合は、`Yes` を返します。 したがって、顧客が 4 件の注文を行った場合、4 番目の注文の行は `Is customer's last order?` の `Yes` を返します
* else `No`：ステートメントが満たされた場合に他のどれも返されない場合は、`No` を返します
* end: If - Then ステートメントが終了します

この列から返される可能性のある値（`NULL`、`Yes`、`No`）には数字以外の文字が含まれているので、ここでのデータタイプは文字列です。

**例 2：受注品目合計値（数量*価格）**

多くの顧客は、`product name` や `category` などのフィールドでスライスして、品目レベルで売上高を分析したいと考えています。 ほとんどのデータベースでは、実際には製品の売上高は注文で提供されるのではなく、注文で販売された数量と品目の価格が提供されます。

製品の売上高分析を有効にするために、ほとんどのアカウントの `Orders Items` テーブルには `Order item total value (quantity * price)` という列があります。 アカウントが新しいアーキテクチャ上にある場合、この列も `Calculation` の列を使用して作成され、次のスクリーンショットで確認できます。

![](../../assets/Order_item_total_value.png)

Commerce スキーマの `Order item total value (quantity * price)` 列では、入力 `qty ordered` とエイリアス `base price` をそれぞれ `A` と `B` として使用します。

この新しい列から返される値はドルとセント単位なので、正しいデータ型は `Decimal(10,2)` です。

**力学**

次に示すように **[!DNL Manage Data > Data Warehouse]** に移動して、新しい `Calculation` 列をテーブルに追加できます。

![](../../assets/blobid2.png)

ここから、次の手順に従って `Calculation` しい列を作成できます。

1. `Calculation` 列を追加するテーブルを選択します。
1. 正しいテーブルで、画面の右上にある **[!UICONTROL Create New Column]** をクリックします。
1. `Select a definition` ドロップダウンから「`Same Table`」を選択します。
1. `column definition equation` として `Calculation` を選択します。
1. 列名を入力します。
1. 新しい列のロジックで使用されているテーブルから `input` 列を選択します。 追加する各列には文字のエイリアスが割り当てられ、最初の列は `A`、2 番目の列は `B` というようになります。
1. ウィンドウで、入力の文字エイリアスを使用して、新しい列に対する PostgreSQL ロジックを入力します。 SQL 計算は、SQL 問合せの SELECT 文と FROM 文の間のすべてのロジックを含む、単一の列の定義に限定する必要があります。 SQL キーワードで任意の入力文字を使用する場合は、小文字にする必要があります。 例えば、`CASE` ステートメントを使用する場合は、小文字 – `case` で記述する必要があります。 システムでは、大文字の `A` が入力の 1 つを指すと想定します。
1. 適切なデータタイプを選択します。
   * `Integer` – 整数
   * `Decimal(10,2)` – 小数点の右側に 2 が表示される、合計 10 桁の 10 進数
   * `String` – 数値以外を使用する任意のタイプのテキストまたは一連の文字
   * `Datetime` - `yyyy-MM-dd hh:mm:ss` 形式

1. 「**[!UICONTROL test column]**」をクリックします。 これにより、各入力に対して 5 つのテスト値のリストが生成され、各テスト値セットに対する手順 6 のロジックの結果が表示されます。 SQL のいずれかの部分でエラーが発生した場合は、適切なエラーメッセージが返されます。 サンプル結果は、すべての入力列がネイティブフィールドの場合にのみ生成できます。 入力列のいずれかが計算列の場合は、列を指標に追加し、ビジュアルReport Builderで表示して結果を検証する必要があります

1. 結果に満足したら、「**[!UICONTROL Save]**」をクリックします。 この列は使用できます。
