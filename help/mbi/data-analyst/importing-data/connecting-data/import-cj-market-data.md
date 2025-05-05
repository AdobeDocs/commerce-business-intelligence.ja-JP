---
title: CJ アフィリエイト（コミッション結合）マーケティングデータの読み込み
description: CJ アフィリエイトデータを  [!DNL Commerce Intelligence].L Commerce Intelligence&rbrack; に読み込む方法を説明します。
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# [!DNL CJ Affiliate] データの読み込み

データ [!DNL CJ Affiliate (Commission Junction)][!DNL Adobe Commerce Intelligence] に読み込むには、次の手順に従い、結果のファイルを [ サポートチケット ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) に添付します。 Adobeはアカウントにデータテーブルを設定し、ユーザーが引き続き個別にデータをアップロードできるようにします。

## [!DNL CJ Affiliate] データのエクスポート

1. [!DNL CJ Affiliate] アカウントで、「`Reports`」タブに移動します。

1. 「`Performance`」タブで、「`Report Options`」を選択します。

1. 「`Performance By`」を `Program` に、「`Trend`」を `Daily` に、「`Date Range`」を監査対象の日付範囲に設定します。

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. 「`Run Report`」を選択します。

1. `File Format` ドロップダウンで「`CSV`」を選択します。  「**[!UICONTROL Download]**」をクリックします。

   ![cj アフィリエイトデータのエクスポート ](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. ファイルをダウンロードしたら、[!DNL Commerce Intelligence] Data Warehouseに [ ファイルをアップロード ](../connecting-data/using-file-uploader.md) できます。

   これにより、[!DNL Commerce Intelligence] Data Warehouseにテーブルが作成され、新しいデータを引き続き定期的にアップロードできます。 ファイルをアップロードする場合は、[ ファイルアップローダの使用 ](../connecting-data/using-file-uploader.md) に記載されている書式設定要件に従います。
