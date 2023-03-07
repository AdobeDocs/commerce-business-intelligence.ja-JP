---
title: ビルド[!DNL Google ECommerce]寸法
description: e コマースデータを注文件数や顧客データとリンクするディメンションの作成について説明します。
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '988'
ht-degree: 0%

---

# ビルド [!DNL Google ECommerce] Dimension

>[!NOTE]
>
>必要 [管理者権限](../../administrator/user-management/user-management.md).

これで完了です [接続[!DNL Google ECommerce]アカウント](../../data-analyst/importing-data/integrations/google-ecommerce.md)で、そのデータを使用して何ができるかを [!DNL MBI]? この記事では、e コマースデータを注文件数および顧客データとリンクするディメンションの構築に関する手順を説明します。

対象となるディメンションを使用すると、分析を構築できます。 [マーケティングチャネルとキャンペーンに関する重要な質問に回答する](../../data-analyst/analysis/most-value-source-channel.md). 各ソースから得られる売上の割合 facebookが獲得した顧客のライフタイム値と、 [!DNL Google]?

## 前提条件と概要

この記事でディメンションを作成するには、次の条件を満たす必要があります： [!DNL Google ECommerce] テーブル、 `orders` テーブル、および `customers` 表。 それらのテーブルは、 [Data Warehouseに同期済み](../../data-analyst/data-warehouse-mgr/tour-dwm.md) ディメンションを作成する前に 同期されたテーブルは、 `Synced Tables` セクション `Data Warehouse Manager`.

リフレッシャーが必要な場合の、テーブルと列の同期の概要を以下に示します。

![](../../assets/Syncing_New_Columns.gif)

から結合を作成した後 `orders` テーブルから [!DNL Google eCommerce] テーブルで、以下のリストに最初の 3 つのディメンションを作成します。 次に、これらのディメンションを使用して、 `customers` 表。 完了するには、これらの列を `orders` 表。

次に、カバーされるディメンションを示します。

* **注文テーブル**

* 注文 [!DNL Google Analytics] ソース
* 注文 [!DNL Google Analytics] 中
* 注文 [!DNL Google Analytics]キャンペーン
* 顧客の最初の注文 [!DNL Google Analytics] ソース
* 顧客の最初の注文 [!DNL Google Analytics] 中
* 顧客の最初の注文 [!DNL Google Analytics] campaign

* **顧客テーブル**

* 顧客の最初の注文 [!DNL Google Analytics] ソース
* 顧客の最初の注文 [!DNL Google Analytics] 中
* 顧客の最初の注文 [!DNL Google Analytics] campaign

## ディメンションの作成

ディメンションを作成するには、 [Data Warehouse管理](../data-warehouse-mgr/tour-dwm.md) クリックして **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### 注文テーブル、ラウンド 1

この例では、 **注文 [!DNL Google Analytics] ソース** ディメンション。

1. Data Warehouseのテーブルのリストから、テーブル ( この場合は `orders`) に含まれます。
1. クリック **[!UICONTROL Create a Column]**.
1. 列に名前を付けます。
1. 選択 `Joined Column` から [定義ドロップダウン](../data-warehouse-mgr/calc-column-types.md). この例では、 [一対一の関係](../data-warehouse-mgr/table-relationships.md)、 `eCommerce.transactionID` 列を `orders` 表。
1. 次に、パスを定義するか、使用するテーブルと列の接続方法を定義する必要があります。 次をクリック： `Select a table and column` ドロップダウン。
1. 必要なパスは使用できないので、新しく作成する必要があります。 クリック **[!UICONTROL Create new Path]**.
1. 表示されるウィンドウで、 `Many` ～の横に `orders.order\_id`または `orders` 注文 ID が格納されているテーブル。
1. の `One` サイド、 `Google ECommerce` テーブルを開き、列を `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. クリック **[!UICONTROL Save]** をクリックしてパスを作成します。
1. パスを追加したら、 **[!UICONTROL Select table and column]** ドロップダウンを再度使用します。
1. を `ECommerce` テーブルを開き、 `Source` 列。 これにより、注文がソース情報に結び付けられます。
1. テーブルスキーマに戻ったら、「 **[!UICONTROL Save]** を再度クリックして、ディメンションを作成します。

プロセス全体を以下に示します。

![](../../assets/help_center.gif)

次に、作成を試みます **注文 [!DNL Google Analytics] 中** および `campaign`. これらのディメンションに対する変更は多くないので、やり直してください。 しかし、立ち往生した場合は、次を確認できます [この記事の最後](#stuck) 何が違うのかを見るために

### 顧客テーブル {#customers}

この例では、 **顧客の最初の注文 [!DNL Google Analytics] ソース** ディメンション。

1. Data Warehouseのテーブルのリストから、テーブル ( この場合は `customers`) に含まれます。
1. クリック **[!UICONTROL Create a Column]**.
1. 列に名前を付けます。
1. この例では、 `is MAX` 定義 [定義ドロップダウン](../../data-analyst/data-warehouse-mgr/calc-column-types.md). この `is MIN` 定義は、可能な値を 1 つだけ持つテキスト列に適用した場合にも機能します。 重要な点は、適切なフィルターが設定されていることを確認することです（後で設定します）。
1. 次をクリック： **[!UICONTROL Select a table and column]** ドロップダウンと選択 `orders` テーブルを開き、 `Order's [!DNL Google Analytics] source` 列。
1. クリック **[!UICONTROL Save]**.
1. テーブルスキーマに戻ったら、 `Options` ドロップダウン、 `Filters`.
1. クリック **[!UICONTROL Add Filter Set]** 次に、 `Orders we count` 設定します。 カウントするフィルターセットに含まれるオーダーのみが含まれるようにするので、このフィルターセットを選択することが重要です。
1. クリック **[!UICONTROL Add Filter]**. 顧客の最初の注文の [!DNL Google Analytics] ソースの場合は、次のようにフィルターを追加する必要があります。

   _orders.顧客の注文番号= 1

   _
