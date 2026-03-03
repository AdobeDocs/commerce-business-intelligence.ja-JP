---
title: 期待される Mixpanel データ
description: Mixpanel から自分のアカウントに読み込むことができるメインデータテーブル  [!DNL Commerce Intelligence]  調べます。
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 5e80ff8f8ec76996b88a22b115be696b110581be
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 予期される [!DNL Mixpanel] データ

[&#x200B; アカウントに接続  [!DNL Mixpanel]  た &#x200B;](../integrations/mixpanel.md) 後、[Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) を使用して、関連するデータフィールドを簡単に追跡して分析できます。

このトピックでは、[!DNL Mixpanel] から [!DNL Commerce Intelligence] アカウントに読み込むことができるメインデータテーブルについて説明します。 [!DNL Mixpanel] を接続すると、Data Warehouseに次のテーブルが作成されます。 トラッキングに使用できるすべてのフィールドを表示するには、テーブル名列のリンクをクリックします。

>[!NOTE]
>
>[!DNL Mixpanel] API の制限により、履歴データ（[!DNL Commerce Intelligence] への接続日から 7 日以上経過したデータ）はレプリケートされません。

| **テーブル名** | **説明** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | このテーブルには、イベント、イベント日付、プラットフォームバケットなど、生のイベントデータが含まれています。 |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | このテーブルには、funnel ID、funnelの長さ（funnelを完了する必要がある日数）、funnelの開始日と終了日など、ファネルに関するデータが含まれています。 |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | これには、セッション ID、ページおよびユーザー情報、ユーザーが最後に表示された日時など、People Analytics からのデータが含まれます。 |

{style="table-layout:auto"}

## 関連ドキュメント

* [接続  [!DNL Mixpanel]](../integrations/mixpanel.md)
* [&#x200B; 統合の再認証 &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
