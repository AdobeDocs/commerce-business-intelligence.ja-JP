---
title: 指標の操作テーブルの変更
description: 指標が操作を実行するために使用するデータテーブルを変更する方法を説明します。
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/9yJ1Zc2NLDvXYO16UvDkeWE0hD1jx0-Ne3AyFFHX5ns
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 231
ht-degree: 0%

---

# 指標の操作テーブルの変更

場合によっては、指標が操作を実行するために使用するデータテーブルを変更することもできます。 例えば、新しいユーザーテーブルがある場合、`Users\_Old` テーブルからユーザー関連の指標を移行して、`Users\_New` テーブルを代わりに使用します。

1. **[!UICONTROL Data]** > **[!UICONTROL Metrics]**&#x200B;に移動
1. **[!UICONTROL Edit]** テーブルを切り替える指標の横にある`operational`をクリックします。
1. エディターで、**[!UICONTROL Change]**&#x200B;をクリックします。

   操作テーブルの設定を示す![指標の定義ページ &#x200B;](../../assets/change-metrics-1.png)
1. この指標のベースとなる新しいテーブルを選択します。
1. 既存のデータディメンションを、新しいテーブル内の対応するデータディメンションに一致させます。 例えば、`User's registration date`という列がある場合は、新しいテーブルのどの列に同じ日付データが記録されているかを選択するだけです。 （新しいテーブルに一致する列がない場合は、次の手順を参照してください）

   ![使用可能なテーブルを表示するテーブル選択ドロップダウン &#x200B;](../../assets/change-metrics-2.png)

1. 新しいテーブルに一致する列がない場合は、**データテーブルに作成するか、**&#x200B;によって作成された計算列またはディメンションである[&#x200B; サポート &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)にお問い合わせください。 [!DNL Commerce Intelligence]指標&#x200B;**からディメンションを**&#x200B;削除することもできます。 不要になったディメンションを削除するには、指標のエディターに戻り、`Dimensions`で削除するディメンションを選択するだけです。

   ![業務列選択ドロップダウンメニュー](../../assets/change-metrics-3.png)