1. クリック **[!UICONTROL Save]** をクリックして、ディメンションを作成します。

次に、作成を試みます **顧客の最初の注文 [!DNL Google Analytics] 中** および `campaign`. これらのディメンションに対する変更は多くないので、やり直してください。 しかし、立ち往生した場合は、次を確認できます [この記事の最後](#stuck) 何が違うのかを見るために

### ボーナス：注文テーブル、ラウンド 2

必要に応じてここで停止できますが、このセクションでは、 **顧客の最初の注文 [!DNL Google Analytics] 寸法** 次の場所で作成した [最後のセクション](#customers) に `orders` 表。 このセクションでディメンションを作成すると、 `orders` 表 — `Revenue`, `Number of orders`, `Distinct buyers`など — を使用 [!DNL Google Analytics] 顧客の最初の注文の属性。

この例は、 `Customer's first order's [!DNL Google Analytics] source` 次元を `orders` 表。

1. Data Warehouseのテーブルのリストから、テーブル ( この場合は `orders`) に含まれます。
1. クリック **[!UICONTROL Create a Column]**.
1. 列に名前を付けます。
1. 選択 `Joined Column` を選択します。 これにより、前の節で作成した顧客ディメンションが `orders` 表。
1. 次をクリック： **[!UICONTROL Select a table and column]** ドロップダウンで、 `customers` テーブルと `Customer's first order's [!DNL Google Analytics] source` 列。
1. パスが自動的に入力されない場合は、顧客と注文テーブルを結び付けるのに最適なパスを選択します。
1. クリック **[!UICONTROL Save]** をクリックして、ディメンションを作成します。

プロセス全体を以下に示します。

![](../../assets/help_center2.gif)

次の項目に参加して作業を完了 `Customer's first order's` 中 `campaign` 次元を `orders` 表。 ディメンションを結合し、問題がある場合は、チェックアウトします [記事の最後](#stuck) （ヘルプが必要な場合）

### 折り返し

ディメンションの作成が完了したので、様々なチャネルやキャンペーンのパフォーマンスを追跡する強力な分析を作成できます。 次の点に注意してください。 **新しい列は、次の更新が完了するまで使用できません**.

より人気のあるディメンションのいくつかは、この記事でカバーされていますが、空は制限です — 独自のを作成するか、他のオプションを調べるのに役立つ場合は、自由に ping を実行してください。 

### 行き詰まった！ 何が違うの？ {#stuck}

**`Orders`テーブル#1:** を作成する際に `Order's [!DNL Google Analytics]` 中 `campaign` ディメンションの場合、差は手順 12 で選択した列です。 この例では、列は `Source`.

**`Customers`テーブル：** を作成する際に `Customer's first order's [!DNL Google Analytics]` 中 `campaign` ディメンションの場合、差は手順 5 で選択した列です。 この例では、列は `Order's [!DNL Google Analytics]` ソース。

**`Orders`テーブル#2:** を結合する場合 `Customer's first order's [!DNL Google Analytics]` 中 `campaign` 列を `orders` 表の値が異なるのは、手順 5 で選択した列です。 この例では、列は `Customer's first order's [!DNL Google Analytics]` ソース。
