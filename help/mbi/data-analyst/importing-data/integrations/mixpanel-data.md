---
title: 期待される Mixpanel データ
description: Mixpanel からに読み込むことができるメインデータテーブルについて説明します [!DNL Commerce Intelligence] アカウント。
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 予測 [!DNL Mixpanel] データ

後 [を接続しました [!DNL Mixpanel] アカウント](../integrations/mixpanel.md)を使用する場合は、 [Data Warehouse管理者](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) 関連するデータフィールドを容易に追跡して分析できるようにする。

このトピックでは、インポート元となるメインのデータ テーブルについて説明します [!DNL Mixpanel] を自分の [!DNL Commerce Intelligence] アカウント。 接続後、次のテーブルがData Warehouseに作成されます [!DNL Mixpanel]. トラッキングに使用できるすべてのフィールドを表示するには、テーブル名列のリンクをクリックします。

>[!NOTE]
>
>の制限事項により [!DNL Mixpanel] API、履歴データ – への接続日から 7 日以上前のデータ [!DNL Commerce Intelligence]  – はレプリケートされません。

| **テーブル名** | **説明** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | このテーブルには、イベント、イベント日付、プラットフォームバケットなど、生のイベントデータが含まれています。 |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | このテーブルには、ファネル ID、ファネルの長さ（ユーザーがファネルを完了する必要がある日数）、ファネルの開始日と終了日など、ファネルに関するデータが含まれています。 |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | これには、セッション ID、ページおよびユーザー情報、ユーザーが最後に表示された日時など、People Analytics からのデータが含まれます。 |

{style="table-layout:auto"}

## 関連ドキュメント

* [接続中 [!DNL Mixpanel]](../integrations/mixpanel.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
