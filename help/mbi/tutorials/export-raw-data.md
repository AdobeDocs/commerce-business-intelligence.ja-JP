---
title: 生データの書き出し
description: ' [!DNL Commerce Intelligence]  ダッシュボードからレコードをエクスポートして、Data Warehouseの機能を詳しく確認する方法を説明します。'
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# 生データの書き出し

生データの書き出しを使用すると、ダッシュボードからレコードを書き出して、Data Warehouseの機能を詳しく確認できます。 また、生データの書き出しは、[ データの不一致をピンポイントで特定 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=ja) するのに役立ちます。

生データの書き出しでは、関連指標の正規化の解除と事前集計によって生成された追加の列とディメンションにアクセスできます。 例えば、`User's first order date` は [!DNL Commerce Intelligence] の各ユーザーに対して書き出すことができるディメンションですが、データベースでは使用できない場合があります。

このチュートリアルでは、次の内容について説明します。

* [エクスポートするデータの選択](#select)
* [書き出しのダウンロード （](#download)
* [履歴エクスポートへのアクセス](#historical)

## 手順 1：エクスポートするデータの選択 {#select}

生データを [!DNL Commerce Intelligence] に書き出す方法は 2 つあります。

1. グラフレベル
1. テーブルレベル

### 「[!UICONTROL Manage Data]」タブのテーブルレベルでのエクスポート

[!UICONTROL Manage Data] のタブからテーブルを書き出すには、[ 管理者 ](../administrator/user-management/user-management.md) 権限が必要です。

1. **[!UICONTROL Manage Data** > **&#x200B; データの書き出し &#x200B;**/**生データの書き出し]** をクリックします。
1. 最近作成したデータ書き出しが存在する場合は、その `Export List` が表示されます。 「**[!UICONTROL Add Export]**」をクリックして、書き出しを作成します。
1. `New Raw Data Export` ダイアログが表示されます。 ここでは、列とフィルターを選択または選択解除して、書き出しをカスタマイズできます。

   * `Table` - 「`Table`」フィールドは、データの書き出し元のテーブルを選択します。 デフォルトでは、移動先のテーブルが表示されます。
   * `Export Name` – このフィールドに、書き出しの名前を入力します。 例：`Philadelphia - Daily Revenue`。
   * `Available Columns` – このフィールドには、エクスポートに含めることができるデータベース内の列（ディメンション）が一覧表示されます。 列を追加するには、列の名前をクリックします。
   * `Selected Columns` – このフィールドには、現在エクスポートに含まれている列（ディメンション）が一覧表示されます。 列を削除するには、列の名前をクリックします。
   * `Filter` – このセクションには、書き出しに現在適用されているフィルターが一覧表示されます。 これらのフィルターは変更できます。新しいフィルターを追加して、特定のデータセットを書き出すこともできます。
   * 終了したら、「**[!UICONTROL Export Data]**」をクリックします。

### ダッシュボードからのチャート・レベルでのエクスポート

1. グラフの右上隅にある歯車アイコンをクリックします。

1. ドロップダウンから「`Raw Export`」を選択し、「`Raw Export`」ダイアログを表示します。

1. 含めるか除外する `table`、`columns`、`filters` を選択して、書き出しをカスタマイズします。 このモジュールのフィールドについて詳しくは、前の節を参照してください。

   >[!NOTE]
   >
   >`Table` フィールドに表示されるテーブルは、デフォルトでは、グラフを強化するテーブルです。

1. 終了したら、「**[!UICONTROL Export Data]**」をクリックします。

プロセス全体をチャートレベルで見てみましょう。

![](../assets/Chart-level_export.gif)

## 手順 2：エクスポートのダウンロード {#download}

書き出しは、`Raw Data Export` ダイアログでの選択が完了するとすぐに、処理を開始します。 一部の書き出しはサイズが大きくなる可能性があるので、行数が 1,000 万行に制限され、実行に時間がかかる場合があります。

書き出しの準備ができているかどうかを確認するには、画面の右上隅にある「**[!UICONTROL Raw Data Exports]**」をクリックします。 「**[!UICONTROL Download]**」をクリックして、書き出しの zip フ `.csv` ールド ファイルをダウンロードします。

![](../assets/Downloading_export.gif)

## 手順 3：履歴エクスポートへのアクセス {#historical}

過去の書き出しを表示するには、画面の右上隅にある「**[!UICONTROL Raw Data Export]**」をクリックします。 保留中および完了済みのレポートには、最大 7 日間アクセスできます。
