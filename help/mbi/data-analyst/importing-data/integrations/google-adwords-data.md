---
title: Google Adwords データが必要です
description: Data Warehouseマネージャーを使用して、関連するデータフィールドを簡単にトラッキングして分析する方法を説明します。
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# 予測 [!DNL Google Adwords] データ

後 [を接続しました [!DNL Google Adwords] アカウント](../integrations/google-adwords.md)を使用する場合は、 [Data Warehouse管理者](../../data-warehouse-mgr/tour-dwm.md) 関連するデータフィールドを容易に追跡して分析できるようにする。

ここで、Data Warehouseへのレプリケーションに使用できる 2 つのテーブルがあります。

* `campaigns[account-id]`
* `adwords[account-id]`

この `campaigns` テーブル *は、デフォルトで使用される必要があります*&#x200B;最初に、そのテーブルから関連するすべてのフィールドを同期できます。

この `adwords` テーブルに含まれていない 4 つの列 `campaigns` テーブル：

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

これらの属性を考慮した分析を実行する場合は、常に `adwords` テーブル。

>[!IMPORTANT]
>
>この表には、これらの 4 つの列がすべて含まれる行は含まれません `null`.

両方のテーブルで想定されるスキーマを以下に示します。

## [!DNL Campaigns] テーブル

この `campaigns` テーブルには、次の列が含まれます。

| **列** | **説明** |
|-----|-----|
| `\_id` | テーブルのプライマリキー |
| `accountId` | アカウント ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | その日のクリック総数 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | その日のキャンペーンの合計コスト |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] キャンペーン ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | キャンペーン名（例： [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)） |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | キャンペーンが実行された日付 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | その日のインプレッション数 |
| `profileId` | プロファイル ID |
| `profileName` | プロファイル名 |
| `\_updated\_at` | この行の最終更新日時 |

{style="table-layout:auto"}

## [!DNL AdWords] テーブル

この `adwords` テーブルには、次の列が含まれます。

| **列** | **説明** |
|-----|-----|
| `\_id` | テーブルのプライマリキー |
| `accountId` | アカウント ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | その日のクリック総数 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | その日のキャンペーンの合計コスト |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] キャンペーン ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | キャンペーン名（例： [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)） |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | キャンペーンが実行された日付 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | その日のインプレッション数 |
| `profileId` | プロファイル ID |
| `profileName` | プロファイル名 |
| `\_updated\_at` | この行の最終更新日時 |
| `keyword` | キャンペーンのキーワード |
| `adContent` | オンラインキャンペーンのテキストの 1 行目 |
| `adDestinationUrl` | この URL に対して [!DNL Adwords] 広告が参照するトラフィック |
| `adGroup` | の名前 [!DNL Adwords] 広告グループ |

{style="table-layout:auto"}

このデータを使用して、の作成を開始できます [指標](../../../data-user/reports/ess-manage-data-metrics.md) および [報告書](../../../tutorials/using-visual-report-builder.md) 支出データと [ライフタイムの売上高と結合して ROI を計算](../../analysis/roi-ad-camp.md).

## 統合テーブル

[!DNL Adobe] では、以下を作成することをお勧めします `consolidated ad spend` 複数の広告ソースすべてのデータを 1 つのテーブルに結合するテーブル。 これにより、広告分析に単一の指標セットを使用できます。

統合テーブルがなく、で美しいダッシュボードを作成する場合 `adwords` テーブルでは、レポートをレプリケートするか、重複指標を作成して、そのデータをのデータと比較する必要があります [!DNL Facebook Ads] データ。 統合テーブルを使用すると、をシームレスに組み込むことができます [!DNL Facebook Ads] 既存のデータを使用 [!DNL Adwords] レポート。 広告プラットフォームでセグメント化することもできます。

上記のフィールドを既に同期している場合は、 [contact us](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 広告費用を統合します。
