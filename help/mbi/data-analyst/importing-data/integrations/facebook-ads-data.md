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

# 予測 [!DNL Facebook Ads] データ

次の手順を実行した後 [さんがに接続しました [!DNL Facebook Ads] アカウント](../integrations/facebook-ads.md)を使用する場合は、 [Data Warehouse管理者](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 関連するデータフィールドを容易に追跡して分析できるようにする。

このトピックでは、AdobeがData Warehouseに同期する際に推奨するテーブルの概要を説明します。 かなりの数のサブテーブルがあるので、ここではコアテーブルのみが強調表示されます。

## コア広告キャンペーンテーブル

これらのテーブルには、コア広告キャンペーンコンポーネントに関するデータが含まれています。

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

このテーブルは、 [!DNL Facebook Ads] アカウント。 列には次が含まれます `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

このテーブルレコードは、のコアテーブルです [!DNL Facebook Ads] 内のセット [!DNL Facebook Ads] アカウント。 列には広告が含まれます `Campaign id/name` 広告セットは、予算編成、入札タイプ、スケジュールおよびオーディエンスターゲット設定情報に属しています。

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

このテーブルは、以下のすべての広告を記録します [!DNL Facebook Ads] アカウント。 列には、広告セットと所属する広告キャンペーン、広告入札、広告ターゲティング、広告が使用する特定のクリエイティブ（画像/テキスト）への参照などの広告情報が含まれています。

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

このテーブルは、で使用されるクリエイティブを記録します [!DNL Facebook Ads]. クリエイティブには、クリエイティブ名、説明、適切な場合に関連する画像 URL が含まれます。

## セグメント化されたキャンペーンテーブル

次の表には、各日のキャンペーン/セット/広告の組み合わせのエントリが、年齢、性別、国などのディメンションでセグメント化されています。

### `facebook _ads insights_ (account-id)`

この表には、インプレッション数、クリック数、コスト、cpc、cpm、cpp、ctr、リーチ、ソーシャルリーチ、支出などの統計と共に、各キャンペーン/セット/広告の組み合わせのエントリが含まれています。

### `facebook _ads insights_ (account-id)_~\_actions`

これは、のサブテーブルです `facebook_ads_insights_{account_id}` テーブル。 これには、様々なキャンペーンに基づいて実行されるアクションのコンバージョンデータが含まれます。

### `facebook _ads insights country_ (account-id)`

このテーブルには、と同じ情報が含まれます `facebook_ads_insights_{account_id}` テーブルとセグメント （国別）。

### `facebook ads insights age and gender (account-id)`

このテーブルには、と同じ情報が含まれます `facebook_ads_insights_{account_id}` テーブルとセグメントを年齢と性別で分けます。

## 関連

* [接続中 [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
