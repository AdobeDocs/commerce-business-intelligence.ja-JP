---
title: 指標アクセスの制限
description: 指標のアクセスと制限の操作方法について説明します。
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 指標ユーザーの管理

ユーザー権限レベルを設定するだけでなく、ユーザーごとに指標へのアクセスを制限することもできます。 例えば、会計部門に売上高関連の指標にアクセスできる一方で、ユーザー獲得指標にはアクセスできないようにする場合、これらの指標へのアクセスを制限できます。

このような場合、Adobeは、そのユーザーのアカウントを **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** の権限は、Data Warehouse、計算列、統合またはユーザーを作成または変更する必要はなく、指標のデータにアクセスする必要があるユーザーに付与する必要があります。 データへのアクセスを完全に制限する場合は、 **[!UICONTROL Read Only]** 権限を設定する必要があります。

権限レベルを設定した後、指標を選択できます。 **[!UICONTROL Standard]** ユーザーは、次の操作を行うことでにアクセスできます。

1. に移動します。 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. 目的のユーザーアカウントを選択します。
1. この **[!UICONTROL Metrics]** 「 」タブに、使用可能な指標のリストが表示されます。 ユーザーにアクセス権を付与する指標を選択し、ユーザーがアクセス権を付与しない指標の選択を解除します。
1. [!DNL Adobe Commerce Intelligence] は変更を自動的に保存します。 変更が成功した場合、 [!DNL Commerce Intelligence] 表示 **[!UICONTROL Saved!]** をクリックします。

>[!NOTE]
>
>次の条件を満たすすべてのユーザー **[!UICONTROL Standard]** 権限は、のすべての指標に加えて、データの書き出しを介してData Warehouse内のすべてのデータにアクセスできます。 [!DNL Google Analytics].

また、指標を編集し、 **[!UICONTROL Standard]** ユーザーの選択 **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** 」セクションに入力します。

>[!NOTE]
>
>指標を複製する場合、 [!DNL Commerce Intelligence] 元の指標に設定されたユーザー権限をコピーします。
