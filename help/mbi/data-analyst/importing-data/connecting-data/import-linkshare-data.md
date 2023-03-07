---
title: Linkshare データをインポート中
description: Linkshare データをに読み込む方法を説明します。 [!DNL MBI].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# インポート `Linkshare` データ

お客様の `Linkshare` データを [!DNL MBI]次の 2 つの操作を実行する必要があります。

1. [Linkshare のデータをにエクスポートします。 ](#export)
1. [にスプレッドシートをアップロードします。 [!DNL MBI]](../connecting-data/using-file-uploader.md)

## Linkshare からデータを書き出す {#export}

1. を `Linkshare` アカウント、に移動します。 **[!UICONTROL Reports** > **Run Reports].**

1. 内 `Report` ドロップダウン、選択 **[!UICONTROL Sales & Activity Report]**.

1. その他のすべてのドロップダウンオプションはデフォルトの選択のままにします。

1. 内 `Date Range` ドロップダウンで、いずれかのオプション (`Sun - Sat`, `Mon - Sun`) が `Start of Week` の設定 [!DNL MBI].

1. をクリア `Compare Year-Over-Year Data` チェックボックス。

1. の下 `Data Type`を選択します。 `Transaction Date`.

   ![importing\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. クリック **[!UICONTROL View Report]**.

1. クリック **[!UICONTROL Download]**.

   この時点で、 `.csv` ファイルに保存し、ダウンロードしました。

ファイルのダウンロード後は、次の場所にアップロードできます。 [!DNL MBI] の使用 [`File Upload` 機能](../connecting-data/using-file-uploader.md).
