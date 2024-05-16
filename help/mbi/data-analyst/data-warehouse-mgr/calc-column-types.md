---
title: 集計列の種類
description: 分析用にデータを拡張および最適化するための列を作成する方法を説明します。
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 0%

---

# 集計列の種類

* [同じテーブルの計算](#sametable)
* [1 対多の計算](#onetomany)
* [多対 1 の計算](#manytoone)
* [便利な参照マップ](#map)
* [高度な計算列](#advanced)

内 [Data Warehouse管理者](../data-warehouse-mgr/tour-dwm.md)を参照してください。また、列を作成して、分析用にデータを補強し最適化できます。 [この機能](../data-warehouse-mgr/creating-calculated-columns.md) アクセスするには、Data Warehouseマネージャで任意のテーブルを選択し、をクリックします **[!UICONTROL Create New Column]**.

ここでは、Data Warehouseマネージャを使用して作成できる列のタイプについて説明します。 また、説明、その列の視覚的なウォークスルーおよび [参照マップ](#map) 列の作成に必要なすべての入力。 計算列を作成する方法は 3 つあります。

1. [同じテーブルの計算列](#sametable)
1. [1 対多の計算列](#onetomany)
1. [多対 1 の計算列](#manytoone)

## 同じテーブルの計算列 {#sametable}

これらの列は、同じテーブルの入力列を使用して作成されます。

### 年齢 {#age}

年齢の計算列は、現在の時刻と入力時刻の間の秒数を返します。

次の例では、を作成します。 `Seconds since customer's most recent order` が含まれる `customers` テーブル。 これを使用して、内で購入を行っていない顧客（チャーンと呼ばれることもあります）のユーザーリストを作成できます `X days`.

![](../../assets/age.gif)

### 通貨換算

通貨換算計算列は、列のネイティブ通貨を目的の新しい通貨に変換します。

次の例では、を作成します。 `base\_grand\_total In AED`、変換 `base\_grand\_total` から AED のネイティブ通貨です。 `sales\_flat\_order` テーブル。 この列は、現地通貨でレポートを作成する複数通貨のストアに適しています。

Commerce クライアントの場合、 `base\_currency\_code` 通常、フィールドには現地通貨を格納します。 この `Spot Time` フィールドは、指標で使用された日付と一致する必要があります。

![](../../assets/currency_converter.png)

## 1 対多の計算列 {#onetomany}

`One-to-Many` 列 [2 つのテーブル間のパスを使用](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). このパスは、常に、属性が存在する 1 つのテーブルと、その属性が「再配置」される多数のテーブルを意味します。 パスは `foreign key--primary key` 関係。

### 結合された列 {#joined}

結合された列は、1 つのテーブルの属性を再配置します *対象：* 多数のテーブル。 典型的な 1 対多の例は、顧客（1 人）と注文（多数）です。

以下の例では、 `Customer's group\_id` ディメンションは、以下に結合されます `orders` テーブル。

![](../../assets/joined_column.gif)

## 多対 1 の計算列 {#manytoone}

これらの列は、1 対多の列と同じパスを使用しますが、データを反対方向に指します。 列は、多の側とは異なり、パスの片側に作成されます。 この関係により、列の値は集計、つまり、多側のデータポイントに対して実行される数学演算である必要があります。 多くの使用例がありますが、以下にいくつか示します。

### カウント {#count}

このタイプの計算列は、多数のテーブルの値の数を返します *を対象* 1 つのテーブル。

次の例では、ディメンションです `Customer's lifetime number of canceled orders` 次の日に作成される `customers` テーブル （フィルター付き） `orders.status`）に設定します。

![](../../assets/many_to_one.gif){: width=&quot;699&quot; height=&quot;351&quot;}

### 合計 {#sum}

合計計算列は、上の値の合計です `many` 1 つのテーブル上のテーブル。

これは、次のような顧客レベルのディメンションを作成するために使用できます `Customer's lifetime revenue`.

### 最小または最大 {#minmax}

最小または最大計算列は、多側にある最小または最大のレコードを返します。

これは、次のような顧客レベルのディメンションを作成するために使用できます `Customer's first order date`.

### が存在する {#exists}

計算列は、多側でのレコードの存在を判断するバイナリテストです。 つまり、新しい列はを返します。 `1` パスが各テーブルの 1 行以上を接続する場合、および `0` 接続できない場合。

このタイプのディメンションは、例えば、顧客が特定の製品を購入したことがあるかどうかを決定する場合があります。 間の結合の使用 `customers` テーブルと `orders` テーブル、特定の製品のフィルター、ディメンション `Customer has purchased Product X?` を作成できます。

## 便利な参照マップ {#map}

計算列を作成するときにすべての入力が何であるかを思い出すのに苦労している場合は、以下を作成するときにこの参照マップを手元に置いておいてください。

![](../../assets/merged_reference_map.png)

## 高度な計算列 {#advanced}

ビジネスに関する質問を分析し、回答しようとすると、必要な正確な列を作成できない状況が発生する場合があります。

迅速な復旧を確実にするために、Adobeでは以下を確認することをお勧めします。 [高度な計算列のタイプ](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) Adobeサポートチームが作成できる列の種類を確認するためのガイド。 このトピックでは、列を作成するために必要な情報も扱います。これをリクエストに含めます。

## 関連ドキュメント

* [計算列の作成](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [計算列のパスの作成/削除](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [テーブルの関係の理解と評価](../../data-analyst/data-warehouse-mgr/table-relationships.md)
