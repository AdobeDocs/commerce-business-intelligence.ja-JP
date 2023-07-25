---
title: ファイルアップローダを使用
description: すべてのデータを 1 つのData Warehouseに配置する方法を説明します。
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---

# ファイルアップローダを使用

>[!NOTE]
>
>必要 [管理者権限](../../../administrator/user-management/user-management.md).

[!DNL Adobe Commerce Intelligence] は、ビジュアライゼーション機能だけでなく、すべてのデータを単一のData Warehouseに配置できるので、強力です。 データベースや統合の外部に存在するデータも、に取り込むことができます。 [!DNL Commerce Intelligence] Data Warehouse・マネージャのファイル・アップロード・ツールを使用して

例として広告キャンペーンを使用します。 オンラインとオフラインの両方のキャンペーンを実行している場合、オンライン統合からのデータの分析のみを行っている場合は、全体像を把握することはできません。 オフラインキャンペーンデータを使用してスプレッドシートをアップロードすると、両方のデータセットを分析し、キャンペーンのパフォーマンスをより詳細に把握できます。

## 制限事項と要件 {#require}

1. **ファイルのアップロードでサポートされる形式は、次のとおりです。 `CSV` または`comma separated values`**. Excel で作業している場合は、「名前を付けて保存」機能を使用して、ファイルをに保存できます。 `.csv` 形式
1. **`CSV`ファイルは`UTF-8 encoding`**. ほとんどの場合、これは問題ではありません。 ファイルのアップロード中にこのエラーが発生した場合は、 [このサポート記事を参照してください。](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html).
1. **100 MB を超えるファイルは使用できません**. ファイルがこれより大きい場合は、テーブルをチャンクに分割し、個々のファイルとして保存します。 最初のファイルの読み込み後に、データを追加できます。
1. **すべてのテーブルには`primary key`**. テーブル内に、 `primary key`、またはテーブル内の各行の一意の ID。 次に指定された列： `primary key` can *なし* が null の場合に限ります。 A `primary key` は、各行に数値を与える列を追加するのと同じくらい簡単にできます。また、2 つの列を連結して一意の値の列を作成することもできます ( 例： `campaign name` および `date`) をクリックします。

   列（または列）が一意であると指定されているが、重複がある場合、重複する行はインポートされません。

## アップロード用のデータの形式設定 {#formatting}

データをにアップロードする前に [!DNL Commerce Intelligence]の場合は、この節のガイドラインに従って形式が設定されていることを確認します。

### ヘッダー行 {#header}

列に正しくラベルが付けられ、読み込まれるようにするには、スプレッドシートの最初の行が、各列のデータを表すヘッダーであることを確認します。

列名は一意で、文字、数字、スペース、および次の記号のみを含める必要があります。 `$ % # /`. 列名にコンマが含まれる場合、ファイルのアップロード時に 2 つの列に分割されます。 また、Adobeでは、更新速度を最適化するために、ファイル内の列数を 85 列未満にすることをお勧めします。

### コンマ付きデータ {#commas}

ファイルは `CSV` 形式の場合、コンマを使用すると、データのアップロードで問題が発生する可能性があります。 `CSV` ファイルでは、コンマを使用して新しい値を指定します。そのため、次のような名前の列を指定します。 `Campaigns`, `August` は 2 つの列 (`Campaigns` および `August`) ではなく、すべてのデータを 1 行に移動します。 Adobeでは、可能な限りコンマを使用しないことをお勧めします。 以下を使用できます。 `Data Preview` 更新が完了した後に、データが正しく表示されているかどうかを確認します。

### 日付

