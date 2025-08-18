---
title: 指標へのアクセスの制限
description: 指標へのアクセスと制限の操作方法を説明します。
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# 指標ユーザーの管理

ユーザー権限レベルの設定に加えて、指標へのアクセスをユーザーごとに制限することもできます。 例えば、会計部門から売上高に関連する指標へのアクセスを許可しても、ユーザー獲得指標へのアクセスを許可しない場合は、それらの指標へのアクセスを制限できます。

このような場合、Adobeでは、そのユーザーのアカウントを **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)** に設定することをお勧めします。 指標、計算列、統合またはユーザーを作成または変更する必要はないが、Data Warehouseのデータにアクセスする必要があるユーザーには、**[!UICONTROL Standard]** の権限を付与する必要があります。 データへのアクセスを完全に制限する場合は、**[!UICONTROL Read Only]** の権限を使用します。

権限レベルを設定した後、**[!UICONTROL Standard]** ユーザーがアクセスできる指標を選択するには、次の操作を行います。

1. **[!UICONTROL Account Settings]**/**[!UICONTROL Manage Users]** に移動します。
1. 目的のユーザーアカウントを選択します。
1. 「**[!UICONTROL Metrics]**」タブには、使用可能な指標のリストが表示されます。 ユーザーがアクセスできる指標を確認し、ユーザーがアクセス権を持たない指標の選択を解除します。
1. 変更 [!DNL Adobe Commerce Intelligence] 自動的に保存されます。 変更に成功すると、ページ [!DNL Commerce Intelligence] 上部に **[!UICONTROL Saved!]** が表示されます。

>[!NOTE]
>
>**[!UICONTROL Standard]** 権限を持つすべてのユーザーは、[!DNL Google Analytics] のすべての指標に加え、Data Warehouseのすべてのデータにデータ書き出しを介してアクセスできます。

また、指標を編集し、「**[!UICONTROL Standard]**」セクションでユーザーを選択すること **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)**、指標へのアクセスを制限できます。

>[!NOTE]
>
>指標を複製すると、[!DNL Commerce Intelligence] は元の指標に設定されたユーザー権限をコピーします。
