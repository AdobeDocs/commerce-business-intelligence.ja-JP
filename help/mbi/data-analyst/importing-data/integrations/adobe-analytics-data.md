---
title: 期待  [!DNL Adobe Analytics]  データ
description: RDS インスタンスを接続する手順を説明します。
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# 予期される [!DNL Adobe Analytics] データ

[!DNL Adobe Analytics] の [!DNL Adobe Commerce Intelligence] 統合では、[Analytics 2.0 レポート API](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md) を使用します。

>[!INFO]
>
>目的のデータを確実に取得するには、まず [!DNL Adobe Analytics] Workspaceで、目的の指標とディメンションを含むレポートを作成します。 これにより、データの互換性と可用性を確認できます。

`report-suite-<ID>` と呼ばれる接続されたレポートスイートごとに 1 つのテーブル（`<ID>` は、[!DNL Commerce Intelligence] によって生成された一意の ID）がData Warehouseに作成されます。

このテーブルのスキーマは、統合設定プロセスで選択した指標およびディメンションで構成されています。 識別を目的として、[!DNL Commerce Intelligence] でもいくつかの追加の列が生成されます。

例えば、設定時に次の指標とディメンションを選択した場合：
- `Metric`: `Page views`
- `Dimension`: `Page`

テーブルには、次の列が含まれます。

| 列名 | 説明 |
| --- | --- |
| `_id` | この列はプライマリキーです。 |
| `_item_hash` | 一意 [!DNL Commerce Intelligence]ID。 この列は [!DNL Commerce Intelligence] が作成しました。 |
| `_updated_at` | この列には、データ行が最後に更新された時刻が含まれています。 [!DNL Commerce Intelligence] によって作成されます。 |
| `start_date` | その行に含まれるデータの開始日。 `start_date` は常に 1 行内の同じ日の 00:00 です。 |
| `end_date` | その行に含まれるデータの終了日。 `end_date` は常に 1 行以内の同じ日の 23:59 です。 |
| `page_views` | 選択した指標：特定された期間のページビューの合計数。 |
| `page` | 選択したディメンション：追跡されたビューを含む個々のページ名。 |

[!DNL Commerce Intelligence] ページの *同期* または *同期解除* オプションを使用して、選択した指標およびディメンションのうち、`Data Warehouse` テーブルで使用できるデータを持つものを制御します。 現在同期されていない列はグレーで表示されます。 列の同期を停止した場合は、後でもう一度同期を開始できます。

## 現在の制限事項

この節では、[!DNL Adobe Analytics] の [!DNL Commerce Intelligence] 統合の制限について概説します。

| 制限事項 | 説明 |
| --- | --- |
| `Historical data period` | 他のサードパーティ統合と同様に、[!DNL Adobe Analytics] 統合では、限られた量の履歴データを取り込み、その後もデータを最新の状態に保ちます。 履歴期間は 2 週間に設定されています。 |
| `Empty component combinations` | 指標とディメンションの一部の組み合わせには、データが含まれていません。 このような組み合わせをレプリケーションに選択 [!DNL Commerce Intelligence] ると、レプリケートされたテーブルから列が除外されます。 このような組み合わせを選ばないようにするには、まず [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html?lang=ja) でレポートを作成して、目的のデータが得られることを確認します。 |
| `Re-authorization cadence` | [!DNL Adobe Analytics] 統合の再認証は、2 週間ごとに必要です。 再認証するには、統合の編集ページに移動し、「**[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**」をクリックします。 |
| `One dimension per row` | [!DNL Adobe Analytics] は、一度に 1 つのディメンションの指標データを提供します。 設定時に複数の寸法を選択した場合、[!DNL Commerce Intelligence] テーブルの各行には、1 つの寸法値と他の寸法の NULL が含まれます。 |
