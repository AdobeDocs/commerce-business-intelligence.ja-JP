---
title: Google Adwords データが必要です
description: Data Warehouse Managerを使用して、分析用の関連データフィールドを簡単に追跡する方法について説明します。
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iCKOCRAELybmKfHS8F7XaKpEx9blpkRK0i0e-eEYJgU
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 436
ht-degree: 0%

---

# [!DNL Google Adwords] データが必要です

[&#x200B; アカウント  [!DNL Google Adwords] を接続した後、](../integrations/google-adwords.md)Data Warehouse Manager[を使用して、分析用の関連データフィールドを簡単に追跡できます。](../../data-warehouse-mgr/tour-dwm.md)

ここでは、Data Warehouseへのレプリケーションに使用できる2つのテーブルが表示されます。

* `campaigns[account-id]`
* `adwords[account-id]`

`campaigns` テーブル *はデフォルト*&#x200B;で使用する必要があるので、まず、そのテーブルのすべての関連フィールドを同期することから始めます。

`adwords` テーブルには、`campaigns` テーブルにない4つの列が含まれています。

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

これらの属性を考慮した分析を実行する場合は、必ず`adwords` テーブルを使用する必要があります。

>[!IMPORTANT]
>
>このテーブルでは、これら4つの列がすべて`null`である行は除外されます。

以下では、両方のテーブルの想定されるスキーマを見ていきます。

## [!DNL Campaigns] テーブル

`campaigns` テーブルには、次の列が含まれています。

| **列** | **説明** |
|-----|-----|
| `\_id` | テーブルのプライマリキー |
| `accountId` | アカウント ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | その日の合計クリック数 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | その日のキャンペーンの合計コスト |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] キャンペーン ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | キャンペーン名（例：[utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)） |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | キャンペーンの実行日 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | その日のインプレッション数 |
| `profileId` | プロファイル ID |
| `profileName` | プロファイル名 |
| `\_updated\_at` | この行の最終更新日時 |

{style="table-layout:auto"}

## [!DNL AdWords] テーブル

`adwords` テーブルには、次の列が含まれています。

| **列** | **説明** |
|-----|-----|
| `\_id` | テーブルのプライマリキー |
| `accountId` | アカウント ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adclicks) | その日の合計クリック数 |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adcost) | その日のキャンペーンの合計コスト |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_adwordscampaignid) | [!DNL Adwords] キャンペーン ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=traffic_sources&jump=ga_campaign) | キャンペーン名（例：[utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)） |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=time&jump=ga_date) | キャンペーンの実行日 |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&group=adwords&jump=ga_impressions) | その日のインプレッション数 |
| `profileId` | プロファイル ID |
| `profileName` | プロファイル名 |
| `\_updated\_at` | この行の最終更新日時 |
| `keyword` | キャンペーンのキーワード |
| `adContent` | オンラインキャンペーンのテキストの最初の行 |
| `adDestinationUrl` | [!DNL Adwords]広告がトラフィックを参照したURL |
| `adGroup` | [!DNL Adwords]広告グループの名前 |

{style="table-layout:auto"}

このデータを使用すると、支出データに基づいて[指標](../../../data-user/reports/ess-manage-data-metrics.md)と[&#x200B; レポート &#x200B;](../../../tutorials/using-visual-report-builder.md)の作成を開始し、それを生涯収益と[組み合わせてROI](../../analysis/roi-ad-camp.md)を計算できます。

## 統合テーブル

[!DNL Adobe]では、複数の広告ソースのすべてのデータを1つのテーブルにまとめるために、`consolidated ad spend` テーブルを作成することをお勧めします。 これにより、広告分析に単一の指標セットを使用できるようになります。

統合テーブルがなく、`adwords` テーブル上に美しいダッシュボードを作成する場合は、レポートをレプリケートするか、重複する指標を作成して、そのデータを[!DNL Facebook Ads] データと比較する必要があります。 統合テーブルを使用すると、[!DNL Facebook Ads] データを既存の[!DNL Adwords] レポートにシームレスに組み込むことができます。 広告プラットフォーム別にもセグメンテーションすることができます。

既に上記のフィールドを同期している場合は、[お問い合わせください](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)。広告費を統合します。
