---
title: 生データの書き出し
description: ' [!DNL Commerce Intelligence] Data Warehouseからレコードを書き出して、ダッシュボードの機能を強化している内容を詳しく確認する方法について説明します。'
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Developer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
TQID: https://experienceleague.adobe.com/8n0DUwkiI1BVF5612vCd4jFWx7jwWlfOHg2K3hgWkco
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: f8a45b24-4be7-4f1b-909b-60d06b483a20id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 491
ht-degree: 0%

---

# 生データの書き出し

生データの書き出しを使用すると、Data Warehouseからレコードを書き出し、ダッシュボードの機能を強化している内容を詳しく確認できます。 また、生データの書き出しは、[ データの不一致を特定するのに役立ちます](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html)。

生データの書き出しにより、関連する指標の非正規化と事前集計によって生成された追加の列とディメンションにアクセスできます。 例えば、`User's first order date`は、[!DNL Commerce Intelligence]のユーザーごとに書き出すことができるディメンションですが、データベースでは使用できない場合があります。

このチュートリアルでは、次の項目について説明します。

* [書き出すデータの選択](#select)
* [書き出し（](#download)
* [履歴エクスポートへのアクセス](#historical)

## 手順1：書き出すデータの選択 {#select}

[!DNL Commerce Intelligence]で生データを書き出すには、次の2つの方法があります。

1. より詳細に把握できます
1. より詳細に把握できます

### [!UICONTROL Manage Data] タブのテーブル レベルでの書き出し

テーブルを[!UICONTROL Manage Data] タブからエクスポートする場合は、[管理者](../administrator/user-management/user-management.md)権限が必要です。

1. **[!UICONTROL Manage Data** > ** データの書き出し&#x200B;**> **Raw データの書き出し]**&#x200B;をクリックします。
1. 最近作成したデータ書き出しの`Export List`が存在する場合は、表示されます。 **[!UICONTROL Add Export]**&#x200B;をクリックして書き出しを作成します。
1. `New Raw Data Export` ダイアログが表示されます。 ここでは、列とフィルターを選択または選択解除して、書き出しをカスタマイズできます。

   * `Table` - `Table` フィールドは、データの書き出し元となるテーブルを選択します。 デフォルトでは、移動したテーブルが表示されます。
   * `Export Name` – このフィールドに、書き出しの名前を入力します。 例：`Philadelphia - Daily Revenue`。
   * `Available Columns` – このフィールドには、書き出しに含めることができるデータベース内の列（ディメンション）が一覧表示されます。 列を追加するには、その列の名前をクリックします。
   * `Selected Columns` – このフィールドには、書き出しに現在含まれている列（ディメンション）が一覧表示されます。 列を削除するには、その列の名前をクリックします。
   * `Filter` – このセクションには、現在エクスポートに適用されているフィルターが一覧表示されます。 これらのフィルターは変更できます。新しいフィルターを追加して、特定のデータセットを書き出すこともできます。
   * 完了したら、**[!UICONTROL Export Data]**&#x200B;をクリックします。

### ダッシュボードからのグラフレベルでの書き出し

1. 任意のグラフの右上隅にある歯車アイコンをクリックします。

1. ドロップダウンから「`Raw Export`」を選択して、`Raw Export` ダイアログを表示します。

1. `table`、`columns`および`filters`を選択して、含めるか除外するかを選択して、書き出しをカスタマイズします。 このモジュールのフィールドについて詳しくは、前の節を参照してください。

   >[!NOTE]
   >
   >`Table` フィールドに表示されるテーブルは、デフォルトでは、グラフを強化するテーブルです。

1. 完了したら、**[!UICONTROL Export Data]**&#x200B;をクリックします。

プロセス全体をチャートレベルで確認できます。

![ チャートから生データを書き出すアニメーションのデモ ](../assets/Chart-level_export.gif)

## 手順2：書き出しのダウンロード {#download}

書き出しは、`Raw Data Export` ダイアログで選択を完了した直後に処理を開始します。 一部の書き出しはサイズが大きくなる可能性があるため、1,000万行に制限され、実行に時間がかかる場合があります。

書き出しの準備ができているかどうかを確認するには、画面の右上隅にある「**[!UICONTROL Raw Data Exports]**」をクリックします。 「**[!UICONTROL Download]**」をクリックして、書き出しの圧縮された`.csv` ファイルをダウンロードします。

![書き出されたCSV ファイルのダウンロードをアニメーション化したデモ ](../assets/Downloading_export.gif)

## 手順3：履歴エクスポートへのアクセス {#historical}

過去の書き出しを表示するには、画面の右上隅にある「**[!UICONTROL Raw Data Export]**」をクリックします。 保留中および完了済みのレポートには、最大7日間アクセスできます。
