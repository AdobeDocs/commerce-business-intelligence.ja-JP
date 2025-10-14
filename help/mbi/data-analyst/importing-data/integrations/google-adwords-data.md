---
title: Google Adwords データが必要です
description: Data Warehouse Manager を使用して、関連するデータフィールドを簡単にトラッキングし、分析する方法を説明します。
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# 予期される [!DNL Google Adwords] データ

[&#x200B; アカウントに接続  [!DNL Google Adwords]  た &#x200B;](../integrations/google-adwords.md) 後、[Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) を使用して、関連するデータフィールドを簡単に追跡して分析できます。

ここには、Data Warehouseへのレプリケーションに使用できる 2 つのテーブルがあります。

* `campaigns[account-id]`
* `adwords[account-id]`

`campaigns` テーブル *デフォルトで使用する必要があります* を使用すると、そのテーブルのすべての関連フィールドを同期して開始できます。

`adwords` テーブルには、`campaigns` テーブルにない 4 つの列が含まれています。

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

これらの属性を考慮した分析を実行する場合は、常に `adwords` テーブルを使用する必要があります。

>[!IMPORTANT]
>
>この表には、これらの 4 つの列すべてが `null` まれる行が除外されます。

両方のテーブルで想定されるスキーマを以下に示します。

## [!DNL Campaigns] テーブル

`campaigns` の表には、次の列があります。

| **列** | **説明** |
|-----|-----|
| `\_id` | テーブルのプライマリキー |
| `accountId` | アカウント ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | その日のクリック総数 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | その日のキャンペーンの合計コスト |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] キャンペーン ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | キャンペーン名（例：[utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)） |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | キャンペーンが実行された日付 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | その日のインプレッション数 |
| `profileId` | プロファイル ID |
| `profileName` | プロファイル名 |
| `\_updated\_at` | この行の最終更新日時 |

{style="table-layout:auto"}

## [!DNL AdWords] テーブル

`adwords` の表には、次の列があります。

| **列** | **説明** |
|-----|-----|
| `\_id` | テーブルのプライマリキー |
| `accountId` | アカウント ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | その日のクリック総数 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | その日のキャンペーンの合計コスト |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] キャンペーン ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | キャンペーン名（例：[utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)） |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | キャンペーンが実行された日付 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | その日のインプレッション数 |
| `profileId` | プロファイル ID |
| `profileName` | プロファイル名 |
| `\_updated\_at` | この行の最終更新日時 |
| `keyword` | キャンペーンのキーワード |
| `adContent` | オンラインキャンペーンのテキストの 1 行目 |
| `adDestinationUrl` | [!DNL Adwords] 広告がトラフィックを参照した URL |
| `adGroup` | [!DNL Adwords] 広告グループの名前 |

{style="table-layout:auto"}

このデータを使用して、支出データに基づく [&#x200B; 指標 &#x200B;](../../../data-user/reports/ess-manage-data-metrics.md) および [&#x200B; レポート &#x200B;](../../../tutorials/using-visual-report-builder.md) の作成を開始し、[&#x200B; ライフタイム収益と結合して ROI を計算 &#x200B;](../../analysis/roi-ad-camp.md) できます。

## 統合テーブル

[!DNL Adobe] では、複数の広告ソースすべてからのデータを 1 つのテーブルに組み合わせる `consolidated ad spend` テーブルを作成することをお勧めします。 これにより、広告分析に単一の指標セットを使用できます。

統合テーブルがなく、`adwords` テーブルに美しいダッシュボードを作成する場合は、レポートをレプリケートするか、重複指標を作成して、そのデータを [!DNL Facebook Ads] データと比較する必要があります。 統合テーブルを使用すると、既存の [!DNL Facebook Ads] レポート [!DNL Adwords] データをシームレスに組み込むことができます。 広告プラットフォームでセグメント化することもできます。

上記のフィールドを既に同期している場合は、[&#x200B; お問い合わせ &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja) して、広告費用を統合します。
