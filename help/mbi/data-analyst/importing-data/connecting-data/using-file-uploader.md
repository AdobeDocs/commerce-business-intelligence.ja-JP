---
title: ファイルアップローダの使用
description: すべてのデータを 1 つのData Warehouseに配置する方法を説明します。
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 0%

---

# ファイルアップローダの使用

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

[!DNL Adobe Commerce Intelligence] は、ビジュアライゼーション機能だけでなく、すべてのデータを 1 つのData Warehouseに配置する機能を提供するので強力です。 データベースや統合の外部にあるデータでも、に取り込むことができます。 [!DNL Commerce Intelligence] Data Warehouseマネージャーのファイルのアップロードツールを使用する。

広告キャンペーンを例として使用します。 オンラインとオフラインの両方のキャンペーンを実行している場合、オンライン統合のデータを分析するだけでは全体像を把握できません。 オフラインのキャンペーンデータを含んだスプレッドシートをアップロードすると、両方のデータセットを分析してキャンペーンのパフォーマンスをより堅牢に把握できます。

## 制限事項と要件 {#require}

1. **ファイルのアップロードでサポートされている形式は次のとおりです。 `CSV` または`comma separated values`**. Excel で作業している場合は、「名前を付けて保存」関数を使用してファイルをに保存できます。 `.csv` 形式。
1. **`CSV`ファイルが使用する必要がある`UTF-8 encoding`**. ほとんどの場合、これは問題ではありません。 ファイルのアップロード中にこのエラーが発生した場合、 [このサポート記事を参照してください](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html).
1. **ファイルのサイズは 100 MB を超えることはできません**. ファイルのサイズがこのサイズより大きい場合は、テーブルをチャンクに分割して、個々のファイルとして保存します。 初期ファイルが読み込まれた後で、データを追加できます。
1. **すべてのテーブルには以下が必要です：`primary key`**. として使用できる列がテーブルに少なくとも 1 つ必要です。 `primary key`、またはテーブルの各行の一意の ID。 として指定された列 `primary key` 可能 *なし* null を指定します。 A `primary key` 各行に数値を示す列を追加するのと同じくらい単純な場合もあれば、2 つの列を連結して一意の値の列にすることができます（例：）。 `campaign name` および `date`）に設定します。

   列（または列）が一意として指定されていて、重複がある場合、重複する行はインポートされません。

## アップロード用のデータのフォーマット {#formatting}

データをにアップロードする前に [!DNL Commerce Intelligence]で、この節のガイドラインに従ってフォーマットされていることを確認します。

### ヘッダー行 {#header}

列にラベルが付けられ、正しくインポートされるようにするには、スプレッドシートの最初の行が、各列のデータを説明するヘッダーであることを確認します。

列名は一意である必要があり、文字、数字、スペースおよび次の記号のみを含める必要があります： `$ % # /`. 列名にコンマが含まれている場合、ファイルをアップロードすると 2 つの列に分割されます。 また、Adobeは更新速度を最適化するために、ファイルの列数を 85 未満にすることをお勧めします。

### コンマを使用したデータ {#commas}

ファイルはにある必要があるため `CSV` 形式、コンマの使用は、データのアップロードで問題を引き起こす可能性があります。 `CSV` ファイルでは、新しい値を示すためにコンマが使用されるので、次のような名前の列が表示されます `Campaigns`, `August` は 2 列として読み取られます（`Campaigns` および `August`）を使用します。1 行にではなく、すべてのデータを 1 行に移動します。 Adobeでは、可能な限りコンマを避けることをお勧めします。 次を使用できます `Data Preview` 更新が完了した後にデータが正しく表示されているかどうかを確認します。

### 日付

