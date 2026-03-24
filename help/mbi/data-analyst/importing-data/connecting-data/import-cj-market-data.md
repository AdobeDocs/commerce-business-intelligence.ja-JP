---
title: CJ アフィリエイト（Commission Junction）マーケティングデータのインポート
description: CJ Affiliate （Commission Junction） データを [!DNL Commerce Intelligence].L Commerce Intelligence&rbrack;に読み込む方法について説明します。
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
TQID: https://experienceleague.adobe.com/tZ2fzAKou0fBmkmKD5zdLFBNCSiAGpT3GNgkHp9ptx4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 141
ht-degree: 0%

---

# [!DNL CJ Affiliate] データの読み込み

[!DNL CJ Affiliate (Commission Junction)] データを[!DNL Adobe Commerce Intelligence]に読み込むには、次の手順に従って、生成されたファイルを[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)に添付するだけです。 Adobeは、アカウントのデータテーブルを設定し、引き続きデータを個別にアップロードできます。

## [!DNL CJ Affiliate] データの書き出し

1. [!DNL CJ Affiliate] アカウントで、「`Reports`」タブに移動します。

1. 「`Performance`」タブで、「`Report Options`」を選択します。

1. `Performance By`を`Program`に、`Trend`を`Daily`に、`Date Range`を監査中の日付範囲に設定します。

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. `Run Report`を選択します。

1. `File Format` ドロップダウンで、`CSV`を選択します。  **[!UICONTROL Download]**&#x200B;をクリックします。

   ![cj アフィリエイトデータの書き出し](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. ファイルをダウンロードしたら、[&#x200B; ファイル &#x200B;](../connecting-data/using-file-uploader.md)を[!DNL Commerce Intelligence] Data Warehouseにアップロードできます。

   これにより、[!DNL Commerce Intelligence] Data Warehouseにテーブルが作成され、定期的に新しいデータをアップロードし続けることができます。 ファイルをアップロードする場合は、[&#x200B; ファイルアップローダーの使用](../connecting-data/using-file-uploader.md)に記載されている書式要件に従います。
