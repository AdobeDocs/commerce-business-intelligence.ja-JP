---
title: 指標の操作テーブルの変更
description: 指標が操作の実行に使用するデータテーブルの変更方法を説明します。
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# 指標の操作テーブルの変更

場合によっては、指標が操作の実行に使用するデータテーブルを変更することもできます。 例えば、新しいユーザーテーブルがある場合、ユーザー関連の指標をから移行するとします  `Users\_Old` を使用するテーブル `Users\_New` 代わりにテーブルを使用します。

1. に移動 **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. クリック **[!UICONTROL Edit]** を切り替える指標の横 `operational` テーブル。
1. エディターで、 **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. この指標のベースとする新しいテーブルを選択します。
1. 既存のデータディメンションを、新しいテーブル内の対応するディメンションに一致させます。 例えば、という列があるとします。 `User's registration date`新しいテーブルのどの列に同じ日付データを記録するかを選択するだけです。 （新しいテーブルに一致する列がない場合は、次の手順を参照）

   ![](../../assets/change-metrics-2.png)

1. 新しいテーブルに一致する列がない場合、次のいずれかを実行できます **データテーブルでの作成** または [サポートに連絡する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 計算列または計算次元の作成者 [!DNL Commerce Intelligence]. 以下の手順でも可能です **指標からのディメンションの削除**. 不要になったディメンションを削除するには、指標のエディターに戻り、削除するディメンションを選択します `Dimensions`.

   ![](../../assets/change-metrics-3.png)
