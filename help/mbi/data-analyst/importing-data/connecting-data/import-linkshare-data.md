---
title: Linkshare データをインポート中
description: Linkshare データをに読み込む方法を説明します。 [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 2%

---

# インポート [!DNL Linkshare] データ

次の手順で [!DNL Linkshare] データを [!DNL Adobe Commerce Intelligence]次の 2 つの操作を実行する必要があります。

1. [Linkshare のデータをに書き出す ](#export)
1. [にスプレッドシートをアップロードします。 [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Linkshare からデータを書き出す {#export}

1. を [!DNL Linkshare] アカウント、に移動します。 **[!UICONTROL Reports** > **Run Reports].**

1. Adobe Analytics の `Report` ドロップダウン、選択 **[!UICONTROL Sales & Activity Report]**.

1. その他のすべてのドロップダウンオプションはデフォルトの選択のままにします。

1. Adobe Analytics の `Date Range` ドロップダウンで、どちらかのオプション (`Sun - Sat`, `Mon - Sun`) が `Start of Week` の設定 [!DNL Commerce Intelligence].

1. 次をクリア： `Compare Year-Over-Year Data` チェックボックス。

1. の下 `Data Type`を選択します。 `Transaction Date`.

   ![importing\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. クリック **[!UICONTROL View Report]**.

1. クリック **[!UICONTROL Download]**.

   この時点で、 `.csv` ファイルに保存し、ダウンロードしました。

ファイルのダウンロード後は、次の場所にアップロードできます。 [!DNL Commerce Intelligence] の使用 [`File Upload` 機能](../connecting-data/using-file-uploader.md).
