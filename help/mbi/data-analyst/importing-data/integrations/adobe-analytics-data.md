---
title: ' [!DNL Adobe Analytics] 件のデータが必要です'
description: RDS インスタンスを接続する手順を説明します。
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/vA-1cABpxQNwI8xTF4Elkgv2geudkp5tnBH1l6-PZiY
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 400
ht-degree: 0%

---

# [!DNL Adobe Analytics] データが必要です

[!DNL Adobe Analytics]の[!DNL Adobe Commerce Intelligence]統合では、[Analytics 2.0 レポート API](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md)を使用しています。

>[!INFO]
>
>必要なデータを取得するには、まず[!DNL Adobe Analytics] Workspaceで、目的の指標とディメンションを使用してレポートを作成します。 これにより、データの互換性と可用性を確認できます。

接続されたレポートスイート `report-suite-<ID>`ごとに1つのテーブル （`<ID>`は[!DNL Commerce Intelligence]によって生成された一意のID）がData Warehouseに作成されます。

このテーブルのスキーマは、統合設定プロセスで選択した指標とディメンションで構成されます。 [!DNL Commerce Intelligence]によって、識別のために、いくつかの追加の列も生成されます。

例えば、設定中に次の指標とディメンションを選択した場合は、
- `Metric`: `Page views`
- `Dimension`: `Page`

テーブルには、次の列が含まれます。

| 列名 | 説明 |
| --- | --- |
| `_id` | この列はプライマリキーです。 |
| `_item_hash` | [!DNL Commerce Intelligence]の一意のID。 この列は[!DNL Commerce Intelligence]によって作成されました。 |
| `_updated_at` | この列には、データ行が最後に更新された時刻が含まれます。 [!DNL Commerce Intelligence]によって作成されます。 |
| `start_date` | 行に含まれるデータの開始日。 `start_date`は常に1行以内の同日の00:00です。 |
| `end_date` | 行に含まれるデータの終了日。 `end_date`は、1行以内で常に同じ日の23:59です。 |
| `page_views` | 選択指標：特定された期間のページビューの合計数。 |
| `page` | 選択したディメンション：追跡ビューを持つ個々のページ名。 |

[!DNL Commerce Intelligence] ページの&#x200B;*同期*&#x200B;または&#x200B;*非同期* オプションを使用して、選択した指標およびディメンションのうち、`Data Warehouse` テーブルで使用可能なデータを持つものを制御します。 現在同期されていない列はグレーで表示されます。 列の同期を停止した場合は、後でもう一度同期を開始できます。

## 現在の制限

このセクションでは、[!DNL Adobe Analytics]の[!DNL Commerce Intelligence]統合の制限事項について説明します。

| 制限 | 説明 |
| --- | --- |
| `Historical data period` | 他のサードパーティ統合と同様に、[!DNL Adobe Analytics]統合では限られた量の履歴データが引き出され、その後データを最新の状態に保つことができます。 過去の期間は2週間に設定されています。 |
| `Empty component combinations` | 指標とディメンションの一部の組み合わせには、データが含まれていません。 このような組み合わせがレプリケーション用に選択されている場合、[!DNL Commerce Intelligence]はレプリケートされたテーブルからその列を除外します。 このような組み合わせを選択しないようにするには、まず[[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html)でレポートを作成して、想定したデータが得られることを確認します。 |
| `Re-authorization cadence` | [!DNL Adobe Analytics]統合の再認証は2週間ごとに必要です。 再認証するには、統合の編集ページに移動し、**[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**&#x200B;をクリックします。 |
| `One dimension per row` | [!DNL Adobe Analytics]は、一度に1つのディメンションの指標データを提供します。 設定中に複数のディメンションを選択した場合、[!DNL Commerce Intelligence] テーブルの各行には、1つのディメンション値と各他のディメンションのnullが含まれます。 |
