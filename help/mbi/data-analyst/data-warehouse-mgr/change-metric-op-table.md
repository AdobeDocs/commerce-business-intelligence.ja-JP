---
title: 指標の操作可能テーブルの変更
description: 指標が操作の実行に使用するデータテーブルを変更する方法を説明します。
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# 指標の操作可能テーブルの変更

場合によっては、指標が操作の実行に使用するデータテーブルを変更することにします。 例えば、新しいユーザーテーブルがある場合、  `Users\_Old` 使用するテーブル `Users\_New` テーブルを使用します。

1. に移動します。 **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. クリック **[!UICONTROL Edit]** をクリックします。 `operational` 表。
1. エディターで、 **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. この指標のベースにする新しいテーブルを選択します。
1. 既存のデータディメンションを、新しいテーブルの対応するディメンションに一致させます。 例えば、 `User's registration date`に値を入力する場合は、新しいテーブル内で同じ日付データを記録する列を選択するだけです。 （新しいテーブルに一致する列がない場合は、次の手順を参照）

   ![](../../assets/change-metrics-2.png)

1. 新しいテーブルに一致する列がない場合は、次のいずれかを実行できます。 **データテーブルに作成します。** または [連絡先サポート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) が次の方法で作成された計算列または次元の場合： [!DNL Commerce Intelligence]. また、 **指標からディメンションを削除**. 不要になったディメンションを削除するには、指標のエディターに戻って、削除するディメンションを「 」の下で選択します `Dimensions`.

   ![](../../assets/change-metrics-3.png)
