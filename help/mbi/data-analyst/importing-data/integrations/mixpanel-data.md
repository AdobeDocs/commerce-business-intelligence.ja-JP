---
title: 予期される Mixpanel データ
description: Mixpanel から [!DNL MBI] アカウント
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# 予測 [!DNL Mixpanel] データ

後 [接続しました [!DNL Mixpanel] アカウント](../integrations/mixpanel.md)を使用する場合、 [Data Warehouse管理](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 分析に関連するデータフィールドを容易に追跡する。

この記事では、読み込み元となる主なデータテーブルについて説明します。 [!DNL Mixpanel] を [!DNL MBI] アカウント 次の表は、Mixpanel を接続した後にData Warehouseで作成されます。 追跡に使用できるすべてのフィールドを表示するには、テーブル名列でリンクをクリックします。

>[!NOTE]
>
>の制限により [!DNL Mixpanel] API、履歴データ — 接続日から 7 日を経過したデータ [!DNL MBI]  — はレプリケートされていません。

| **テーブル名** | **説明** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | この表には、イベント、イベント日、プラットフォームバケットを含む生のイベントデータが含まれています。 |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | この表には、ファネル ID、ファネルの長さ（ユーザーがファネルを完了するまでにかかった日数）、ファネルの開始日と終了日を含む、ファネルに関するデータが含まれています。 |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | これには、セッション ID、ページおよびユーザー情報、およびユーザーが最後に閲覧された日時など、People Analytics からのデータが含まれます。 |

{style="table-layout:auto"}

## 関連ドキュメント

* [接続中 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
