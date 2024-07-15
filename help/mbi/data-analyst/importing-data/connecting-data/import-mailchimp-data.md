---
title: MailChimp データのインポート
description: MailChimp データを  [!DNL Commerce Intelligence] にインポートする方法を説明します。
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# [!DNL Mailchimp] データの読み込み

キャンペーンの取り組みを包括的に把握するために、[!DNL Mailchimp] しいメールキャンペーンデータを [!DNL Commerce Intelligence] にインポートできます。 読み込みを完了するには、使用する [!DNL Mailchimp] キャンペーンごとに次の手順を実行する必要があります。

## 開封数データのエクスポート {#opens}

1. [!DNL Mailchimp] にログインしたら、「`Campaigns`」タブに移動します。

   ![mailchimp 1 の読み込み ](../../../assets/import-mailchimp-1.png)

1. キャンペーン名の横にある「**[!UICONTROL View Report]**」をクリックします。

   ![mailchimp 2 を読み込みます ](../../../assets/import-mailchimp-2.png)

1. **[!UICONTROL Opened]** 番号をクリックします。

   ![mailchimp 3 を読み込みます ](../../../assets/import-mailchimp-3.png)

1. 「**[!UICONTROL Export]**」をクリックして、`.csv` ファイルを保存します。

   このファイルに `primary key`、`date (mm/dd/yyyy)`、および `campaign name` 列を追加する必要があります。 `primary keys` が各行に対して一意であることを確認します。

   ![mailchimp 4 を読み込む ](../../../assets/import-mailchimp-4.png)

## クリックデータの書き出し {#clicks}

1. キャンペーンの `View Report` 画面に戻ります。

1. `Clicked` の番号をクリックします。

   ![mailchimp 5 をインポート ](../../../assets/import-mailchimp-5.png)

1. `Total Clicks` または `Unique Clicks` 列の下にある数字をクリックします。

   ![mailchimp 6 をインポート ](../../../assets/import-mailchimp-6.png)

1. 「**[!UICONTROL Export]**」をクリックして、`.csv` ファイルを保存します。

   このファイルに `Primary Key`、`date (mm/dd/yyyy)`、`campaign name`、および `URL` 列を追加する必要があります。 完全な URL を追加する必要はありません。クリックされた内容が分かるだけです。

   ![mailchimp 7 をインポート ](../../../assets/import-mailchimp-7.png)

1. 完了したら、すべてのデータを同じ `.csv` ファイルに結合して、メールでクリックされた URL ごとに手順 3 と 4 を繰り返します。

## 送信済みデータを書き出し {#sent}

1. [!DNL Mailchimp] の「`Campaigns`」タブに移動します。

1. キャンペーン名の横にある「**[!UICONTROL View Report]**」をクリックします。

1. 「`Recipients`」の横の数字をクリックします。

   ![mailchimp 8 をインポート ](../../../assets/import-mailchimp-8.png)

1. 「**[!UICONTROL Export]**」をクリックして、`.csv` ファイルを保存します。

   このファイルに `Primary Key`、`date (mm/dd/yyyy)`、および `campaign name` 列を追加する必要があります。

   ![mailchimp 9 をインポート ](../../../assets/import-mailchimp-9.png)

## [!DNL Commerce Intelligence] にアップロードするファイルの準備 {#upload}

`Opens`、`Clicks`、`Sent` の各ファイルは、個別のファイルとして [!DNL Commerce Intelligence] にアップロードする必要があります。 Adobeでは、次の命名規則を使用してファイルに名前を付けることをお勧めします。`MailChimp\_ACTION\_DATE` `ACTION` を `Open`、`Click` または `Sent` に、`DATE` をエクスポート日に置き換えます。

ファイルをアップロードする準備が整ったら、[`File Upload` 機能を使用して ](../connecting-data/using-file-uploader.md) データをData Warehouseに取り込みます。
