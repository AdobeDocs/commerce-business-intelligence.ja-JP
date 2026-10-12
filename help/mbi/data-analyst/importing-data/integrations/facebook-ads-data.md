---
title: 期待されるFacebook広告データ
description: Data Warehouseに同期する際に推奨されるテーブルの概要について説明します
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/LBpqIMm4nGx-Vu-zxw-iPLgNg1yfDsYi0yDyFHCyxvA'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%
---
# [!DNL Facebook Ads] データが必要です

[&#128279;](../integrations/facebook-ads.md)&#x200B; アカウント  [!DNL Facebook Ads] を接続した後、[Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)を使用して、分析用の関連データフィールドを簡単に追跡できます。

このトピックでは、AdobeでData Warehouseに同期する際に推奨されるテーブルの概要について説明します。 これは、かなり多くのサブテーブルがあるので、コアテーブルのみをハイライト表示します。

## コア広告キャンペーンテーブル

これらのテーブルには、コア広告キャンペーンコンポーネントに関するデータが含まれています。

### `facebook _campaigns_ (account-id)`

[`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

このテーブルは、[!DNL Facebook Ads] アカウントのキャンペーンのコア テーブルです。 列には、`campaign id`、`name`、`status (active/paused)`、`objective`が含まれます。

### `facebook _adsets_ (account-id)`

[`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

このテーブル レコードは、[!DNL Facebook Ads] アカウントの[!DNL Facebook Ads] セットのコア テーブルです。 列には、広告セットが属する広告`Campaign id/name`、予算編成、入札タイプ、スケジュール、オーディエンスのターゲティング情報が含まれます。

### `facebook _ads_ (account-id)`

[`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

このテーブルには、[!DNL Facebook Ads] アカウントのすべての広告が記録されます。 列には、属する広告セットと広告キャンペーン、広告の入札、広告のターゲティング、広告が使用する特定のクリエイティブ（画像/テキスト）への参照などの広告情報が含まれます。

### `facebook _adcreative_ (account-id)`

[`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

このテーブルには、[!DNL Facebook Ads]で使用されているクリエイターが記録されます。 クリエイティブ：クリエイティブ名、説明、画像のURLを適宜入力します

## セグメント化されたキャンペーンテーブル

次の表に、年齢、性別、国などのディメンション別にセグメント化された、各日のキャンペーン/セット/広告の組み合わせのエントリを示します。

### `facebook _ads insights_ (account-id)`

この表には、インプレッション数、クリック数、コスト、cpc、cpm、ctr、リーチ、ソーシャルリーチ、支出などの統計情報と、各日の各キャンペーン/セット/広告の組み合わせのエントリが含まれています。

### `facebook _ads insights_ (account-id)_~\_actions`

これは`facebook_ads_insights_{account_id}` テーブルのサブテーブルです。 また、さまざまなキャンペーンにもとづいて発生したアクションのコンバージョンデータも含まれます。

### `facebook _ads insights country_ (account-id)`

このテーブルには、`facebook_ads_insights_{account_id}` テーブルと同じ情報が含まれており、国別にセグメント化されています。

### `facebook ads insights age and gender (account-id)`

このテーブルには、`facebook_ads_insights_{account_id}` テーブルと同じ情報が含まれており、年齢と性別ごとにセグメント化されます。

## 関連

* [接続中 [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [統合の再認証](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations)
