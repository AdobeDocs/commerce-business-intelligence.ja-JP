---
title: 予想されるMixpanel データ
description: Mixpanelから [!DNL Commerce Intelligence]  アカウントに読み込むことができる主なデータテーブルを確認します。
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iM6GzisImrjed7uCZf6lf6HIze9MwWdhq2gEP-IrIXA
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 187
ht-degree: 0%

---

# [!DNL Mixpanel] データが必要です

[&#x200B; アカウント  [!DNL Mixpanel] を接続した後、](../integrations/mixpanel.md)Data Warehouse Manager[を使用して、分析用の関連データフィールドを簡単に追跡できます。](../../../data-analyst/data-warehouse-mgr/tour-dwm.md)

このトピックでは、[!DNL Mixpanel]から[!DNL Commerce Intelligence] アカウントにインポートできる主なデータ テーブルについて説明します。 [!DNL Mixpanel]を接続すると、次のテーブルがData Warehouseに作成されます。 トラッキングに使用できるすべてのフィールドを表示するには、テーブル名の列のリンクをクリックします。

>[!NOTE]
>
>[!DNL Mixpanel] APIの制限により、過去データ （接続日から[!DNL Commerce Intelligence]までの7日以上のデータ）はレプリケートされません。

| **テーブル名** | **説明** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | このテーブルには、イベント、イベント日、プラットフォームバケットなどの生のイベントデータが含まれています。 |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | このテーブルには、funnel ID、funnelの長さ（funnelに入力する必要がある日数）、funnelの開始日と終了日など、ファネルに関するデータが含まれます。 |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | これには、セッション ID、ページおよびユーザー情報、ユーザーが最後に表示された日時など、People Analyticsのデータが含まれます。 |

{style="table-layout:auto"}

## 関連ドキュメント

* [接続中 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [統合を再認証しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
