---
title: MailChimp データをインポート
description: MailChimp データをにインポートする方法を説明します。 [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# インポート [!DNL Mailchimp] データ

キャンペーンの取り組みの包括的な状況を把握するには、 [!DNL Mailchimp] キャンペーンデータをメールで送る [!DNL Commerce Intelligence]. インポートを完了するには、それぞれに対して次の操作を実行する必要があります [!DNL Mailchimp] 以下のキャンペーンがあります。

## 開封数データを書き出し {#opens}

1. へのログイン後 [!DNL Mailchimp]、に移動します。 `Campaigns` タブをクリックします。

   ![mailchimp 1 をインポート](../../../assets/import-mailchimp-1.png)

1. クリック **[!UICONTROL View Report]**（キャンペーン名の横）をクリックします。

   ![mailchimp 2 をインポート](../../../assets/import-mailchimp-2.png)

1. 次をクリック： **[!UICONTROL Opened]** 数値。

   ![mailchimp 3 をインポート](../../../assets/import-mailchimp-3.png)

1. クリック **[!UICONTROL Export]** をクリックし、 `.csv` ファイル。

   を追加する必要があります `primary key`, `date (mm/dd/yyyy)`、および `campaign name` 列をこのファイルに追加します。 次を確認します。 `primary keys` は、各行に固有です。

   ![mailchimp 4 をインポート](../../../assets/import-mailchimp-4.png)

## クリック数データの書き出し {#clicks}

1. に戻ります。 `View Report` 画面を開きます。

1. 次の番号をクリックします。 `Clicked`.

   ![mailchimp 5 をインポート](../../../assets/import-mailchimp-5.png)

1. 次のいずれかの数値をクリックします： `Total Clicks` または `Unique Clicks` 列。

   ![mailchimp 6 をインポート](../../../assets/import-mailchimp-6.png)

1. クリック **[!UICONTROL Export]** をクリックし、 `.csv` ファイル。

   を追加する必要があります `Primary Key`, `date (mm/dd/yyyy)`, `campaign name`、および `URL` 列をこのファイルに追加します。 完全な URL を追加する必要はありません。何がクリックされたかを知らせる単なる手段です。

   ![mailchimp 7 をインポート](../../../assets/import-mailchimp-7.png)

1. 電子メールでクリックした URL ごとに手順 3 と 4 を繰り返し、すべてのデータを同じに組み合わせます。 `.csv` ファイルを作成します。

## 送信済みデータの書き出し {#sent}

1. 次に進みます。 `Campaigns` タブ [!DNL Mailchimp].

1. クリック **[!UICONTROL View Report]** キャンペーン名の横に表示されます。

1. の横の数字をクリックします。 `Recipients`.

   ![mailchimp 8 をインポート](../../../assets/import-mailchimp-8.png)

1. クリック **[!UICONTROL Export]** をクリックし、 `.csv` ファイル。

   を追加する必要があります `Primary Key`, `date (mm/dd/yyyy)`、および `campaign name` 列をこのファイルに追加します。

   ![mailchimp 9 をインポート](../../../assets/import-mailchimp-9.png)

## へのアップロード用ファイルの準備 [!DNL Commerce Intelligence] {#upload}

各ファイル — `Opens`, `Clicks`、および `Sent`  — にアップロードする必要があります [!DNL Commerce Intelligence] を別のファイルとして指定します。 Adobeでは、次の命名規則を使用してファイルに名前を付けることをお勧めします。 `MailChimp\_ACTION\_DATE`. 置換 `ACTION` 次を使用 `Open`, `Click`または `Sent`、および `DATE` を、エクスポート日付と共に追加します。

ファイルをアップロードする準備が整ったら、 [`File Upload` 機能](../connecting-data/using-file-uploader.md) データをData Warehouseに取り込む
