---
title: 指標のアクセス制限
description: 指標へのアクセスと制限の操作方法について説明します。
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b6935462-7263-4ced-a703-60de6a5aeb2d
subfeature_v2: id: a763c1a2-1d0a-40d7-9617-8139636fd12e
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 94b6ebcdfcf08c1ef7b878966c0985cdce8f80bd
workflow-type: tm+mt
source-wordcount: 242
ht-degree: 0%

---

# 指標ユーザーの管理

ユーザー権限レベルを設定するだけでなく、ユーザーごとに指標へのアクセスを制限することもできます。 たとえば、経理部門に収益関連の指標へのアクセス権を付与し、ユーザー獲得指標へのアクセス権を付与しない場合は、これらの指標へのアクセスを制限できます。

このような場合、Adobeでは、そのユーザーのアカウントを&#x200B;**[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**&#x200B;に設定することをお勧めします。 **[!UICONTROL Standard]**&#x200B;権限は、指標、計算列、統合、またはユーザーを作成または変更する必要はないが、Data Warehouseのデータにアクセスする必要があるユーザーに付与する必要があります。 データへのアクセスを完全に制限する場合は、代わりに&#x200B;**[!UICONTROL Read Only]**&#x200B;権限を使用してください。

権限レベルを設定したら、次の操作を行うことで、**[!UICONTROL Standard]** ユーザーがアクセスできる指標を選択できます。

1. **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**&#x200B;に移動します。
1. 目的のユーザーアカウントを選択します。
1. 「**[!UICONTROL Metrics]**」タブには、使用可能な指標のリストが表示されます。 ユーザーにアクセス権を付与する指標を確認し、ユーザーにアクセス権を付与しない指標の選択を解除します。
1. [!DNL Adobe Commerce Intelligence]は変更を自動的に保存します。 変更が成功した場合、[!DNL Commerce Intelligence]はページの上部に&#x200B;**[!UICONTROL Saved!]**&#x200B;と表示されます。

>[!NOTE]
>
>**[!UICONTROL Standard]**&#x200B;権限を持つすべてのユーザーは、[!DNL Google Analytics]のすべての指標に加えて、Data Exportを介してData Warehouseのすべてのデータにアクセスできます。

また、**[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** セクションで指標を編集し、**[!UICONTROL Standard]** ユーザーを選択することで、指標へのアクセスを制限することもできます。

>[!NOTE]
>
>指標を複製すると、[!DNL Commerce Intelligence]は元の指標に設定されたユーザー権限をコピーします。


