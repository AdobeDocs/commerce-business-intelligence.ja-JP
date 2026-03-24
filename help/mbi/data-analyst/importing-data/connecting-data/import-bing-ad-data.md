---
title: Bing広告支出データのインポート
description: 分析のためにBing広告費データを [!DNL Commerce Intelligence] にインポートする方法について説明します。
exl-id: c8dec4b4-74ce-41b2-a77d-403fe44e2816
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/66UAmNWDCkiflHxsq9X1MlkwEgzC5Cl1HfRirNd8AHM
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
source-wordcount: 131
ht-degree: 0%

---

# [!DNL Bing] データのインポート

[!DNL Bing]広告費データを[!DNL Adobe Commerce Intelligence]に読み込んで分析するには、[!DNL Bing Ads Editor]から`.csv`形式でデータを書き出し、次の手順に従って[!DNL Commerce Intelligence]にアップロードするだけです。

## [!DNL Bing Ads Editor]

[!DNL Bing Ads] データをエクスポートするには、[!DNL Bing Ads Editor]がインストールされている必要があります。 [[!DNL Bing Ads Editor]](https://about.ads.microsoft.com/en-us/solutions/tools/editor)の無料ダウンロードを見つけることができます。

## [!DNL Bing Ads] データのエクスポート

1. `Browser`の[!DNL Bing Ads Editor] ペインで、書き出すキャンペーンまたは広告グループを右クリックし、**[!UICONTROL Export]**&#x200B;をクリックします。
1. `Export` ダイアログボックスで、**[!UICONTROL Export]**&#x200B;をクリックします。
1. `Save As` ダイアログボックスで、書き出しファイルを保存するフォルダーをクリックします。
1. `File name` ボックスで、ファイルの書き出し名を選択します。
1. **[!UICONTROL Save]**&#x200B;をクリックします。
1. ファイルをダウンロードした後、[&#x200B; サポート &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)に連絡して、お客様に代わって最初のアップロードを実行し、必要なバックエンドディメンションを設定します。
