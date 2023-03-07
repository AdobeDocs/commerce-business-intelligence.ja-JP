---
title: 予期されるGoogle Adwords データ
description: Data Warehouseマネージャーを使用して、分析に関連するデータフィールドを簡単に追跡する方法を説明します。
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# 予期されるGoogle Adwords データ

後 [接続しました [!DNL Google Adwords] アカウント](../integrations/google-adwords.md)を使用する場合、 [Data Warehouse管理](../../data-warehouse-mgr/tour-dwm.md) 分析に関連するデータフィールドを容易に追跡する。

Data Warehouseへのレプリケーションに使用できる 2 つのテーブルがあります。 `campaigns[account-id]` および `adwords[account-id]`.

この `campaigns` 表 *は、デフォルトで使用する必要があります*&#x200B;を使用すると、そのテーブルの関連するすべてのフィールドを同期することから始めることができます。

この `adwords` テーブルに、 `campaigns` テーブル：

* `keyword`
* `adContent`
* `adDestinationUrl`
* `adGroup`

これらの属性を考慮した分析を実行したい場合は、 `adwords` 表。

>[!IMPORTANT]
>
>このテーブルでは、これらの 4 つの列がすべて含まれる行が除外されます `null`.

両方のテーブルで期待されるスキーマの概要を次に示します。

## `Campaigns` 表

この `campaigns` テーブルには、次の列が含まれます。

| **列** | **説明** |
|-----|-----|
| `\_id` | テーブルのプライマリキー |
| `accountId` | アカウント ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | その日のクリック総数 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | その日のキャンペーンの合計コスト |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] キャンペーン ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | キャンペーン名 ( 例： [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | キャンペーン実行日 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | その日のインプレッション数 |
| `profileId` | プロファイル ID |
| `profileName` | プロファイル名 |
| `\_updated\_at` | この行の最後の更新の日時 |

{style="table-layout:auto"}

## AdWords テーブル

この `adwords` テーブルには、次の列が含まれます。

| **列** | **説明** |
|-----|-----|
| `\_id` | テーブルのプライマリキー |
| `accountId` | アカウント ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | その日のクリック総数 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | その日のキャンペーンの合計コスト |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] キャンペーン ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | キャンペーン名 ( 例： [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | キャンペーン実行日 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | その日のインプレッション数 |
| `profileId` | プロファイル ID |
| `profileName` | プロファイル名 |
| `\_updated\_at` | この行の最後の更新の日時 |
| `keyword` | キャンペーンのキーワード |
| `adContent` | オンラインキャンペーンのテキストの最初の行 |
| `adDestinationUrl` | URL [!DNL Adwords] 広告参照トラフィック |
| `adGroup` | の名前 [!DNL Adwords] 広告グループ |

{style="table-layout:auto"}

このデータを使用して、 [指標 ](../../../data-user/reports/ess-manage-data-metrics.md) および [レポート](../../../tutorials/using-visual-report-builder.md) 支出データと [ROI を計算するために生涯収益と結び付ける](../../analysis/roi-ad-camp.md).

## 統合テーブル

Adobeは、 `consolidated ad spend` 表を使用して、複数の広告ソースのすべてのデータを 1 つの表に組み合わせることができます。 これにより、広告分析に単一の指標セットを使用できます。

統合されたテーブルがない場合、 `adwords` テーブルを作成する場合は、レポートを複製するか、重複する指標を作成して、そのデータを [!DNL Facebook Ads] データ。 統合テーブルを使用すると、シームレスに組み込むことができます [!DNL Facebook Ads] 既存の [!DNL Adwords] レポート。 また、広告プラットフォーム別にセグメント化することもできます。

上記のフィールドを既に同期している場合は、アドビに連絡して広告費用を統合してください。
