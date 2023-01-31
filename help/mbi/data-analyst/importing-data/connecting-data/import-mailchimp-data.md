---
title: MailChimp データをインポート
description: MailChimp データをにインポートする方法を説明します。 [!DNL MBI].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# インポート `MailChimp` データ

キャンペーンの取り組みの包括的な状況を把握するには、 `MailChimp` キャンペーンデータをメールで送る [!DNL MBI]. インポートを完了するには、それぞれに対して次の操作を実行する必要があります `MailChimp` 以下のキャンペーンがあります。

## 開封数データのエクスポート {#opens}

1. へのログイン後 `MailChimp`、 `Campaigns` タブをクリックします。

   ![mailchimp 1 をインポート](../../../assets/import-mailchimp-1.png)

1. クリック **[!UICONTROL View Report]**（キャンペーン名の横）

   ![mailchimp 2 をインポート](../../../assets/import-mailchimp-2.png)

1. 次をクリック： **[!UICONTROL Opened]** 数値。

   ![mailchimp 3 をインポート](../../../assets/import-mailchimp-3.png)

1. クリック **[!UICONTROL Export]** をクリックし、 `.csv` ファイル。

   次を追加する必要があります： `primary key`, `date (mm/dd/yyyy)`、および `campaign name` 列をこのファイルに追加します。 次を確認します。 `primary keys` は、各行に固有です。

   ![mailchimp 4 をインポート](../../../assets/import-mailchimp-4.png)

## クリック数データの書き出し {#clicks}

1. に戻ります。 `View Report` 画面を開きます。

1. 次の番号をクリックします。 `Clicked`.

   ![mailchimp 5 をインポート](../../../assets/import-mailchimp-5.png)

1. 次のいずれかの番号をクリックします。 `Total Clicks` または `Unique Clicks` 列。

   ![mailchimp 6 をインポート](../../../assets/import-mailchimp-6.png)

1. クリック **[!UICONTROL Export]** をクリックし、 `.csv` ファイル。

   次を追加する必要があります： `Primary Key`, `date (mm/dd/yyyy)`, `campaign name`、および `URL` 列をこのファイルに追加します。 完全な URL を追加する必要はありません。何がクリックされたかを知らせる単なる情報です。

   ![mailchimp 7 をインポート](../../../assets/import-mailchimp-7.png)

1. 電子メールでクリックした URL ごとに手順 3 と 4 を繰り返し、すべてのデータを同じに組み合わせます。 `.csv` ファイルを作成します。

## 送信済みデータのエクスポート {#sent}

1. を `Campaigns` MailChimp のタブ

1. クリック **[!UICONTROL View Report]** をクリックします。

1. の横の番号をクリックします。 `Recipients`.

   ![mailchimp 8 をインポート](../../../assets/import-mailchimp-8.png)

1. クリック **[!UICONTROL Export]** をクリックし、 `.csv` ファイル。

   次を追加する必要があります： `Primary Key`, `date (mm/dd/yyyy)`、および `campaign name` 列をこのファイルに追加します。

   ![mailchimp 9 をインポート](../../../assets/import-mailchimp-9.png)

## へのアップロード用ファイルの準備 [!DNL MBI] {#upload}

各ファイル — `Opens`, `Clicks`、および `Sent`  — にアップロードする必要があります [!DNL MBI] を別のファイルとして指定します。 また、この命名規則を使用してファイルに名前を付けることをお勧めします。 `MailChimp\_ACTION\_DATE`. 置換 `ACTION` と `Open`, `Click`または `Sent`、および `DATE` をエクスポート日付と共に追加します。

ファイルをアップロードする準備が整ったら、 [`File Upload` 機能](../connecting-data/using-file-uploader.md) をクリックして、データを data warehouse に取り込みます。
