---
title: 更新サイクルのステータスの確認
description: 更新サイクルのステータスを確認する方法を説明します。
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# サイクルの進行状況を更新

次にログインすると、 [!DNL Adobe Commerce Intelligence] ダッシュボードには、最後の更新サイクルのステータスを確認する方法がいくつかあります。 すべては、 [ユーザー権限](../administrator/user-management/user-management.md) あなたが持っている

## 更新サイクルのステータスを確認する必要があるのはなぜですか？

ステータスの更新サイクルを確認すると、 [!DNL Commerce Intelligence] アカウント。 もし、 [期待を満たさない結果](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)( 例： [!DNL Commerce Intelligence] が、e コマースプラットフォームまたは [[!DNL Google] e コマース売上高](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) 最後のデータポイントを調べて、更新が完了した後に問題が解決したかどうかを確認できます。

## [!UICONTROL Read-Only] および [!UICONTROL Standard] ユーザー

`Read-only` ユーザーは、ダッシュボードにログインし、ページの右上にあるアイコンにマウスポインターを置くと、データが更新された最近の状態を確認できます。 これは、最後のデータポイントが取り込まれた日時を示します。

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] ユーザー

`Admin` ユーザーは、ダッシュボードにログインし、上記の最後のデータポイントを、アカウント統合の簡単なステータスアイコンと共に表示できます。

詳しくは、管理者ユーザーは **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

このページには、現在の更新ステータスと最後に完了した更新の時刻が表示されます。

更新が進行中の場合は、更新が完了した後に電子メール通知をリクエストするリンクが表示されます。

更新が進行中でない場合は、更新を強制的に開始するためのリンクが表示されます。

>[!NOTE]
>
>ブラックアウト時間がある場合（時間が不要な場合） [!DNL Commerce Intelligence] （データを更新する場合）セットを更新するために、更新を強制すると、これらのブラックアウト時間の制限を考慮しない更新サイクルが開始されます。
