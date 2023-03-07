---
title: 計算列のタイプ
description: 列を作成して、データを拡張し分析用に最適化する方法を説明します。
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---

# 計算列のタイプ

* [同じテーブル計算](#sametable)
* [1 対多の計算](#onetomany)
* [多対 1 の計算](#manytoone)
* [ハンディリファレンスマップ](#map)
* [高度な計算列](#advanced)

内 [Data Warehouse管理](../data-warehouse-mgr/tour-dwm.md)を使用すると、列を作成して、データを分析用に拡張および最適化できます。 [この機能](../data-warehouse-mgr/creating-calculated-columns.md) は、Data Warehouseマネージャで任意のテーブルを選択し、 **[!UICONTROL Create New Column]**.

この記事では、Data Warehouse・マネージャを使用して作成できる列のタイプについて説明します。 また、説明、その列の視覚的なウォークスルー、 [参照マップ](#map) 列の作成に必要なすべての入力値を含むデータを取得できます。 計算列を作成する方法は 3 つあります。

* [同じテーブル計算列](#sametable)
* [1 対多の計算列](#onetomany)
* [多対 1 の計算列](#manytoone)

## 同じテーブル計算列 {#sametable}

これらの列は、同じテーブルの入力列を使用して作成されます。

### 年齢 {#age}

経過時間計算列は、現在の時間と入力時間の間の秒数を返します。

次の例はを作成します。 `Seconds since customer's most recent order` 内 `customers` 表。 これは、内で購入を行っていない（チャーンと呼ばれる場合もあります）顧客のユーザーリストを作成するために使用できます `X days`.

![](../../assets/age.gif)

### 通貨コンバータ

通貨コンバータ計算列は、列のネイティブ通貨を目的の新しい通貨に変換します。

次の例はを作成します。 `base\_grand\_total In AED`、 `base\_grand\_total` それはネイティブの通貨から AED に `sales\_flat\_order` 表。 この列は、現地通貨でレポートする複数の通貨を持つ店舗で適しています。

コマースクライアントの場合、 `base\_currency\_code` フィールドは通常、ネイティブの通貨を保存します。 この `Spot Time` フィールドは、指標で使用される日付と一致する必要があります。

![](../../assets/currency_converter.png)

## 1 対多の計算列 {#onetomany}

`One-to-Many` 列 [2 つのテーブルの間のパスを使用する](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). このパスは常に、属性が存在する 1 つのテーブルと、その属性が「再配置」される多くのテーブルを示します。 パスは、 `foreign key--primary key` 関係。

### 結合された列 {#joined}

結合された列は、1 つのテーブルの属性を再配置します *から* 多くのテーブル。 1/多の典型的な例は、顧客（1 つ）と注文（多数）です。

次の例では、 `Customer's group\_id` ディメンションは、 `orders` 表。

![](../../assets/joined_column.gif)

## 多対 1 の計算列 {#manytoone}

これらの列は、1 対多の列と同じパスを使用しますが、データは反対の方向を指します。 列は、多くの側とは対照的に、パスの片側に作成されます。 この関係により、列の値は集計である必要があります。つまり、多くの側のデータポイントで実行される数学的演算です。 これには多くの使用例があり、いくつかを以下に示します。

### カウント {#count}

このタイプの計算列は、多数のテーブルの値の数を返します *onto* 一つのテーブル。

次の例では、ディメンション `Customer's lifetime number of canceled orders` が `customers` テーブル ( `orders.status`) をクリックします。

![](../../assets/many_to_one.gif){:width=&quot;699&quot; height=&quot;351&quot;}

### 合計 {#sum}

合計の計算列は、 `many` テーブルを 1 つのテーブル上に置きます。

これは、 `Customer's lifetime revenue`.

### 最小または最大 {#minmax}

最小または最大の計算列は、多辺に存在する最小または最大のレコードを返します。

これは、 `Customer's first order date`.

### 存在する {#exists}

「存在する」計算列は、多くの側にレコードが存在するかどうかを判断するバイナリテストです。 つまり、新しい列は `1` パスが各テーブルの少なくとも 1 つの行を接続している場合、 `0` 接続できない場合。

このタイプのディメンションは、例えば、顧客が特定の製品を購入したことがあるかどうかを判断する場合があります。 結合の使用 `customers` 表と `orders` テーブル、特定の製品のフィルター、ディメンション `Customer has purchased Product X?` を構築できます。

## ハンディリファレンスマップ {#map}

計算列を作成する際に、すべての入力値を覚えるのに少し問題がある場合は、作成時にこのリファレンスマップを手元に用意してください。

![](../../assets/merged_reference_map.png)

## 高度な計算列 {#advanced}

ビジネスに関する質問を分析し、回答するためのクエストで、必要な列を正確に作成できない状況が発生する場合があります。

迅速な転換を実現するため、Adobeは、 [高度な計算列のタイプ](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) ガイドを参照して、Adobeサポートチームが構築できる列の種類を確認します。 この記事では、列の作成に必要な情報についても説明します。リクエストに含めます。

## 関連ドキュメント

* [計算列の作成](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [計算列のパスの作成/削除](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [テーブルの関係の理解と評価](../../data-analyst/data-warehouse-mgr/table-relationships.md)
