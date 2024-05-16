---
title: ビルド[!DNL Google ECommerce] 寸法
description: e コマースデータを注文および顧客データとリンクするディメンションの作成方法を説明します。
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# ビルド [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>が必要 [管理者権限](../../administrator/user-management/user-management.md).

これで作業は完了です [の接続[!DNL Google ECommerce] アカウント](../../data-analyst/importing-data/integrations/google-ecommerce.md)で、そのデータに対して何ができるか [!DNL Commerce Intelligence]? このトピックでは、e コマースデータを注文および顧客データにリンクするディメンションの構築について説明します。

ここで説明するディメンションを使用すると、次の内容を分析できます [マーケティングチャネルやキャンペーンに関する重要な質問に回答する](../../data-analyst/analysis/most-value-source-channel.md). 各ソースからの売上高の割合 のライフタイム値はどうですか [!DNL Facebook] 獲得した顧客を獲得した顧客と比較 [!DNL Google]?

## 前提条件と概要

このトピックでディメンションを作成するには、 [!DNL Google ECommerce] テーブル、 `orders` テーブルおよび `customers` テーブル。 これらのテーブルは、 [Data Warehouseに同期済み](../../data-analyst/data-warehouse-mgr/tour-dwm.md) ディメンションの作成前。 同期されたテーブルは、 `Synced Tables` の節 `Data Warehouse Manager`.

以下に、リフレッシャーを使用する必要がある場合の、テーブルと列の同期に関する概要を示します。

![](../../assets/Syncing_New_Columns.gif)

からの結合の作成後 `orders` テーブルから [!DNL Google eCommerce] テーブルでは、以下のリストの最初の 3 つのディメンションを作成します。 次に、これらのディメンションを使用して、で 3 つのユーザー/顧客ディメンションを作成します `customers` テーブル。 完了するには、これらの列を `orders` テーブル。

以下に、対象となるディメンションを示します。

* **注文テーブル**

* 順序`s [!DNL Google Analytics] ソース
* 順序`s [!DNL Google Analytics] 中
* 順序`s [!DNL Google Analytics]キャンペーン
* 顧客の初回注文 [!DNL Google Analytics] ソース
* 顧客の初回注文 [!DNL Google Analytics] 中
* 顧客の初回注文 [!DNL Google Analytics] campaign

* **顧客テーブル**

* 顧客の初回注文 [!DNL Google Analytics] ソース
* 顧客の初回注文 [!DNL Google Analytics] 中
* 顧客の初回注文 [!DNL Google Analytics] campaign

## ディメンションの作成

ディメンションを作成するには、 [Data Warehouse管理者](../data-warehouse-mgr/tour-dwm.md) クリックして **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### 受注テーブル、丸 1

この例では、をビルドします **順序`s [!DNL Google Analytics] ソース** ディメンション。

