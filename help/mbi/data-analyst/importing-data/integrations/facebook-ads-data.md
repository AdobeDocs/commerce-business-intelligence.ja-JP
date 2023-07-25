---
title: 予想されるFacebook Ads データ
description: Data Warehouseとの同期が推奨されるテーブルの概要を説明します
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# 予測 [!DNL Facebook Ads] データ

次の条件が満たされた後 [接続済み [!DNL Facebook Ads] アカウント](../integrations/facebook-ads.md)を使用する場合、 [Data Warehouse管理](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 分析に関連するデータフィールドを容易に追跡する。

このトピックでは、AdobeがData Warehouseと同期することを推奨する表の概要を簡単に説明します。 これは、かなりのサブテーブルがあるので、コアテーブルのみをハイライトします。

## コア広告キャンペーンの表

これらの表には、コア広告キャンペーンコンポーネントに関するデータが含まれています。

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

次の表は、 [!DNL Facebook Ads] アカウント 列の内容 `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

このテーブルレコードは、 [!DNL Facebook Ads] のセット [!DNL Facebook Ads] アカウント 広告を含む列 `Campaign id/name` 広告セットは、予算設定、入札タイプ、スケジュール設定およびオーディエンスのターゲティング情報に属します。

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

このテーブルでは、 [!DNL Facebook Ads] アカウント 列には、広告が属する広告セットおよび広告キャンペーン、広告入札、広告のターゲティング、広告が使用する特定のクリエイティブ（画像/テキスト）への参照を含む広告情報が含まれます。

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

このテーブルには、 [!DNL Facebook Ads]. クリエイティブには、クリエイティブ名、説明、適切な場合は関連する画像 URL が含まれます。

## セグメント化キャンペーンテーブル

次の表には、各日のキャンペーン/セット/広告の組み合わせのエントリが含まれ、年齢、性別、国などのディメンションでセグメント化されています。

### `facebook _ads insights_ (account-id)`

この表には、インプレッション数、クリック数、コスト、cpc、cpp、ctr、リーチ、ソーシャルリーチ、支出を含む統計と共に、日別のキャンペーン/セット/広告の組み合わせのエントリが含まれます。

### `facebook _ads insights_ (account-id)_~\_actions`

これは、 `facebook_ads_insights_{account_id}` 表。 これには、様々なキャンペーンに基づいて発生するアクションのコンバージョンデータが含まれます。

### `facebook _ads insights country_ (account-id)`

このテーブルには、 `facebook_ads_insights_{account_id}` 表を参照し、国別にセグメント化します。

### `facebook ads insights age and gender (account-id)`

このテーブルには、 `facebook_ads_insights_{account_id}` 表を開き、年齢別および性別別にセグメント化します。

## 関連

* [接続中 [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
