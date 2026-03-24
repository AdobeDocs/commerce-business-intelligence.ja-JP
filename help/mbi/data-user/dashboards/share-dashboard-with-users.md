---
title: ダッシュボードを他のユーザーと共有する
description: ダッシュボードを他のユーザーと共有する方法について説明します。
exl-id: 6279b049-d1b2-4d40-b30b-ee8772e990f4
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/19tCk4327YLMnSrgQ0xHBinwiK2XHd7QU6l5rO-B6-k
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
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 269
ht-degree: 0%

---

# ダッシュボードを他のユーザーと共有する

ダッシュボードの共有は、チームの動向を常に把握し、協力的な議論を促進する優れた方法です。 一元化されたダッシュボードを作成して共有することで、チームの統制を維持しながら、必要な情報を提供できます。 [[!DNL Adobe] は、誤った変更を最小限に抑えるために、](../../best-practices/share-dashboard-best-practice.md){: target="_blank"}の権限を一部のユーザーに付与することを`Edit`に推奨します。

>[!NOTE]
>
>共有しているダッシュボードに、特定のユーザーがアクセスできない指標で構築されたレポートが含まれている場合、レポートには`Error Loading Data` メッセージが表示されます。 特定のユーザーにデータを表示するには、[管理者ユーザー](../../administrator/user-management/user-management.md)が、これらのレポートで使用されるすべての指標にアクセス権を付与する必要があります。

## ダッシュボードの共有

1. 画面上部の「**[!UICONTROL Share Dashboard]**」をクリックします。

   [!DNL Commerce Intelligence] アカウントのすべてのユーザーのリストが表示されます。

1. ダッシュボードを共有するユーザーを選択するには、名前の左側にあるチェックボックスをオンにします。

   すべてのユーザーを選択または選択解除するには、**[!UICONTROL Select]**&#x200B;をクリックし、それぞれ`Everyone`または`None`を選択します。

1. 権限は、ユーザーごとに、または一括で設定できます。

   *個別の権限を設定するには、ユーザー名の右側にある*&#x200B;をクリックします。 **[!UICONTROL None]**&#x200B;このドロップダウンから、ユーザーが持つ権限のタイプを選択します。

   *権限を一括設定するには、*&#x200B;をクリックします。**[!UICONTROL Set Permissions]** このドロップダウンから、選択したユーザーに付与する権限のタイプを選択します。

   >[!NOTE]
   >
   >この機能を使用して、以前に設定した権限を更新することもできます。 例えば、ダッシュボードの共有を停止する場合、そのユーザーの権限を`None`に設定します。

1. ダッシュボードを共有するには、**[!UICONTROL Save Changes]**&#x200B;をクリックします。 選択したユーザーには、ダッシュボードの表示を促す電子メールが送信されます。

例：

![&#x200B; ダッシュボードを共有](../../assets/Share_Dashboards.gif)
