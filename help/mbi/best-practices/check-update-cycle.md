---
title: 更新サイクルステータスの確認
description: 更新サイクルのステータスを確認する方法を説明します。
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# 更新サイクルの進行状況

にログインしたとき [!DNL Adobe Commerce Intelligence] ダッシュボードでは、最後の更新サイクルのステータスを確認する方法がいくつかあります。 それはすべてタイプによって異なります [ユーザー権限](../administrator/user-management/user-management.md) 君が持っていること。

## 更新サイクルのステータスを確認する必要があるのはなぜですか。

ステータス更新サイクルの確認は、のデータを監査する場合に便利です [!DNL Commerce Intelligence] アカウント。 次のようなメッセージが表示されます。 [期待を満たさない結果](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)例えば、での毎日の販売などです [!DNL Commerce Intelligence] が、e コマースプラットフォームまたはユーザーに表示されているものと一致しない [[!DNL Google] e コマースの売上高](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) 最後のデータポイントを調べて、更新が完了した後に問題が解決されたかどうかを確認できます。

## [!UICONTROL Read-Only] および [!UICONTROL Standard] ユーザー

`Read-only` ユーザーは、ダッシュボードにログインし、ページの右上のアイコンにカーソルを合わせると、最近データが更新されたかどうかを確認できます。 これは、最後のデータポイントが取り込まれたタイミングを示します。

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] ユーザー

`Admin` ユーザーは、ダッシュボードにログインすると、上記の最後のデータポイントと、アカウント統合の簡単なステータスアイコンを確認できます。

詳細については、管理者ユーザーは次をクリックできます **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

このページには、現在の更新ステータスと、最後に完了した更新の時刻が表示されます。

更新が進行中の場合は、更新が完了したらメール通知をリクエストするためのリンクが表示されます。

更新が進行中でない場合は、更新を強制的に開始するためのリンクが表示されます。

>[!NOTE]
>
>ブラックアウト時間（不要な時間）がある場合 [!DNL Commerce Intelligence] データを更新する）セットを使用する場合、更新を強制すると、それらのブラックアウト時間の制限を考慮しない更新サイクルが開始されます。
