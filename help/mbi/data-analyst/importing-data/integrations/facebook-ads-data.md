---
title: 予想されるFacebook Ads データ
description: Data Warehouseへの同期に推奨されるテーブルの概要を説明します
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# 予期される [!DNL Facebook Ads] データ

[ アカウントに接続 ](../integrations/facebook-ads.md) した後  [!DNL Facebook Ads] [Data Warehouseマネージャー ](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) を使用すると、関連するデータフィールドを簡単に追跡して分析できます。

このトピックでは、AdobeがData Warehouseに同期する際に推奨するテーブルの概要を説明します。 かなりの数のサブテーブルがあるので、ここではコアテーブルのみが強調表示されます。

## コア広告キャンペーンテーブル

これらのテーブルには、コア広告キャンペーンコンポーネントに関するデータが含まれています。

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

このテーブルは、[!DNL Facebook Ads] アカウントのキャンペーンのコアテーブルです。 列には、`campaign id`、`name`、`status (active/paused)`、`objective` が含まれます。

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

このテーブル レコードは、[!DNL Facebook Ads] アカウント内の [!DNL Facebook Ads] セットのコア テーブルです。 列には、広告セットが属す `Campaign id/name` 広告、予算、入札タイプ、スケジュール、オーディエンスターゲット設定情報が含まれます。

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

このテーブルは、すべての広告を [!DNL Facebook Ads] アカウントに記録します。 列には、広告セットと所属する広告キャンペーン、広告入札、広告ターゲティング、広告が使用する特定のクリエイティブ（画像/テキスト）への参照などの広告情報が含まれています。

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

このテーブルは、[!DNL Facebook Ads] で使用されるクリエイティブを記録しています。 クリエイティブには、クリエイティブ名、説明、適切な場合に関連する画像 URL が含まれます。

## セグメント化されたキャンペーンテーブル

次の表には、各日のキャンペーン/セット/広告の組み合わせのエントリが、年齢、性別、国などのディメンションでセグメント化されています。

### `facebook _ads insights_ (account-id)`

この表には、インプレッション数、クリック数、コスト、cpc、cpm、cpp、ctr、リーチ、ソーシャルリーチ、支出などの統計と共に、各キャンペーン/セット/広告の組み合わせのエントリが含まれています。

### `facebook _ads insights_ (account-id)_~\_actions`

これは、`facebook_ads_insights_{account_id}` テーブルのサブテーブルです。 これには、様々なキャンペーンに基づいて実行されるアクションのコンバージョンデータが含まれます。

### `facebook _ads insights country_ (account-id)`

このテーブルには、`facebook_ads_insights_{account_id}` テーブルと同じ情報が含まれており、国別にセグメント化されています。

### `facebook ads insights age and gender (account-id)`

このテーブルには、`facebook_ads_insights_{account_id}` テーブルと同じ情報が含まれ、年齢と性別でセグメント化されています。

## 関連

* [接続  [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
