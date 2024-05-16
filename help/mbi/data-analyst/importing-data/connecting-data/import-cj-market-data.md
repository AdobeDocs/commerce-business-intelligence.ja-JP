---
title: CJ アフィリエイト（コミッション結合）マーケティングデータの読み込み
description: CJ アフィリエイトデータの次への読み込み方法を説明します [!DNL Commerce Intelligence].L Commerce Intelligence].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# インポート [!DNL CJ Affiliate] データ

インポートする [!DNL CJ Affiliate (Commission Junction)] データ対象 [!DNL Adobe Commerce Intelligence]で作成します。次の手順に従い、結果のファイルをに添付するだけです [サポートチケット](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). Adobeはアカウントにデータテーブルを設定し、ユーザーが引き続き個別にデータをアップロードできるようにします。

## Export [!DNL CJ Affiliate] データ

1. あなたの [!DNL CJ Affiliate] アカウント、に移動 `Reports` タブ。

1. が含まれる `Performance` タブ、選択 `Report Options`.

1. を設定 `Performance By` 次と等しい `Program`, `Trend` 次と等しい `Daily`、および `Date Range` は、監査される日付範囲と等しくなります。

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. を選択 `Run Report`.

1. が含まれる `File Format` ドロップダウン、選択 `CSV`.  クリック **[!UICONTROL Download]**.

   ![cj アフィリエイトデータのエクスポート](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. ファイルのダウンロードが完了したら、次の操作を実行できます [ファイルをアップロードします](../connecting-data/using-file-uploader.md) 宛先： [!DNL Commerce Intelligence] Data Warehouse。

   これにより、にテーブルが作成されます [!DNL Commerce Intelligence] 新しいデータを定期的ににアップロードし続けることができるData Warehouse。 ファイルをアップロードする際は、次に示す書式設定要件に従います [ファイルアップローダの使用](../connecting-data/using-file-uploader.md).
