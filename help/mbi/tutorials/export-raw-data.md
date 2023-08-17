---
title: 生データを書き出し
description: からレコードをエクスポートする方法を学ぶ [!DNL Commerce Intelligence] Data Warehouseを参照して、ダッシュボードの機能を詳しく確認してください。
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# 生データを書き出し

生データの書き出しを使用して、Data Warehouseからレコードを書き出し、ダッシュボードの機能を詳しく確認できます。 また、生データの書き出しは、 [データの相違を正確に示す](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

生データのエクスポートでは、関連する指標の正規化および事前集計を解除して生成された追加の列およびディメンションにアクセスできます。 例： `User's first order date` は、 [!DNL Commerce Intelligence]の代わりに使用できますが、データベースでは使用できない場合があります。

このチュートリアルでは、次の内容について説明します。

* [エクスポートするデータの選択](#select)
* [エクスポートのダウンロード (](#download)
* [履歴エクスポートへのアクセス](#historical)

## 手順 1：エクスポートするデータの選択 {#select}

に生データを書き出すには、次の 2 つの方法があります。 [!DNL Commerce Intelligence]:

1. グラフレベルで
1. テーブルレベルで

### テーブルレベルでのエクスポート [!UICONTROL Manage Data] タブ

からテーブルをエクスポートする場合 [!UICONTROL Manage Data] タブ、 [管理者](../administrator/user-management/user-management.md) 権限。

1. クリック **[!UICONTROL Manage Data** > **&#x200B;データを書き出し&#x200B;**> **生データの書き出し]**.
1. 次の項目が表示されます。 `Export List` 最近作成したデータの書き出し（存在する場合）。 クリック **[!UICONTROL Add Export]** をクリックして、エクスポートを作成します。
1. The `New Raw Data Export` ダイアログが表示されます。 ここでは、列とフィルターを選択または選択解除することで、エクスポートをカスタマイズできます。

   * `Table` - `Table` field は、データの書き出し元のテーブルを選択します。 デフォルトでは、ナビゲート先のテーブルが表示されます。
   * `Export Name`  — このフィールドに、エクスポートの名前を入力します。 例： `Philadelphia - Daily Revenue`.
   * `Available Columns`  — このフィールドには、エクスポートに含めることができる列（ディメンション）がデータベースに表示されます。 列を追加するには、列の名前をクリックします。
   * `Selected Columns`  — このフィールドには、現在エクスポートに含まれている列（ディメンション）が一覧表示されます。 列を削除するには、その名前をクリックします。
   * `Filter`  — このセクションには、現在エクスポートに適用されているフィルターが一覧表示されます。 これらのフィルターは変更できます。また、新しいフィルターを追加して、特定のデータセットを書き出すこともできます。
   * 終了したら、 **[!UICONTROL Export Data]**.

### ダッシュボードからのグラフレベルでのエクスポート

1. グラフの右上隅にある歯車アイコンをクリックします。

1. 選択 `Raw Export` ドロップダウンから、 `Raw Export` ダイアログ。

1. 「 `table`, `columns`、および `filters` をクリックします。 このモジュールのフィールドの詳細については、前の節を参照してください。

   >[!NOTE]
   >
   >次に表示するテーブル： `Table` フィールドは、デフォルトで、グラフの基になるテーブルです。

1. 終了したら、 **[!UICONTROL Export Data]**.

グラフレベルでプロセス全体を確認します。

![](../assets/Chart-level_export.gif)

## 手順 2：エクスポートのダウンロード {#download}

エクスポートは、 `Raw Data Export` ダイアログ。 一部の書き出しはサイズが大きい場合があるので、1,000 万行に制限され、実行に時間がかかる場合があります。

書き出しの準備ができたかどうかを確認するには、 **[!UICONTROL Raw Data Exports]** をクリックします。 クリック **[!UICONTROL Download]** 圧縮されたファイルをダウンロードするには `.csv` ファイルに書き出しを保存します。

![](../assets/Downloading_export.gif)

## 手順 3：履歴エクスポートへのアクセス {#historical}

過去のエクスポートを表示するには、 **[!UICONTROL Raw Data Export]** をクリックします。 保留中のレポートと完了したレポートには、最大 7 日間アクセスできます。
