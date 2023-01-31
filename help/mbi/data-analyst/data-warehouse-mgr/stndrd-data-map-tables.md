---
title: マッピングテーブルを使用してデータを標準化します
description: マッピングテーブルの操作方法を説明します。
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# マッピング・テーブルを使用したデータの標準化

次の画像を表示：あなたは `Report Builder`、 `Revenue by State` レポート。 あなたはゾーンにいます。 追加に行くまで、すべてが順調に進んでいます `billing state` グループ化を使用して次の情報を確認できます。

![](../../assets/Messy_State_Segments.png)

## どうしてこんな事が起こるの？

残念ながら、標準化の欠如が、レポートを作成する際に、データの乱雑さや頭痛を引き起こす可能性があります。 この例では、顧客が請求状態情報を入力するためのドロップダウンメニューや標準化された方法がない場合があります。 これにより、様々な値が得られます。 `pa`, `PA`, `penna`, `pennsylvania`、および `Pennsylvania`  — 同じ状態で、確かに何か奇妙な結果を招くだろう `Report Builder`.

データのクリーンアップや、データベースに直接必要な列の挿入に役立つ技術リソースが存在する可能性がありますが、存在しない場合は別の解決策があります。 **マッピングテーブル**. マッピングテーブルを使用すると、データを単一の出力にマッピングすることで、メッセージのあるデータをすばやく簡単にクレンジングし、標準化できます。

>[!NOTE]
>
>統合テーブルのマッピングテーブルは、サポートチームの支援を受けずに作成できません。 詳細は、お問い合わせください。

## 作成する方法を教えてください。 {#how}

**データフォーマットリフレッシャ：**

* スプレッドシートにヘッダー行があることを確認します。
* コンマは使用しないでください。 ファイルをアップロードする際に問題が発生します。
* 標準の日付形式を使用 `(YYYY-MM-DD HH:MM:SS)` （日付）
* パーセンテージは小数で入力する必要があります。
* 先頭または末尾の 0 が適切に保持されていることを確認します。

に進む前に、 [生のテーブルデータをエクスポート](../../tutorials/export-raw-data.md). まず生データを見ると、クリーンアップする必要のあるデータの可能なすべての組み合わせを調べることができ、それにより、マッピングテーブルがすべてをカバーしていることを確認できます。

マッピングテーブルを作成するには、 [ファイルアップロード用の書式ルール](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

最初の列に、データベースに格納されている値を **各行に 1 つの値のみ**. 例： `pa` および `PA` は同じ行にはできません。各入力には、独自の行が必要です。 例については、以下を参照してください。

2 番目の列に、これらの値を入力します。 **は、**. 請求の状態の例を続けます。 `pa`, `PA`, `Pennsylvania`、および `pennsylvania` 単純に `PA`その場合、 `PA` を入力します。

![](../../assets/Mapping_table_examples.jpg)

## 必要な操作 [!DNL MBI] 使用するには？ {#use}

マッピングテーブルの作成が完了したら、次の操作を行う必要があります。 [ファイルをアップロード](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) into [!DNL MBI] および [結合された列を作成](../../data-analyst/data-warehouse-mgr/calc-column-types.md) 新しいフィールドを目的のテーブルに再配置します。 これは、ファイルが Data Warehouse に同期された後で実行できます。

この例では、 `mapping_state` テーブル (`state_input`) を `customer_address` 結合された列を使用するテーブル。 これにより、我々はクリーンでグループ化することができます `state_input` 」列を使用して、 `state` 列。

次の手順で `joined` 列に移動し、Data Warehouseマネージャでフィールドの移動先のテーブルに移動します。 この例では、次のようになります。 `customer_address` 表。

1. クリック **[!UICONTROL Create a Column]**.
1. 選択 `Joined Column` から `Definition` ドロップダウン。
1. 列に、 `state` 」列を使用します。 一緒に行く `billing state (mapped)` そのため、report builder でセグメント化する際に使用する列を指定できます。
1. テーブルを接続するために必要なパスが存在しないので、新しく作成する必要があります。 クリック **[!UICONTROL Create new path]**  内 `Select a table and column` ドロップダウン。

   テーブルの関係や、主キーと外部キーを適切に定義する方法がわからない場合は、 [アドビのチュートリアル](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) 助けを借りるために

   * の `Many` サイド、フィールドの移動先のテーブルを選択します ( 再度選択します。 `customer_address`) および `Foreign Key` 列、または `state` 列に表示されます。
   * の `One` サイド、 `mapping` テーブルと `Primary key` 列。 この場合、「 `state_input` 列 `mapping_state` 表。
   * パスがどのように表示されるかを以下に示します。

      ![](../../assets/State_Mapping_Path.png)

1. 終了したら、「 **[!UICONTROL Save]** をクリックしてパスを作成します。
1. 保存後すぐにパスが設定されない場合があります。この場合、 `Path` 」ボックスに移動し、先ほど作成したパスを選択します。
1. クリック **[!UICONTROL Save]** をクリックして列を作成します。

それだ！

## どうすればいい？ {#wrapup}

更新サイクルが完了したら、新しい結合列を使用して、データベースの messy 列ではなく、データを適切にセグメント化できます。 今すぐグループ化オプションをご覧ください。ストレスの混乱はなくなりました。

![](../../assets/Clean_State_Segments.png)

マッピングテーブルは、データウェアハウスで問題が発生する可能性のあるデータをいつでもクリーンアップする場合に便利です。 ただし、マッピングテーブルは、他のクールな使用例（例： ）にも使用できます [MBI でのGoogle Analyticsチャネルのレプリケート](../data-warehouse-mgr/rep-google-analytics-channels.md).

### 関連

* [テーブルの関係の理解と評価](../data-warehouse-mgr/table-relationships.md)
* [計算列のパスの作成/削除](../data-warehouse-mgr/create-paths-calc-columns.md)