日付を含むデータセットでは、 [標準の日付形式](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` または `MM/DD/YYYY`.

### 特殊文字

一部の特殊文字は使用できません。 たとえば、パイプ記号 `& # 1 2 4` は列の作成と解釈され、ファイルのアップロード時にエラーが発生します。

### 小数

通貨の値にはデータ型が必要です `Decimal Number` を選択すると、これらの列は自動的にData Warehouseの小数点以下 2 桁に丸められます。 小数点以下の桁数を丸めない場合や、精度がこれより大きい場合は、 `Non-Currency Decimal Number` データ型。

### 割合 (%)

パーセンテージは小数で入力する必要があります。 例：

| **右：** | **間違い：** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### 先頭または末尾にゼロを持つ値 {#zeroes}

ファイル内の一部の値（郵便番号や ID など）は、ゼロで始まる、または終わる場合があります。 ゼロが適切に保持され、アップロードされるように、書式設定タイプ ( 例： [数からテキストへ](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&amp;rs=en-us&amp;ad=us)) または数値書式を適用します。

用途 `US ZIP codes` 数値の書式設定を変更する方法の例を示します。 In [!DNL Excel]、次を含む列をハイライト表示します。 `ZIP codes` および [数値の形式を変更する](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&amp;rs=en-us&amp;ad=us) から `ZIP code`. また、カスタムの数値書式を選択し、 `Type` ウィンドウ： `00000`. この方法では、一部のコードが `00000` その他のものは `00000-0000`.

この `Type` は [他のデータ型の対応に合わせて別の形式に設定](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-us&amp;rs=en-us&amp;ad=us)（ID など） 次の場合、 `ID` の長さは 9 桁です ( 例： `Type` は、 `000000000` または `000-000-000`. これは変更されます `123456` から `000-123-456`.

の場合 [!DNL Google Docs] および [!DNL Apple Numbers] リソース ( [関連](#related) リストを表示します。

## データのアップロード {#uploading}

これで、スプレッドシートが正しくフォーマットされ、 [!DNL Commerce Intelligence]-friendly、Data Warehouseに追加します。

1. 利用を開始するには、に移動します。 **[!UICONTROL Data** > **File Uploads]**.

1. 次をクリック： **[!UICONTROL Upload to New Table]** タブをクリックします。

1. クリック **[!UICONTROL Choose File]** ファイルを選択します。 クリック **[!UICONTROL Open]** をクリックしてアップロードを開始します。

   アップロードが完了した後、列のリスト [!DNL Commerce Intelligence] がファイルディスプレイに表示されます。

1. 列名とデータタイプが正しいことを確認します。 特に、日付列が数値ではなく日付として読み取られていることを確認します。

   >[!NOTE]
   >
   >この `datatype` は重要なので、この手順をスキップしないでください。

1. を構成する列（複数可）を選択します。 `primary key` キーアイコンの下のチェックボックスを使用して、テーブルに追加します。

1. テーブルに名前を付けます。

1. クリック **[!UICONTROL Save Table]**.

A *成功！* テーブルを保存すると、画面の上部にメッセージが表示されます。

ビジュアルが必要な場合は、プロセス全体を確認します。

![](../../../assets/fileupload.gif)

アップロードされたテーブルは、 **ファイルのアップロード** Data Warehouse・マネージャのテーブル・リストの（「すべてのテーブル」オプションと「同期済テーブル」オプションの両方で）次のセクションに移動します。

![](../../../assets/upload-tables.png)

## 既存のテーブルへのデータの更新または追加 {#appending}

既にアップロード済みのファイルに追加する新しいデータがありますか？ 問題なし — で簡単にデータを更新および追加できます [!DNL Commerce Intelligence].

1. 利用を開始するには、に移動します。 **[!UICONTROL Manage Data** > **File Uploads]**.

1. 次をクリック： **[!UICONTROL Edit/Upload `.csv`既存のテーブルに]** タブをクリックします。

1. ドロップダウンで、更新または追加するテーブルの名前をクリックします。

1. ドロップダウンを使用して、重複行を処理するオプションを選択します。

   | オプション | 説明 |
   |---|---|
   | `Overwrite old row with new row` | 既存のテーブルと新しいファイルの両方で行の主キーが同じ場合、既存のデータが新しいデータで上書きされます。 これは、時間の経過と共に変化する値を持つ列（「ステータス」列など）に使用するメソッドです。 既存のデータは上書きされ、新しいデータで更新されます。 既存のテーブルにない主キーを持つ行は、新しい行として追加されます。 |
   | `Retain old row; discard new row` | 既存のテーブルと新しいファイルの両方で行のプライマリキーが同じ場合、新しいデータは無視されます。 |
   | `Purge all existing rows first and ignore duplicate keys within the file` | これにより、既存のデータが削除され、ファイルの新しいデータに置き換えられます。 このオプションは、既存のテーブルのデータが不要な場合にのみ使用します。 |

1. クリック **[!UICONTROL Choose File]** ファイルを選択します。

1. クリック **[!UICONTROL Open]** をクリックしてアップロードを開始します。

   アップロードが完了したら、 [!DNL Commerce Intelligence] はファイル内のデータ構造を検証します。 A *成功！* テーブルを保存すると、画面の上部にメッセージが表示されます。

## データの可用性 {#availability}

計算列と同様に、次の更新サイクルが完了すると、ファイルのアップロードからのデータを使用できるようになります。 ファイルのアップロード中に更新が進行中だった場合、データは次の更新後まで使用できません。 更新サイクルが完了したら、 `Data Preview` 」タブを使用して、ファイルが正しくアップロードされ、データが期待どおりに表示されていることを確認します。

## 折り返し {#wrapup}

このトピックでは、データのインポートの基本についてのみ説明しましたが、より高度な操作を行うこともできます。 金融、e コマース、広告費用、その他のデータのフォーマットとインポートに関するガイダンスについては、関連記事を参照してください。

また、データをに送信する方法は、ファイルのアップロードだけではありません [!DNL Commerce Intelligence]. この [データインポート API](https://developer.adobe.com/commerce/services/reporting/import-api/) 関数を使用すると、任意のデータを [!DNL Commerce Intelligence] Data Warehouse。

## 関連 {#related}

* [財務データのフォーマットとインポート](../../../best-practices/format-import-financial-data.md)
* [オフライン/その他の広告費用データのインポート](../connecting-data/import-offline-ad-data.md)
* [予測[!DNL Google ECommerce] データ](../integrations/google-ecommerce-data.md)

## サードパーティのリソース

* [数値データフォーマットガイド](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] データフォーマットガイド](https://support.google.com/docs/answer/56470?hl=en)
