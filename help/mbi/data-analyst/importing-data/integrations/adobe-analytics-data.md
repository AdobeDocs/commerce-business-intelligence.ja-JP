---
title: 予測 [!DNL Adobe Analytics] データ
description: RDS インスタンスを接続する手順を説明します。
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# 予測 [!DNL Adobe Analytics] データ

この [!DNL Adobe Analytics] の統合 [!DNL Adobe Commerce Intelligence] はを使用します [Analytics 2.0 レポート API](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>目的のデータを確実に取得するには、最初にでレポートを作成します。 [!DNL Adobe Analytics] 必要な指標やディメンションを備えたワークスペース。 これにより、データの互換性と可用性を確認できます。

という接続されたレポートスイートごとに 1 つのテーブル `report-suite-<ID>` （ここで、 `<ID>` は、によって生成された一意の ID です。 [!DNL Commerce Intelligence]）がData Warehouse内に作成されます。

このテーブルのスキーマは、統合設定プロセスで選択した指標およびディメンションで構成されています。 さらに、によって、いくつかの列が生成されます。 [!DNL Commerce Intelligence]（識別目的）。

例えば、設定時に次の指標とディメンションを選択した場合：
- `Metric`: `Page views`
- `Dimension`: `Page`

テーブルには、次の列が含まれます。

| 列名 | 説明 |
| --- | --- |
| `_id` | この列はプライマリキーです。 |
| `_item_hash` | [!DNL Commerce Intelligence] 一意の ID。 この列の作成者 [!DNL Commerce Intelligence]. |
| `_updated_at` | この列には、データ行が最後に更新された時刻が含まれています。 作成者 [!DNL Commerce Intelligence]. |
| `start_date` | その行に含まれるデータの開始日。 `start_date` は、1 行内の同じ日の 00:00 です。 |
| `end_date` | その行に含まれるデータの終了日。 `end_date` は、常に 1 行以内の同じ日の 23:59 です。 |
| `page_views` | 選択した指標：特定された期間のページビューの合計数。 |
| `page` | 選択したディメンション：追跡されたビューを含む個々のページ名。 |

選択した指標およびディメンションのうち、で使用可能なデータを持つものを制御します [!DNL Commerce Intelligence] を使用したテーブル *同期* または *同期の解除* のオプション `Data Warehouse` ページ。 現在同期されていない列はグレーで表示されます。 列の同期を停止した場合は、後でもう一度同期を開始できます。

## 現在の制限事項

ここでは、の制限の概要を説明します [!DNL Adobe Analytics] の統合 [!DNL Commerce Intelligence].

| 制限事項 | 説明 |
| --- | --- |
| `Historical data period` | 他のサードパーティ統合と同様、 [!DNL Adobe Analytics] 統合では、限られた量の履歴データを取り込み、その後もデータを最新の状態に保つことができます。 履歴期間は 2 週間に設定されています。 |
| `Empty component combinations` | 指標とディメンションの一部の組み合わせには、データが含まれていません。 レプリケーションにこのような組み合わせを選択した場合、 [!DNL Commerce Intelligence] レプリケートされたテーブルから列を除外します。 このような組み合わせを選択しないようにするには、まず [[!DNL Adobe Analytics] ワークスペース](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) 期待するデータが得られることを確認します。 |
| `Re-authorization cadence` | の再認証 [!DNL Adobe Analytics] 統合は 2 週間ごとに必要です。 再認証するには、統合の編集ページに移動し、 **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] は、一度に 1 つのディメンションの指標データを提供します。 セットアップ時に複数のディメンションを選択した場合は、各行に [!DNL Commerce Intelligence] テーブルには、1 つの寸法値と他の寸法のヌルが含まれます。 |