1. Data Warehouse内のテーブルのリストから、テーブル（この場合は `orders`）に入力します。
1. クリック **[!UICONTROL Create a Column]**.
1. 列に名前を付けます。
1. を選択 `Joined Column` から [定義ドロップダウン](../data-warehouse-mgr/calc-column-types.md). この例は、 [一対一の関係](../data-warehouse-mgr/table-relationships.md)、に一致 `eCommerce.transactionID` 列を 1 行に制限 `orders` テーブル。
1. 次に、パス、または使用するテーブルと列の接続方法を定義する必要があります。 「」をクリックします `Select a table and column` ドロップダウン。
1. 必要なパスは使用できないので、新しく作成する必要があります。 クリック **[!UICONTROL Create new Path]**.
1. 表示されるウィンドウで、 `Many` ～の側に `orders.order\_id`または、の列 `orders` 注文 ID を含むテーブル。
1. 日 `One` サイド、を見つける `Google ECommerce` テーブルで、列をに設定します `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. クリック **[!UICONTROL Save]** をクリックしてパスを作成します。
1. パスを追加したら、 **[!UICONTROL Select table and column]** もう一度ドロップダウンします。
1. を見つけます。 `ECommerce` テーブルを選択し、 `Source` 列。 これにより、注文がソース情報に結び付けられます。
1. テーブルスキーマに戻ったら、 **[!UICONTROL Save]** 再度、ディメンションを作成します。

プロセス全体を見ると、次のようになります。

![](../../assets/help_center.gif)

次に、以下を作成します **順序`s [!DNL Google Analytics] 中** および `campaign`. これらの寸法はあまり変更されないので、試してみてください。 しかし、行き詰まった場合は、次を確認できます [この記事の最後](#stuck) 違いを見るために。

### 顧客テーブル {#customers}

この例では、をビルドします **顧客の初回注文 [!DNL Google Analytics] ソース** ディメンション。

1. Data Warehouse内のテーブルのリストから、テーブル（この場合は `customers`）に入力します。
1. クリック **[!UICONTROL Create a Column]**.
1. 列に名前を付けます。
1. この例では、 `is MAX` からの定義 [定義ドロップダウン](../../data-analyst/data-warehouse-mgr/calc-column-types.md). この `is MIN` また、1 つの値のみを持つテキスト列に定義を適用した場合も機能します。 重要な部分は、適切なフィルターが設定されていることを確認することです。これについては後で行います。
1. 「」をクリックします **[!UICONTROL Select a table and column]** ドロップダウンから「」を選択します `orders` テーブルの場合は、 `Order's [!DNL Google Analytics] source` 列。
1. クリック **[!UICONTROL Save]**.
1. テーブルスキーマに戻ったら、 `Options` ドロップダウン、 `Filters`.
1. クリック **[!UICONTROL Add Filter Set]** 次に、 `Orders we count` を設定。 フィルターセットをカウントする注文に含まれる注文のみを含める必要があるので、このフィルターセットを選択することが重要です。
1. クリック **[!UICONTROL Add Filter]**. 顧客の最初の注文を検索する [!DNL Google Analytics] ソースなので、フィルターを追加する必要があります。

   _orders.Customer の注文番号= 1

   _
1. クリック **[!UICONTROL Save]** をクリックしてディメンションを作成します。

次に、以下を作成します **顧客の初回注文 [!DNL Google Analytics] 中** および `campaign`. これらの寸法はあまり変更されないので、試してみてください。 しかし、行き詰まった場合は、次を確認できます [この記事の最後](#stuck) 違いを見るために。

### ボーナス：「受注」表、ラウンド 2

必要に応じてここで停止することもできますが、このセクションでは、 **顧客の初回注文 [!DNL Google Analytics] 寸法** 「」に作成しました [最後のセクション](#customers) を、に追加します。 `orders` テーブル。 このセクションでディメンションを作成すると、 `orders` テーブル - `Revenue`, `Number of orders`, `Distinct buyers`などなど – を使用します [!DNL Google Analytics] 顧客の初回注文の属性。

この例では、を結合します `Customer's first order's [!DNL Google Analytics] source` ディメンションの対象 `orders` テーブル。

1. Data Warehouse内のテーブルのリストから、テーブル（この場合は `orders`）に入力します。
1. クリック **[!UICONTROL Create a Column]**.
1. 列に名前を付けます。
1. を選択 `Joined Column` 定義ドロップダウンから。 これにより、前の節で作成した顧客ディメンションが `orders` テーブル。
1. 「」をクリックします **[!UICONTROL Select a table and column]** ドロップダウンを選択してから、 `customers` テーブルと `Customer's first order's [!DNL Google Analytics] source` 列。
1. パスが自動的に入力されない場合は、顧客テーブルと注文テーブルを最もよく接続するパスを選択します。
1. クリック **[!UICONTROL Save]** をクリックしてディメンションを作成します。

プロセス全体を見ると、次のようになります。

![](../../assets/help_center2.gif)

最後に～に参加する `Customer's first order's` 中および `campaign` ディメンションからへ `orders` テーブル。 ディメンションを結合し、問題がある場合は、チェックアウト [記事の最後](#stuck) サポートが必要な場合。

### まとめ

ディメンションの作成が完了しました。つまり、様々なチャネルやキャンペーンのパフォーマンスを追跡する強力な分析を作成できるようになりました。 を覚えておいてください **次の更新が完了するまで、新しい列は使用できません**.

このトピックでは、より人気のあるディメンションの一部について説明していますが、上限は空です。他のオプションの探索に関するヘルプが必要な場合は、独自のディメンションを作成するか、お気軽に ping してください。 

### その他のメモ

**`Orders`テーブル #1**：の作成時 `Order's [!DNL Google Analytics]` 中および `campaign` ディメンションと違うのは、手順 12 で選択した列です。 この例では、列はでした `Source`.

**`Customers`テーブル**：の作成時 `Customer's first order's [!DNL Google Analytics]` 中および `campaign` ディメンションと、手順 5 で選択した列の差です。 この例では、列はでした `Order's [!DNL Google Analytics]` ソース。

**`Orders`テーブル #2**：に参加する場合 `Customer's first order's [!DNL Google Analytics]` 中および `campaign` 列から `orders` テーブルと手順 5 で選択した列の違いです。 この例では、列はでした `Customer's first order's [!DNL Google Analytics]` ソース。
