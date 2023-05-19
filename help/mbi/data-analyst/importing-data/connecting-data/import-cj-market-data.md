---
title: CJ アフィリエイト (Commission Junction) マーケティングデータのインポート
description: CJ アフィリエイト（コミッションジャンクション）データをにインポートする方法を説明します。 [!DNL Commerce Intelligence].L Commerce Intelligence]
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# インポート [!DNL CJ Affiliate] データ

読み込む [!DNL CJ Affiliate (Commission Junction)] データを [!DNL Adobe Commerce Intelligence]以下の手順に従い、結果のファイルをに添付します。 [サポートチケット](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). Adobeがアカウントのデータテーブルを設定し、ユーザーが個別にデータのアップロードを続行できるようにします。

## 書き出し [!DNL CJ Affiliate] データ

1. を [!DNL CJ Affiliate] アカウントに移動します。 `Reports` タブをクリックします。

1. 内 `Performance` タブ、選択 `Report Options`.

1. 設定 `Performance By` 次と等しい `Program`, `Trend` 次と等しい `Daily`、および `Date Range` 監査対象の日付範囲と等しい。

   ![export-cj-affirieate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. 選択 `Run Report`.

1. 内 `File Format` ドロップダウン、選択 `CSV`.  クリック **[!UICONTROL Download]**.

   ![cj アフィリエイトデータのエクスポート](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. ファイルをダウンロードした後、 [ファイルをアップロード](../connecting-data/using-file-uploader.md) を [!DNL Commerce Intelligence] Data Warehouse。

   これにより、 [!DNL Commerce Intelligence] Data Warehouse。新しいデータを定期的ににアップロードし続けることができます。 ファイルをアップロードする際は、 [ファイルアップローダの使用](../connecting-data/using-file-uploader.md).
