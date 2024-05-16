---
title: リンク共有データの読み込み
description: Linkshare データのへの読み込み方法を説明します [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# インポート [!DNL Linkshare] データ

お持ち込み下さい [!DNL Linkshare] データ対象 [!DNL Adobe Commerce Intelligence]は、次の 2 つの操作をおこなう必要があります。

1. [でのリンク共有データのエクスポート ](#export)
1. [スプレッドシートをにアップロードします [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Linkshare からのデータのエクスポート {#export}

1. あなたの [!DNL Linkshare] アカウント、に移動 **[!UICONTROL Reports** > **Run Reports].**

1. が含まれる `Report` ドロップダウン、選択 **[!UICONTROL Sales & Activity Report]**.

1. 他のすべてのドロップダウンオプションはデフォルトのままにします。

1. が含まれる `Date Range` ドロップダウンで、いずれかのオプション（`Sun - Sat`, `Mon - Sun`）がと一致します `Start of Week` の設定 [!DNL Commerce Intelligence].

1. をクリア `Compare Year-Over-Year Data` チェックボックス。

1. 次の下 `Data Type`を選択 `Transaction Date`.

   ![インポート\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. クリック **[!UICONTROL View Report]**.

1. クリック **[!UICONTROL Download]**.

   この時点で、 `.csv` ファイルをダウンロードしました。

ファイルをダウンロードしたら、次の場所にアップロードできます [!DNL Commerce Intelligence] の使用 [`File Upload` 機能](../connecting-data/using-file-uploader.md).
