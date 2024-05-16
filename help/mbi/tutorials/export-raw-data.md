---
title: 生データの書き出し
description: からレコードを書き出す方法を学ぶ [!DNL Commerce Intelligence] ダッシュボードの機能を詳しく見るためのData Warehouseです。
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# 生データの書き出し

生データの書き出しを使用すると、ダッシュボードからレコードを書き出して、Data Warehouseの機能を詳しく確認できます。 生データの書き出しも、次の場合に役立ちます [データの不一致を特定](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

生データの書き出しでは、関連指標の正規化の解除と事前集計によって生成された追加の列とディメンションにアクセスできます。 例： `User's first order date` は、のユーザーごとに書き出すことができるディメンションです [!DNL Commerce Intelligence]データベースで使用できない場合もあります。

このチュートリアルでは、次の内容について説明します。

* [エクスポートするデータの選択](#select)
* [書き出しのダウンロード （](#download)
* [履歴エクスポートへのアクセス](#historical)

## 手順 1：エクスポートするデータの選択 {#select}

生データを書き出す方法には、次の 2 つがあります [!DNL Commerce Intelligence]:

1. グラフレベル
1. テーブルレベル

### のテーブルレベルでの書き出し [!UICONTROL Manage Data] タブ

からテーブルを書き出す場合 [!UICONTROL Manage Data] タブ、必要です [Admin](../administrator/user-management/user-management.md) 権限。

1. クリック **[!UICONTROL Manage Data** > **&#x200B;データを書き出し&#x200B;**> **生データの書き出し]**.
1. 「」が表示されます。 `Export List` 最近作成したデータ書き出しがある場合は、その中から クリック **[!UICONTROL Add Export]** エクスポートを作成します。
1. この `New Raw Data Export` ダイアログが表示されます。 ここでは、列とフィルターを選択または選択解除して、書き出しをカスタマイズできます。

   * `Table`  – が `Table` フィールドは、データの書き出し元のテーブルを選択します。 デフォルトでは、移動先のテーブルが表示されます。
   * `Export Name`  – このフィールドに、書き出しの名前を入力します。 例： `Philadelphia - Daily Revenue`.
   * `Available Columns`  – このフィールドには、エクスポートに含めることができるデータベース内の列（ディメンション）が一覧表示されます。 列を追加するには、列の名前をクリックします。
   * `Selected Columns`  – このフィールドには、現在エクスポートに含まれている列（ディメンション）が一覧表示されます。 列を削除するには、列の名前をクリックします。
   * `Filter`  – このセクションには、現在エクスポートに適用されているフィルターが一覧表示されます。 これらのフィルターは変更できます。新しいフィルターを追加して、特定のデータセットを書き出すこともできます。
   * 終了したら、 **[!UICONTROL Export Data]**.

### ダッシュボードからのチャート・レベルでのエクスポート

1. グラフの右上隅にある歯車アイコンをクリックします。

1. を選択 `Raw Export` ドロップダウンからを表示します `Raw Export` ダイアログ。

1. を選択して、書き出しをカスタマイズします。 `table`, `columns`、および `filters` を含めるか除外します。 このモジュールのフィールドについて詳しくは、前の節を参照してください。

   >[!NOTE]
   >
   >に表示されるテーブル `Table` フィールドは、デフォルトで、グラフを強化するテーブルです。

1. 終了したら、 **[!UICONTROL Export Data]**.

プロセス全体をチャートレベルで見てみましょう。

![](../assets/Chart-level_export.gif)

## 手順 2：エクスポートのダウンロード {#download}

書き出しの処理は、 `Raw Data Export` ダイアログ。 一部の書き出しはサイズが大きくなる可能性があるので、行数が 1,000 万行に制限され、実行に時間がかかる場合があります。

エクスポートの準備ができているかどうかを確認するには、 **[!UICONTROL Raw Data Exports]** 画面の右上隅に表示されます。 クリック **[!UICONTROL Download]** ZIP 形式でダウンロードするには `.csv` 書き出しのファイル。

![](../assets/Downloading_export.gif)

## 手順 3：履歴エクスポートへのアクセス {#historical}

過去の書き出しを表示するには、をクリックします **[!UICONTROL Raw Data Export]** 画面の右上隅に表示されます。 保留中および完了済みのレポートには、最大 7 日間アクセスできます。
