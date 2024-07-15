---
title: リンク共有データの読み込み
description: Linkshare データの  [!DNL Commerce Intelligence] への読み込みについて説明します。
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# [!DNL Linkshare] データの読み込み

[!DNL Linkshare] データを [!DNL Adobe Commerce Intelligence] に取り込むには、次の 2 つの操作が必要です。

1. [でのリンク共有データのエクスポート ](#export)
1. [スプレッドシートをにアップロードします  [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Linkshare からのデータのエクスポート {#export}

1. [!DNL Linkshare] アカウントで、**[!UICONTROL Reports** > **Run Reports].** に移動します

1. `Report` ドロップダウンで「**[!UICONTROL Sales & Activity Report]**」を選択します。

1. 他のすべてのドロップダウンオプションはデフォルトのままにします。

1. 「`Date Range`」ドロップダウンで、[!DNL Commerce Intelligence] で `Start of Week` 定した設定と一致するオプション（`Sun - Sat`、`Mon - Sun`）を選択します。

1. 「`Compare Year-Over-Year Data`」チェックボックスをオフにします。

1. 「`Data Type`」で、「`Transaction Date`」を選択します。

   ![importing\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. 「**[!UICONTROL View Report]**」をクリックします。

1. 「**[!UICONTROL Download]**」をクリックします。

   この時点で、`.csv` ファイルがダウンロードされました。

ファイルをダウンロードしたら、[`File Upload` 機能を使用して [!DNL Commerce Intelligence] にアップロードでき ](../connecting-data/using-file-uploader.md) す。
