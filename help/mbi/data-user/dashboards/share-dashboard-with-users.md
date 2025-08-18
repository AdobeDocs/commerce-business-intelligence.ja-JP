---
title: ダッシュボードを他のユーザーと共有
description: 他のユーザーとダッシュボードを共有する方法を説明します。
exl-id: 6279b049-d1b2-4d40-b30b-ee8772e990f4
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# ダッシュボードを他のユーザーと共有

ダッシュボードの共有は、チームのメンバーが常に同じ状況に置かれ、共同作業によるディスカッションを促進するのに最適な方法です。 中央のダッシュボードを作成して共有することで、コントロールを維持しながらチームに必要な情報を提供できます。 [[!DNL Adobe]  では、誤って変更することを最小限に抑えるために ](../../best-practices/share-dashboard-best-practice.md){: target="_blank"} 一部のに `Edit` の権限を付与することをお勧めします。

>[!NOTE]
>
>共有しているダッシュボードに、特定のユーザーがアクセスできない指標で作成されたレポートが含まれている場合、レポートには `Error Loading Data` のメッセージが表示されます。 特定のユーザーにデータを表示する場合は、[ 管理者ユーザー ](../../administrator/user-management/user-management.md) が、それらのレポートで使用されるすべての指標へのアクセス権を付与する必要があります。

## ダッシュボードの共有

1. 画面上部の「**[!UICONTROL Share Dashboard]**」をクリックします。

   [!DNL Commerce Intelligence] アカウントのすべてのユーザーのリストが表示されます。

1. ダッシュボードを共有するユーザーを選択するには、そのユーザーの名前の左側にあるボックスをオンにします。

   すべてのユーザーを選択/選択解除するには、「**[!UICONTROL Select]**」をクリックして「`Everyone`」または「`None`」を選択します。

1. 権限は、ユーザーごとに設定することも、まとめて設定することもできます。

   *個々の権限を設定するには*、ユーザー名の右側にある **[!UICONTROL None]** をクリックします。 このドロップダウンから、ユーザーに付与する権限のタイプを選択します。

   *権限をまとめて設定する* には、[**[!UICONTROL Set Permissions]**] をクリックします。 このドロップダウンから、選択したユーザーに付与する権限のタイプを選択します。

   >[!NOTE]
   >
   >また、この機能を使用して、以前に設定した権限を更新することもできます。 例えば、他のユーザーとのダッシュボードの共有を停止する場合、そのユーザーの権限を `None` に設定します。

1. ダッシュボードを共有するには、「**[!UICONTROL Save Changes]**」をクリックします。 選択したユーザーには、ダッシュボードを表示するよう招待するメールが届きます。

例：

![ ダッシュボードを共有 ](../../assets/Share_Dashboards.gif)
