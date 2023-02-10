---
title: 予期される Mixpanel データ
description: Mixpanel から [!DNL MBI] アカウント
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# 予測 [!DNL Mixpanel] データ

後 [接続しました [!DNL Mixpanel] アカウント](../integrations/mixpanel.md)を使用する場合、 [Data Warehouse管理](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 分析に関連するデータフィールドを容易に追跡する。

この記事では、インポート元となる主なデータテーブルを確認します。 [!DNL Mixpanel] を [!DNL MBI] アカウント 次の表は、Mixpanel を接続した後で Data Warehouse で作成されます。 追跡に使用できるすべてのフィールドを表示するには、テーブル名列でリンクをクリックします。

>[!NOTE]
>
>の制限により [!DNL Mixpanel] API、履歴データ — 接続日から 7 日を経過したデータ [!DNL MBI]  — はレプリケートされません。

| **テーブル名** | **説明** |
|-----|-----|
| [`mixpanel\_export`](https://mixpanel.com/docs/api-documentation/exporting-raw-data-you-inserted-into-mixpanel#datafeed) | この表には、イベント、イベント日、プラットフォームバケットを含む生のイベントデータが含まれています。 |
| [`mixpanel\_funnels`](https://mixpanel.com/docs/api-documentation/data-export-api#funnels-default) | この表には、ファネル ID、ファネルの長さ（ユーザーがファネルを完了するまでにかかった日数）、ファネルの開始日と終了日を含む、ファネルに関するデータが含まれています。 |
| [`mixpanel\_engage`](https://mixpanel.com/docs/api-documentation/data-export-api#engage-default) | これには、セッション ID、ページおよびユーザー情報、およびユーザーが最後に閲覧された日時など、People Analytics からのデータが含まれます。 |

{style=&quot;table-layout:auto&quot;}

## 関連ドキュメント

* [接続中 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
