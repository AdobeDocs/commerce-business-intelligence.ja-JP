---
title: Bing広告支出データのインポート
description: Bing広告費データを[!DNL Commerce Intelligence]に読み込んで分析する方法を説明します。
exl-id: c8dec4b4-74ce-41b2-a77d-403fe44e2816
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/66UAmNWDCkiflHxsq9X1MlkwEgzC5Cl1HfRirNd8AHM'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%
---
# [!DNL Bing] データのインポート

[!DNL Bing]広告費データを[!DNL Adobe Commerce Intelligence]に読み込んで分析するには、[!DNL Bing Ads Editor]から`.csv`形式でデータを書き出し、次の手順に従って[!DNL Commerce Intelligence]にアップロードするだけです。

## [!DNL Bing Ads Editor]

[!DNL Bing Ads] データをエクスポートするには、[!DNL Bing Ads Editor]がインストールされている必要があります。 [[!DNL Bing Ads Editor]](https://about.ads.microsoft.com/en-us/solutions/tools/editor)の無料ダウンロードを見つけることができます。

## [!DNL Bing Ads] データのエクスポート

1. [!DNL Bing Ads Editor]の`Browser` ペインで、書き出すキャンペーンまたは広告グループを右クリックし、**[!UICONTROL Export]**&#x200B;をクリックします。
1. `Export` ダイアログボックスで、**[!UICONTROL Export]**&#x200B;をクリックします。
1. `Save As` ダイアログボックスで、書き出しファイルを保存するフォルダーをクリックします。
1. `File name` ボックスで、ファイルの書き出し名を選択します。
1. **[!UICONTROL Save]**&#x200B;をクリックします。
1. ファイルをダウンロードした後、[ サポート ](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies)に連絡して、お客様に代わって最初のアップロードを実行し、必要なバックエンドディメンションを設定します。
