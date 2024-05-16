---
title: ダッシュボードを他のユーザーと共有
description: 他のユーザーとダッシュボードを共有する方法を説明します。
exl-id: 6279b049-d1b2-4d40-b30b-ee8772e990f4
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# ダッシュボードを他のユーザーと共有

ダッシュボードの共有は、チームのメンバーが常に同じ状況に置かれ、共同作業によるディスカッションを促進するのに最適な方法です。 中央のダッシュボードを作成して共有することで、コントロールを維持しながらチームに必要な情報を提供できます。 [[!DNL Adobe] 推奨](../../best-practices/share-dashboard-best-practice.md)付与した {: target=&quot;_blank&quot;} `Edit` 偶発的な変更を最小限に抑えるための権限を一部のみ付与します。

>[!NOTE]
>
>共有しているダッシュボードに、特定のユーザーがアクセスできない指標で作成されたレポートが含まれている場合、レポートには次の内容が表示されます `Error Loading Data` メッセージ。 特定のユーザーにデータを表示する場合は、 [管理者ユーザー](../../administrator/user-management/user-management.md) は、これらのレポートで使用されるすべての指標へのアクセス権を付与する必要があります。

## ダッシュボードの共有

1. クリック **[!UICONTROL Share Dashboard]** 画面の上部に。

   のすべてのユーザーのリスト [!DNL Commerce Intelligence] アカウントが表示されます。

1. ダッシュボードを共有するユーザーを選択するには、そのユーザーの名前の左側にあるボックスをオンにします。

   すべてのユーザーを選択/選択解除するには、 **[!UICONTROL Select]** を選択して、 `Everyone` または `None`、それぞれ。

1. 権限は、ユーザーごとに設定することも、まとめて設定することもできます。

   *個々の権限を設定するには*&#x200B;を選択し、 **[!UICONTROL None]** ：ユーザー名の右側。 このドロップダウンから、ユーザーに付与する権限のタイプを選択します。

   *権限をまとめて設定するには*&#x200B;を選択し、 **[!UICONTROL Set Permissions]**. このドロップダウンから、選択したユーザーに付与する権限のタイプを選択します。

   >[!NOTE]
   >
   >また、この機能を使用して、以前に設定した権限を更新することもできます。 例えば、他のユーザーとのダッシュボードの共有を停止する場合、そのユーザーの権限をに設定します。 `None`.

1. ダッシュボードを共有するには、 **[!UICONTROL Save Changes]**. 選択したユーザーには、ダッシュボードを表示するよう招待するメールが届きます。

例：

![ダッシュボードを共有](../../assets/Share_Dashboards.gif)
