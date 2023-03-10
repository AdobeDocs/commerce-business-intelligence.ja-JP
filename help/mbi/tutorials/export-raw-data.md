---
title: 生データを書き出し
description: レコードを [!DNL MBI] Data Warehouseを参照して、ダッシュボードの機能を詳しく確認してください。
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# 生データを書き出し

生データのエクスポートを使用して、 [!DNL MBI] Data Warehouseを参照して、ダッシュボードの機能を詳しく確認してください。 また、生データの書き出しは、 [データの相違を正確に示す](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=en).

生データのエクスポートでは、関連する指標の正規化および事前集計を解除して生成された追加の列およびディメンションにアクセスできます。 例： `User's first order date` は、 [!DNL MBI]の代わりに使用できます。

このチュートリアルでは、次の内容について説明します。

* [エクスポートするデータの選択](#select)
* [エクスポート (](#download)
* [履歴エクスポートへのアクセス](#historical)

## 手順 1:エクスポートするデータの選択 {#select}

に生データを書き出すには、次の 2 つの方法があります。 [!DNL MBI]:グラフレベルまたはテーブルレベルで、

### テーブルレベルでのエクスポート `Manage Data` タブ

からテーブルをエクスポートする場合 `Manage Data` タブ、 [管理者](../administrator/user-management/user-management.md) 権限。

1. クリック **[!UICONTROL Manage Data** > **&#x200B;データを書き出し&#x200B;**> **生データの書き出し]** をクリックして開始します。
1. 表示される `Export List` 最近作成したデータの書き出し（存在する場合） クリック **[!UICONTROL Add Export]** エクスポートを作成します。
1. この `New Raw Data Export` ダイアログが表示されます。 ここでは、列とフィルターを選択または選択解除することで、エクスポートをカスタマイズできます。

   * `Table` - `Table` field データのエクスポート元のテーブルを選択します。 デフォルトでは、ナビゲート先のテーブルが表示されます。
   * `Export Name`  — このフィールドに、エクスポートの名前を入力します。 例： `Philadelphia - Daily Revenue`.
   * `Available Columns`  — このフィールドには、エクスポートに含めることができる列（ディメンション）がデータベースに表示されます。 列を追加するには、列の名前をクリックします。
   * `Selected Columns`  — このフィールドには、現在エクスポートに含まれている列（ディメンション）が一覧表示されます。 列を削除するには、その名前をクリックします。
   * `Filter`  — このセクションには、現在エクスポートに適用されているフィルターが一覧表示されます。 これらのフィルターは変更できます。また、特定のデータセットを書き出すための新しいフィルターを追加することもできます。
   * 終了したら、 **[!UICONTROL Export Data]**.

### ダッシュボードからのグラフレベルでのエクスポート

1. グラフの右上隅にある歯車アイコンをクリックします。
1. 選択 `Raw Export` ドロップダウンから `Raw Export` ダイアログ。
1. 「 `table`, `columns`、および `filters` をクリックします。 このモジュールのフィールドの詳細については、前の節を参照してください。
   >[!NOTE]
   >
   >次に表示するテーブル： `Table` フィールドは、デフォルトで、グラフの基になるテーブルです。

1. 終了したら、 **[!UICONTROL Export Data]**.

グラフレベルでプロセス全体を確認します。

![](../assets/Chart-level_export.gif)

## 手順 2:エクスポートのダウンロード {#download}

エクスポートは、 `Raw Data Export` ダイアログ。 一部の書き出しはサイズが大きい場合があるので、1,000 万行に制限され、実行に時間がかかる場合があります。

書き出しの準備ができたかどうかを確認するには、 **[!UICONTROL Raw Data Exports]** をクリックします。 クリック **[!UICONTROL Download]** 圧縮された `.csv` ファイルに書き出しを保存します。

![](../assets/Downloading_export.gif)

## 手順 3:履歴エクスポートへのアクセス {#historical}

過去のエクスポートを表示するには、 **[!UICONTROL Raw Data Export]** をクリックします。 保留中のレポートと完了したレポートには、最大 7 日間アクセスできます。

おめでとうございます。 完了しました。
