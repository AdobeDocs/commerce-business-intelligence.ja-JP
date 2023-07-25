---
title: ダッシュボードを他のユーザーと共有する
description: ダッシュボードを他のユーザーと共有する方法を説明します。
exl-id: 6279b049-d1b2-4d40-b30b-ee8772e990f4
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# ダッシュボードを他のユーザーと共有する

ダッシュボードの共有は、チームをループ状態に保ち、協調ディスカッションを促進する優れた方法です。 中央のダッシュボードを作成して共有することで、管理を維持しながら、必要な情報をチームに提供できます。 [[!DNL Adobe] 推奨](../../best-practices/share-dashboard-best-practice.md){:許可する target=&quot;_blank&quot;} `Edit` 選択した一部に対する権限で、誤った変更を最小限に抑えることができます。

>[!NOTE]
>
>共有しているダッシュボードに、特定のユーザーがアクセスできない指標で作成されたレポートが含まれている場合は、レポートに「 `Error Loading Data` メッセージ。 特定のユーザーにデータを表示する場合は、 [管理者ユーザー](../../administrator/user-management/user-management.md) では、これらのレポートで使用されるすべての指標に対するアクセス権を付与する必要があります。

## ダッシュボードの共有

1. クリック **[!UICONTROL Share Dashboard]** をクリックします。

   次の [!DNL Commerce Intelligence] アカウントが表示されます。

1. ダッシュボードを共有するユーザーを選択するには、名前の左側にあるボックスをオンにします。

   すべてのユーザーを選択/選択解除するには、 **[!UICONTROL Select]** を選択し、 `Everyone` または `None`、それぞれ。

1. 権限は、ユーザーごとに設定することも、一括で設定することもできます。

   *個々の権限を設定するには*&#x200B;をクリックし、 **[!UICONTROL None]** をクリックします。 このドロップダウンから、ユーザーに割り当てる権限のタイプを選択します。

   *権限を一括して設定するには*&#x200B;をクリックし、 **[!UICONTROL Set Permissions]**. このドロップダウンから、選択したユーザーが持つ必要のある権限のタイプを選択します。

   >[!NOTE]
   >
   >また、この機能を使用して、以前に設定した権限を更新することもできます。 例えば、ダッシュボードの共有を停止する場合は、権限をに設定します。 `None`.

1. ダッシュボードを共有するには、 **[!UICONTROL Save Changes]**. 選択したユーザーに、ダッシュボードを表示するよう招待する電子メールが送信されます。

例：

![ダッシュボードを共有](../../assets/Share_Dashboards.gif)
