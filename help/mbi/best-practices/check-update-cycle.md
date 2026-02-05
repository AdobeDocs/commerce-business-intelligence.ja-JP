---
title: 更新サイクルステータスの確認
description: 更新サイクルのステータスを確認する方法を説明します。
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
source-git-commit: d683f1362d87eee16c41ba9a8a83a9ff533b14aa
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 更新サイクルの進行状況

[!DNL Adobe Commerce Intelligence] ダッシュボードにログインする際に、最後の更新サイクルのステータスを確認する方法はいくつかあります。 それはすべて、持っている [ ユーザー権限 ](../administrator/user-management/user-management.md) のタイプによって異なります。

## 更新サイクルのステータスを確認する必要があるのはなぜですか。

ステータス更新サイクルの確認は、[!DNL Commerce Intelligence] アカウントのデータを監査する場合に便利です。 [ 期待に合わない結果 ](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md) が表示される場合（例えば、[!DNL Commerce Intelligence] の毎日の売上高が e コマースプラットフォームや [[!DNL Google] e コマースの売上高に表示されているものと一致しない場合）は ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) 最後のデータポイントを確認して、更新が完了すると問題が解決するかどうかを確認できます。

## [!UICONTROL Read-Only] および [!UICONTROL Standard] ユーザー

ユーザー `Read-only`、ダッシュボードにログインし、ページの右上のアイコンにマウスポインターを置くと、最近データが更新されたかどうかを確認できます。 これは、最後のデータポイントが取り込まれたタイミングを示します。

![ インターフェイスに表示される前回成功したデータ更新タイムスタンプ ](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] Users

ユーザー `Admin` ダッシュボードにログインすると、上記の最後のデータポイントと、アカウント統合の簡単なステータスアイコンを確認できます。

管理者ユーザーは、**[!UICONTROL Manage Data]**/**[!UICONTROL Integrations]** をクリックすると詳細を確認できます。

![ 接続の詳細と更新ステータスを表示するデータ統合の管理ページ ](../../mbi/assets/detail-manage-data-integrations.png)

このページには、現在の更新ステータスと、最後に完了した更新の時刻が表示されます。

更新が進行中の場合は、更新が完了したらメール通知をリクエストするためのリンクが表示されます。

更新が進行中でない場合は、更新を強制的に開始するためのリンクが表示されます。

>[!NOTE]
>
>ブラックアウト時間（データを更新し [!DNL Commerce Intelligence] い時間）が設定されている場合、更新を強制すると、それらのブラックアウト時間の制限を考慮しない更新サイクルが開始されます。


## API を使用して更新サイクルのステータスを確認する

**更新サイクルステータス API** を使用して、完了した最新の更新サイクルを取得できます。

**リクエスト**

```bash
curl -sS -H "X-RJM-API-Key: <EXPORT-API-KEY>" \
  https://api.rjmetrics.com/0.1/client/<CLIENT_ID>/fullupdatestatus
```

**応答（例）**

```json
{
  "clientId": 194,
  "lastCompletedUpdateJob": {
    "id": 13554,
    "type": { "id": 2, "name": "Full Update" },
    "start": "2025-12-09 03:26:25",
    "end": "2025-12-09 03:29:03",
    "status": { "id": 4, "name": "Completed Successfully" }
  },
  "lastCompletedUpdateJobWithDataSync": null,
  "timezoneAbbreviation": "EST"
}
```

パラメーター、認証、エラーおよびレート制限については、開発者ドキュメントの [ サイクルステータス API の更新 ](https://developer.adobe.com/commerce/services/reporting/update-cycle-status-api/) を参照してください。
