---
title: SQL 計算列の作成と使用
description: 新しいAdobe Commerce Intelligence アーキテクチャで、SQL 計算列の形式で高度な列を作成する方法を説明します。
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, SQL Report Builder, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '816'
ht-degree: 0%

---

# SQL 計算列の作成

このトピックでは、 `Calculation` 列タイプ（を使用してテーブルに追加できます） [Data Warehouse管理](../data-warehouse-mgr/tour-dwm.md). 以下に、SQL 計算の動作、使用理由、SQL 計算の作成プロセスを示します。2 つの例があります。

**説明**

過去に、みなされた列 `advanced` ここでおこなえるのは、カスタマーサクセスチームのアナリストのみです。 [!DNL Adobe Commerce Intelligence]. これで、すべての機能がエンドユーザーに提供され、高度な列は `SQL Calculation` 新しい列 [!DNL Commerce Intelligence] アーキテクチャ。

The `Calculation` 列タイプは、Data Warehouseマネージャのオプションとして使用できるようになりましたが、同じテーブル操作で、PostgreSQL ロジックを使用してテーブルの列を変換できます。 で使用できる関数と演算子に関するドキュメント `Calculation` 列の型は PostgreSQL の Web サイトで見つかります [ここ](https://www.postgresql.org/docs/9.6/functions.html).

を使用して作成できる様々な列 `Calculation` 列はほとんど無制限ですが、ほとんどの列は、次の例で使用される IF-THEN 文と基本的な算術演算を使用して作成できます。

**例 1：顧客の最後の注文は何ですか。**

ほとんどのアカウントには、 `Is customer's last order?` 彼らの `orders` リピート購入率およびチャーン顧客に関する分析を実行するテーブル。 アカウントが新しいアーキテクチャ上にある場合、この列は `Calculation` 列とは、以下のスクリーンショットで確認できます。

![](../../assets/Is_customer_s_last_order.png)

The `Is customer's last order?` 列は、入力を使用します `Customer's lifetime number of orders` および `Customer's order number` 別名 `A` および `B` それぞれ。

行ごとに、PostgreSQL の意味は次のとおりです。

* case：一連の If - Then 文が開始されます。
* when `A` null または `B` が null、null の場合：いずれかの入力が空の場合、出力も空にする必要があります。 これは、SQL エラーを防ぐためです
* when `A=B` その後 `Yes`: `Customer's lifetime number of orders` 次と等しい `Customer's order number` この行に対して、を返します。 `Yes`. したがって、顧客が 4 回注文した場合、4 回目の注文の行が戻ります `Yes` 対象： `Is customer's last order?`
* else `No`：文が満たされた場合に他のどれも満たされない場合は、を返します。 `No`
* end: If - Then 文を終了します。

この列で返される値 (`NULL`, `Yes`, `No`) に数字以外の文字が含まれている場合、ここでのデータ型は String です。

**例 2：注文品目の合計値（数量*価格）**

多くの顧客は、品目レベルで売上高を分析し、 `product name` または `category`. ほとんどのデータベースは、実際には注文での製品の売上高を提供しません。代わりに、注文で販売された数量と品目の価格を提供します。

製品売上高分析を有効にするために、ほとんどのアカウントには `Order item total value (quantity * price)` 彼らの `Orders Items` 表。 アカウントが新しいアーキテクチャ上にある場合、この列は、 `Calculation` 列とは、以下のスクリーンショットで確認できます。

![](../../assets/Order_item_total_value.png)

コマーススキーマで、 `Order item total value (quantity * price)` 列は、入力を使用します `qty ordered` および `base price` 別名 `A` および `B` それぞれ。

この新しい列から返される値は、dolles と cents の値なので、正しいデータタイプは `Decimal(10,2)`.

**力学**

新しい `Calculation` 列は、 **[!DNL Manage Data > Data Warehouse]** を次に示します。

![](../../assets/blobid2.png)

ここから、 `Calculation` 列に次の手順に従います。

1. 追加するテーブルを選択します。 `Calculation` 列。
1. 正しい表を見ながら、 **[!UICONTROL Create New Column]** をクリックします。
1. 次から： `Select a definition` ドロップダウン、選択 `Same Table`.
1. 選択 `Calculation` として `column definition equation`.
1. 列名を入力します。
1. を選択します。 `input` 新しい列のロジックで使用されるテーブルの列。 追加する各列には文字のエイリアスが割り当てられ、最初の列は `A`、2 つ目は `B` など。
1. ウィンドウで、入力のレターエイリアスを使用して、新しい列の PostgreSQL ロジックを入力します。 SQL の計算は、SQL クエリの SELECT 文と FROM 文の間のすべてのロジックを含む、1 つの列定義に制限する必要があります。 任意の入力文字を使用する SQL キーワードは、小文字にする必要があります。 例えば、 `CASE` 文は小文字で記述する必要があります。 `case`. このシステムでは、大文字を想定しています。 `A` は、入力の 1 つを指します。
1. 適切なデータ型を選択します。
   * `Integer`  — 整数
   * `Decimal(10,2)`  — 合計 10 桁の 10 進数で、そのうち 2 は小数点の右側にある
   * `String`  — 数字以外の文字を使用する任意の種類のテキストまたは一連の文字
   * `Datetime` - yyyy-MM-dd hh:mm:ss 形式

1. クリック **[!UICONTROL test column]**. これにより、各入力に対して 5 つのテスト値のリストが生成され、テスト値の各セットに対して手順 6 のロジックの結果が表示されます。 SQL のいずれかの部分でエラーが生成された場合は、適切なエラーメッセージが返されます。 サンプル結果は、すべての入力列がネイティブフィールドの場合にのみ生成できます。 いずれかの入力列が計算列である場合は、指標に列を追加し、ビジュアルReport Builderで表示して、結果を検証する必要があります

1. 結果が正しく表示されたら、 **[!UICONTROL Save]**. この列は使用可能です。
