---
title: Bing Ad 費用データのインポート
description: 分析用に Bing 広告費用データをに読み込む方法  [!DNL Commerce Intelligence]  説明します。
exl-id: c8dec4b4-74ce-41b2-a77d-403fe44e2816
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# [!DNL Bing] データの読み込み

広告費用データ [!DNL Bing] 分析用に [!DNL Adobe Commerce Intelligence] に読み込むには、以下の手順に従って、[!DNL Bing Ads Editor] から `.csv` 形式でデータを書き出し、[!DNL Commerce Intelligence] にアップロードするだけです。

## [!DNL Bing Ads Editor]

[!DNL Bing Ads] データを書き出すには、[!DNL Bing Ads Editor] がインストールされている必要があります。 あなたは [[!DNL Bing Ads Editor]](https://about.ads.microsoft.com/en-us/solutions/tools/editor) の無料ダウンロードを見つけることができます。

## [!DNL Bing Ads] データの書き出し

1. `Browser` の [!DNL Bing Ads Editor] ウィンドウ枠で、エクスポートするキャンペーンまたは広告グループを右クリックし、「**[!UICONTROL Export]**」をクリックします。
1. `Export` ダイアログボックスで、「**[!UICONTROL Export]**」をクリックします。
1. `Save As` ダイアログボックスで、書き出しファイルを保存するフォルダーをクリックします。
1. `File name` ボックスで、ファイルの書き出しの名前を選択します。
1. 「**[!UICONTROL Save]**」をクリックします。
1. ファイルをダウンロードしたら、[ サポートにお問い合わせ ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja) し、ユーザーに代わって最初のアップロードを実行し、必要なバックエンドディメンションを設定します。
