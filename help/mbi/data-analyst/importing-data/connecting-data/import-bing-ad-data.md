---
title: Bing Ad 費用データのインポート
description: Bing 広告費用データのへの読み込みを学ぶ [!DNL Commerce Intelligence] 分析用。
exl-id: c8dec4b4-74ce-41b2-a77d-403fe44e2816
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# インポート [!DNL Bing] データ

インポートする [!DNL Bing] 広告費用データの対象 [!DNL Adobe Commerce Intelligence] 分析の場合、次の場所からデータを書き出すだけです。 [!DNL Bing Ads Editor] in a `.csv` の形式をにアップロードします [!DNL Commerce Intelligence] 以下の手順に従います。

## [!DNL Bing Ads Editor]

をエクスポートするには [!DNL Bing Ads] データです。次が必要です [!DNL Bing Ads Editor] インストールされています。 次の項目を無料でダウンロードできます。 [[!DNL Bing Ads Editor]](https://about.ads.microsoft.com/en-us/solutions/tools/editor).

## [!DNL Bing Ads] データ書き出し

1. が含まれる `Browser` 次のパネル [!DNL Bing Ads Editor]エクスポートするキャンペーンまたは広告グループを右クリックし、 **[!UICONTROL Export]**.
1. が含まれる `Export` ダイアログ ボックスで、 **[!UICONTROL Export]**.
1. が含まれる `Save As` ダイアログ ボックスで、書き出しファイルを保存するフォルダをクリックします。
1. が含まれる `File name` ボックスに、ファイルの書き出しの名前を選択します。
1. クリック **[!UICONTROL Save]**.
1. ファイルのダウンロード後、  [サポートに連絡する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) に代わって最初のアップロードを実行し、必要なバックエンドディメンションを設定します。
