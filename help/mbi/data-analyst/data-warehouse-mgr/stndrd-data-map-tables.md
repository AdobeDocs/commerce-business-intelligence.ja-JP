---
title: マッピングテーブルを使用したデータの標準化
description: マッピングテーブルの操作方法を説明します。
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# マッピングテーブルを使用したデータの標準化

自分が次の場所にいると仮定します： `Report Builder` の構築 `Revenue by State` レポート。 を追加しようとするまですべてがうまくいっています `billing state` レポートに対してグループ化すると、次の情報が表示されます。

![](../../assets/Messy_State_Segments.png)

## どうしてこんな事が起こったの？

残念ながら、標準化されていないと、レポートを作成する際にデータの混乱や頭痛の種になる場合があります。 この例では、顧客が請求状態情報を入力するためのドロップダウンメニューや標準化された方法がなかった可能性があります。 これにより、次のような様々な値が得られます。 `pa`, `PA`, `penna`, `pennsylvania`、および `Pennsylvania`  – すべて同じ状態に対するものです。これにより、 `Report Builder`.

データのクリーンアップや、必要な列のデータベースへの直接挿入に役立つテクニカルリソースが存在する場合があります。 そうでない場合は、別の解決策があります。 **マッピングテーブル**. マッピングテーブルを使用すると、データを単一の出力にマッピングすることで、散らかったデータをすばやく簡単にクレンジングして標準化できます。

>[!NOTE]
>
>統合テーブルのマッピング・テーブルを作成するには、Adobe・サポート・チームのサポートが必要です。

## 作成方法 {#how}

**データ形式リフレッシャ：**

* スプレッドシートにヘッダー行があることを確認します。
* コンマの使用は避けます。 これにより、ファイルをアップロードする際に問題が発生します。
* 標準の日付形式を使用 `(YYYY-MM-DD HH:MM:SS)` 日付の場合。
* 割合は小数で入力する必要があります。
* 先頭または末尾のゼロが正しく保持されていることを確認します。

取り組む前に、Adobeでは次のことをお勧めします [生のテーブルデータのエクスポート](../../tutorials/export-raw-data.md). 最初に生データを調べると、クリーンアップする必要があるデータのすべての組み合わせを調べることができ、マッピングテーブルがすべてをカバーしていることを確認できます。

マッピングテーブルを作成するには、に従って 2 列のスプレッドシートを作成する必要があります [ファイルアップロードのフォーマットルール](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

最初の列に、データベースに格納されている値を次のように入力します **各行に 1 つの値のみ**. 例： `pa` および `PA` 同じ行に入力することはできません。各入力には独自の行が必要です。 以下に例を示します。

2 列目に、これらの値を入力します **は、**. 必要に応じて、請求状態の例を続けます `pa`, `PA`, `Pennsylvania`、および `pennsylvania` 素直に～になる `PA`と入力します。 `PA` この列の各入力値。

![](../../assets/Mapping_table_examples.jpg)

## で必要な作業 [!DNL Commerce Intelligence] それを使うには？ {#use}

マッピングテーブルの作成が完了したら、次の操作を行う必要があります [ファイルをアップロードします](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) 対象 [!DNL Commerce Intelligence] および [結合された列を作成](../../data-analyst/data-warehouse-mgr/calc-column-types.md) これで、新しいフィールドが目的のテーブルに再配置されます。 これは、ファイルがData Warehouseに同期された後で行うことができます。

次の使用例は、 `mapping_state` テーブル （`state_input`）に設定します。 `customer_address` 結合列を使用するテーブル。 これにより、クリーンでグループ化できます `state_input` レポートの列（の代わり） `state` 列。

を作成するには `joined` 列で、Data Warehouseマネージャーでフィールドを再配置するテーブルに移動します。 この例では、のようになります。 `customer_address` テーブル。

1. クリック **[!UICONTROL Create a Column]**.
1. を選択 `Joined Column` から `Definition` ドロップダウン。
1. 列に、と区別できる名前を付けます `state` データベースの列。 列に名前を付ける `billing state (mapped)` そのため、report builder でセグメント化する際に使用する列を指定できます。
1. テーブルの接続に必要なパスが存在しないので、パスを作成する必要があります。 クリック **[!UICONTROL Create new path]**  が含まれる `Select a table and column` ドロップダウン。

   テーブルの関係が何か、またはプライマリキーと外部キーを適切に定義する方法が不明な場合は、 [チュートリアル](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) ヘルプを表示します。

   * 日 `Many` フィールドの移動先となるテーブルを選択します（ここでも、ここでは `customer_address`）および `Foreign Key` 列、または `state` 列（例：）。
   * 日 `One` 側で、を選択します `mapping` テーブルと `Primary key` 列。 この場合、 `state_input` からの列 `mapping_state` テーブル。
   * パスは次のようになります。

     ![](../../assets/State_Mapping_Path.png)

1. 終了したら、 **[!UICONTROL Save]** をクリックしてパスを作成します。
1. パスは保存後すぐには入力されない場合があります – この場合は、 `Path` ボックスに入力し、作成したパスを選択します。
1. クリック **[!UICONTROL Save]** をクリックして列を作成します。

## 私は今何をしますか？ {#wrapup}

更新サイクルが完了すると、データベースの乱雑な列ではなく、新しく結合された列を使用して、データを適切にセグメント化できるようになります。 グループ化オプションを今すぐ見てみましょう。ストレスの混乱をなくします。

![](../../assets/Clean_State_Segments.png)

マッピングテーブルは、Data Warehouse内の散らかっている可能性のあるデータをクリーンアップする場合にいつでも便利です。 ただし、マッピングテーブルは、その他の便利なユースケース（など）にも使用できます [のレプリケーション [!DNL Google Analytics channels] 。対象： [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md).

### 関連

* [テーブルの関係の理解と評価](../data-warehouse-mgr/table-relationships.md)
* [計算列のパスの作成/削除](../data-warehouse-mgr/create-paths-calc-columns.md)
