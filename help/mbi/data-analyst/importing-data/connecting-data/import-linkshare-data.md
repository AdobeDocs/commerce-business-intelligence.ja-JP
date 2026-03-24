---
title: Linkshare データのインポート
description: Linkshare データを [!DNL Commerce Intelligence]にインポートする方法を説明します。
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/TsQYXEwH-8m1rpKg6It8wa-B2eQH0oqDkLcgx-tRBWU
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 94
ht-degree: 0%

---

# [!DNL Linkshare] データの読み込み

[!DNL Linkshare] データを[!DNL Adobe Commerce Intelligence]に取り込むには、次の2つの操作を行う必要があります。

1. [でLinkshare データを書き出す ](#export)
1. [スプレッドシートを [!DNL Commerce Intelligence]にアップロード](../connecting-data/using-file-uploader.md)

## Linkshareからのデータのエクスポート {#export}

1. [!DNL Linkshare] アカウントで、**[!UICONTROL Reports** > **Run Reports]に移動します。**

1. `Report` ドロップダウンで、**[!UICONTROL Sales & Activity Report]**&#x200B;を選択します。

1. その他のドロップダウンオプションはすべてデフォルトの選択範囲のままにします。

1. `Date Range` ドロップダウンで、`Sun - Sat`の`Mon - Sun`設定と一致するオプション （`Start of Week`、[!DNL Commerce Intelligence]）を選択します。

1. 「`Compare Year-Over-Year Data`」チェックボックスをオフにします。

1. `Data Type`で、`Transaction Date`を選択します。

   ![importing\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. **[!UICONTROL View Report]**&#x200B;をクリックします。

1. **[!UICONTROL Download]**&#x200B;をクリックします。

   この時点で`.csv` ファイルがダウンロードされました。

ファイルをダウンロードしたら、[!DNL Commerce Intelligence]機能[`File Upload`を使用して](../connecting-data/using-file-uploader.md)にアップロードできます。
