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

このような場合、Adobeでは、そのユーザーのアカウントをに設定することをお勧めします **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** 指標、計算列、統合またはユーザーを作成または変更する必要はないが、Data Warehouse内のデータにアクセスする必要があるユーザーには権限を付与する必要があります。 データへのアクセスを完全に制限するには、 **[!UICONTROL Read Only]** 代わりに、権限を使用します。

権限レベルを設定した後、指標 a **[!UICONTROL Standard]** ユーザーは、次の操作を行ってにアクセスできます。

1. に移動 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. 目的のユーザーアカウントを選択します。
1. この **[!UICONTROL Metrics]** tab キーを押すと、使用可能な指標のリストが表示されます。 ユーザーがアクセスできる指標を確認し、ユーザーがアクセス権を持たない指標の選択を解除します。
1. [!DNL Adobe Commerce Intelligence] 変更を自動的に保存します。 変更に成功した場合、 [!DNL Commerce Intelligence] ディスプレイ **[!UICONTROL Saved!]** ページの上部

>[!NOTE]
>
>を使用するすべてのユーザー **[!UICONTROL Standard]** 権限では、以下のすべての指標に加えて、データエクスポートを通じてData Warehouse内のすべてのデータにアクセスできます [!DNL Google Analytics].

また、指標を編集して、指標へのアクセスを制限できます。 **[!UICONTROL Standard]** でのユーザーの選択 **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** セクション。

>[!NOTE]
>
>指標を複製する場合、 [!DNL Commerce Intelligence] 元の指標に設定されたユーザー権限をコピーします。
