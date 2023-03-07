---
title: 予測 [!DNL Adobe Analytics] データ
description: RDS インスタンスを接続する手順を説明します。
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# 予測 [!DNL Adobe Analytics] データ

この [!DNL Adobe Analytics] の統合 [!DNL MBI] は [Analytics 2.0 レポート API](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>期待するデータを確実に取得するために、まず [!DNL Adobe Analytics] ワークスペースと目的の指標およびディメンションを表示できます。 これにより、データの互換性と可用性を確認できます。

接続されたレポートスイートごとに 1 つのテーブル ( `report-suite-<ID>`で、 `<ID>` は、 [!DNL MBI]  — がData Warehouseに作成されました。

このテーブルのスキーマは、統合の設定プロセスで選択した指標とディメンションで構成されます。 さらに、 [!DNL MBI]（特定の目的で使用）

例えば、設定時に次の指標とディメンションを選択したとします。
- `Metric`: `Page views`
- `Dimension`: `Page`

テーブルには次の列が含まれます。

| 列名 | 説明 |
| --- | --- |
| `_id` | この列はプライマリキーです。 |
| `_item_hash` | [!DNL MBI] 一意の ID。 この列は次のユーザーによって作成されます： [!DNL MBI]. |
| `_updated_at` | この列には、データ行が最後に更新された日時が含まれます。 作成者 [!DNL MBI]. |
| `start_date` | 行に含まれるデータの開始日。 `start_date` は、常に同じ日の 00:00 を 1 行内に収めます。 |
| `end_date` | 行に含まれるデータの終了日。 `end_date` は常に同じ日の 23:59 を 1 行内に収めます。 |
| `page_views` | 選択した指標：特定された期間のページビューの合計数。 |
| `page` | 選択したディメンション：追跡されたビューを持つ個々のページ名。 |

選択した指標およびディメンションのどれにデータを使用できるかを制御します [!DNL MBI] テーブル *同期* または *同期解除* オプション `Data Warehouse` ページ。 現在同期されていない列はグレーで表示されます。 列の同期を停止した場合は、後で再度同期を開始できます。

## 現在の制限事項

この節では、 [!DNL Adobe Analytics] の統合 [!DNL MBI].

| 制限事項 | 説明 |
| --- | --- |
| `Historical data period` | 他のサードパーティ統合と同様に、 [!DNL Adobe Analytics] 統合では、限られた量の履歴データを取り込んだ後、引き続きデータを更新します。 履歴期間は 2 週間に設定します。 |
| `Empty component combinations` | 指標とディメンションの組み合わせには、データが含まれないものもあります。 レプリケーションでこのような組み合わせが選択されている場合、 [!DNL MBI] レプリケートされたテーブルから列を除外します。 このような組み合わせが選択されないようにするには、まず [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=en) をクリックして、期待するデータを取得したことを確認します。 |
| `Re-authorization cadence` | の再認証 [!DNL Adobe Analytics] 統合は、2 週間おきに必要です。 再認証するには、統合の編集ページに移動し、「 **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] は、一度に 1 つのディメンションの指標データを提供します。 設定時に複数のディメンションを選択した場合、 [!DNL MBI] テーブルには、他のディメンションの単一のディメンション値と null が含まれます。 |
