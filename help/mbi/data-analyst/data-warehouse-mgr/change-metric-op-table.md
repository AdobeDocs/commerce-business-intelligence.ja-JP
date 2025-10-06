---
title: 指標の操作テーブルの変更
description: 指標が操作の実行に使用するデータテーブルの変更方法を説明します。
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# 指標の操作テーブルの変更

場合によっては、指標が操作の実行に使用するデータテーブルを変更することもできます。 例えば、新しいユーザーテーブルがある場合、ユーザー関連の指標を `Users\_Old` テーブルから移行して、代わりに `Users\_New` テーブルを使用するとします。

1. **[!UICONTROL Data]**/**[!UICONTROL Metrics]** に移動します。
1. **[!UICONTROL Edit]** テーブルを切り替える指標の横にある「`operational`」をクリックします。
1. エディターで、「**[!UICONTROL Change]**」をクリックします。

   ![ 操作テーブルの設定を示す指標定義ページ ](../../assets/change-metrics-1.png)
1. この指標のベースとする新しいテーブルを選択します。
1. 既存のデータディメンションを、新しいテーブル内の対応するディメンションに一致させます。 例えば、`User's registration date` という列がある場合、新しいテーブルのどの列に同じ日付データが記録されているかを選択するだけです。 （新しいテーブルに一致する列がない場合は、次の手順を参照）

   ![ 使用可能なテーブルを表示するテーブル選択ドロップダウン ](../../assets/change-metrics-2.png)

1. 新しいテーブルに一致する列がない場合は、**データ テーブル内で作成する** か、[ が作成した計算列またはディメンションである場合は ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) サポートにお問い合わせください [!DNL Commerce Intelligence] ことができます。 また、**指標からディメンションを削除する** こともできます。 不要になったディメンションを削除するには、指標のエディターに戻り、削除するディメンションを `Dimensions` で選択します。

   ![ 操作列選択ドロップダウンメニュー ](../../assets/change-metrics-3.png)