日付を含むデータセットでは、 [標準の日付形式](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` または `MM/DD/YYYY`.

### 特殊文字

使用できない特殊文字があります。 例えば、パイプ記号 `& # 1 2 4` は列の作成として解釈され、ファイルのアップロード時にエラーが発生します。

### 10 進数

通貨の値のデータタイプは `Decimal Number` を選択すると、これらの列はData Warehouseで自動的に小数第 2 位に四捨五入されます。 小数点以下の桁数を四捨五入しない場合、またはこれよりも精度が高い場合は、 `Non-Currency Decimal Number` データタイプ。

### 割合（%）

割合は小数で入力する必要があります。 例：

| **右：** | **間違った形式：** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### 先頭または末尾に 0 がある値 {#zeroes}

ファイル内の一部の値（郵便番号や ID など）は、先頭または末尾がゼロの場合があります。 ゼロが適切に保持およびアップロードされるように、書式設定タイプを変更できます（例： [数値からテキストへ](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&amp;rs=en-us&amp;ad=us)）を選択するか、数値の書式設定を適用します。

使用方法 `US ZIP codes` 数値の書式設定を変更する方法の例として示します。 対象： [!DNL Excel]含む列をハイライト表示 `ZIP codes` および [数値フォーマットの変更](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&amp;rs=en-us&amp;ad=us) 対象： `ZIP code`. カスタムの数値形式を選択したり、 `Type` ウィンドウ、を入力 `00000`. 一部のコードが次のようにフォーマットされている場合、この方法では問題が発生する可能性があることに注意してください `00000` と他名は `00000-0000`.

この `Type` 次になることができます [他のデータタイプに対応するために異なる形式を使用](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-us&amp;rs=en-us&amp;ad=us)（ID など）。 次の場合： `ID` は 9 桁の長さです。例： `Type` 次のようになります。 `000000000` または `000-000-000`. これは変わるだろう `123456` 対象： `000-123-456`.

の場合 [!DNL Google Docs] および [!DNL Apple Numbers] リソースについては、を参照してください [関連](#related) このページの下部に一覧表示します。

## データのアップロード {#uploading}

これで、スプレッドシートの形式が正しくなり、 [!DNL Commerce Intelligence]-friendly、Data Warehouseに追加します。

1. 開始するには、に移動してください **[!UICONTROL Data** > **File Uploads]**.

1. 「」をクリックします **[!UICONTROL Upload to New Table]** タブ。

1. クリック **[!UICONTROL Choose File]** ファイルを選択します。 クリック **[!UICONTROL Open]** をクリックしてアップロードを開始します。

   アップロード完了後、列のリストが表示されます [!DNL Commerce Intelligence] がファイル内に見つかりました表示されます。

1. 列名とデータタイプが正しいことを確認します。 特に、日付列が数値ではなく日付として読み取られていることを確認します。

   >[!NOTE]
   >
   >この `datatype` は重要なので、この手順をスキップしないでください。

1. を構成する列を選択します `primary key` テーブルで、キーアイコンの下にあるチェックボックスを使用します。

1. テーブルに名前を付けます。

1. クリック **[!UICONTROL Save Table]**.

A *成功しました。* テーブルを保存すると、画面の上部にメッセージが表示されます。

ビジュアルが必要な場合は、プロセス全体を見てみましょう。

![](../../../assets/fileupload.gif)

アップロードしたテーブルは、の下に表示されます **ファイルのアップロード** Data Warehouseマネージャーのテーブルリストのセクション（「すべてのテーブル」オプションと「同期テーブル」オプションの両方）:

![](../../../assets/upload-tables.png)

## 既存のテーブルへのデータの更新または追加 {#appending}

既にアップロードしているファイルに、追加する新しいデータはありますか？ 問題なし – でデータを簡単に更新および追加できます [!DNL Commerce Intelligence].

1. 開始するには、に移動してください **[!UICONTROL Manage Data** > **File Uploads]**.

1. 「」をクリックします **[!UICONTROL Edit/Upload `.csv`既存のテーブルへ]** タブ。

1. ドロップダウンで、更新または追加するテーブルの名前をクリックします。

1. ドロップダウンを使用して、重複行を処理するためのオプションを選択します。

   | オプション | 説明 |
   |---|---|
   | `Overwrite old row with new row` | これにより、既存のテーブルと新しいファイルの両方のローに同じプライマリ・キーがある場合、既存のデータが新しいデータで上書きされます。 これは、時間の経過と共に値が変化する列（ステータス列など）に使用する方法です。 既存のデータが上書きされ、新しいデータで更新されます。 既存のテーブルにプライマリキーがない行が新しい行として追加されます。 |
   | `Retain old row; discard new row` | これにより、既存のテーブルと新しいファイルの両方で、行の主キーが同じ場合、新しいデータが無視されます。 |
   | `Purge all existing rows first and ignore duplicate keys within the file` | これにより、既存のデータがすべて削除され、ファイル内の新しいデータに置き換えられます。 このオプションは、既存のテーブルにデータが必要ない場合にのみ使用します。 |

1. クリック **[!UICONTROL Choose File]** ファイルを選択します。

1. クリック **[!UICONTROL Open]** をクリックしてアップロードを開始します。

   アップロード完了後、 [!DNL Commerce Intelligence] は、ファイルのデータ構造を検証します。 A *成功しました。* テーブルを保存すると、画面の上部にメッセージが表示されます。

## データの可用性 {#availability}

計算列と同様に、ファイルのアップロードからのデータは、次の更新サイクルが完了した後で利用できます。 ファイルのアップロード中に更新が進行中の場合、次の更新が完了するまでデータを利用することはできません。 更新サイクルが完了したら、に移動できます `Data Preview` Data Warehouseーで「」タブをクリックし、ファイルが正しくアップロードされ、データが期待どおりに表示されていることを確認します。

## まとめ {#wrapup}

このトピックでは、データの読み込みの使用に関する基本的な事項のみを説明しましたが、より高度な操作が必要な場合があります。 財務、e コマース、広告費用、その他のタイプのデータのフォーマット設定と読み込みに関するガイダンスについては、関連記事を参照してください。

また、ファイルのアップロードは、データをに送信する唯一の方法ではありません [!DNL Commerce Intelligence]. この [データ読み込み API](https://developer.adobe.com/commerce/services/reporting/import-api/) 関数を使用すると、任意のデータを [!DNL Commerce Intelligence] Data Warehouse。

## 関連 {#related}

* [財務データのフォーマットとインポート](../../../best-practices/format-import-financial-data.md)
* [オフライン/その他の広告費用データのインポート](../connecting-data/import-offline-ad-data.md)
* [予測[!DNL Google ECommerce] データ](../integrations/google-ecommerce-data.md)

## サードパーティのリソース

* [数値データ形式ガイド](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] データ形式ガイド](https://support.google.com/docs/answer/56470?hl=en)
