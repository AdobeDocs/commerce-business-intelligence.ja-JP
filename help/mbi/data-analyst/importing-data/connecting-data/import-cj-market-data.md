---
title: CJ アフィリエイト (Commission Junction) マーケティングデータのインポート
description: CJ アフィリエイト（コミッションジャンクション）データをにインポートする方法を説明します。 [!DNL MBI].L MBI]
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# インポート `CJ Affiliate` データ

読み込む `CJ Affiliate` （委員会の接合）データ [!DNL MBI]の場合は、次の手順に従い、結果のファイルをサポートチケットに添付します。 Adobeがアカウントのデータテーブルを設定し、ユーザーが個別にデータのアップロードを続行できるようにします。

## 書き出し `CJ Affiliate` データ

1. を `CJ Affiliate` アカウントに移動します。 `Reports` タブをクリックします。

1. 内 `Performance` タブ、選択 `Report Options`.

1. 設定 `Performance By` 次と等しい `Program`, `Trend` 次と等しい `Daily`、および `Date Range` 監査対象の日付範囲と等しい。

   ![export-cj-affirieate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. 選択 `Run Report`.

1. 内 `File Format` ドロップダウン、選択 `CSV`.  クリック **[!UICONTROL Download]**.

   ![cj アフィリエイトデータのエクスポート](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. ファイルをダウンロードした後、 [ファイルをアップロード](../connecting-data/using-file-uploader.md) を [!DNL MBI] Data Warehouse。

   これにより、 [!DNL MBI] Data Warehouse。新しいデータを定期的ににアップロードし続けることができます。 ファイルをアップロードする際は、必ず [ファイルアップローダの使用](../connecting-data/using-file-uploader.md).
