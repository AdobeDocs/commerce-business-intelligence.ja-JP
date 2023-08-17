---
title: 予期される Mixpanel データ
description: Mixpanel から [!DNL Commerce Intelligence] アカウント。
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# 期待値 [!DNL Mixpanel] データ

後 [接続しました [!DNL Mixpanel] アカウント](../integrations/mixpanel.md)を使用する場合、 [Data Warehouse管理](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 分析に関連するデータフィールドを容易に追跡する。

このトピックでは、からインポートできる主なデータテーブルについて説明します。 [!DNL Mixpanel] を [!DNL Commerce Intelligence] アカウント。 次の表は、接続後にData Warehouseに作成されます [!DNL Mixpanel]. 追跡に使用できるすべてのフィールドを表示するには、テーブル名列でリンクをクリックします。

>[!NOTE]
>
>の制限により [!DNL Mixpanel] API、履歴データ — 接続日から 7 日を経過したデータ [!DNL Commerce Intelligence]  — はレプリケートされていません。

| **テーブル名** | **説明** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | この表には、イベント、イベント日、プラットフォームバケットを含む生のイベントデータが含まれています。 |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | この表には、ファネル ID、ファネルの長さ（ユーザーがファネルを完了するまでにかかった日数）、ファネルの開始日と終了日を含む、ファネルに関するデータが含まれています。 |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | これには、セッション ID、ページおよびユーザー情報、およびユーザーが最後に閲覧された日時など、People Analytics からのデータが含まれます。 |

{style="table-layout:auto"}

## 関連ドキュメント

* [接続中 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
