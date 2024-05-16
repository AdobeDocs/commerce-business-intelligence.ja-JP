---
title: MailChimp データのインポート
description: MailChimp データをにインポートする方法を説明します [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# インポート [!DNL Mailchimp] データ

キャンペーンの取り組みを包括的に把握するには、 [!DNL Mailchimp] キャンペーンデータをにメールで送信 [!DNL Commerce Intelligence]. 読み込みを完了するには、次の各項目を実行する必要があります [!DNL Mailchimp] 保有しているキャンペーン：

## 開封数データのエクスポート {#opens}

1. にログインした後 [!DNL Mailchimp]に移動します。 `Campaigns` タブ。

   ![mailchimp 1 の読み込み](../../../assets/import-mailchimp-1.png)

1. クリック **[!UICONTROL View Report]**、キャンペーン名の横にあります。

   ![mailchimp 2 の読み込み](../../../assets/import-mailchimp-2.png)

1. 「」をクリックします **[!UICONTROL Opened]** 数値。

   ![mailchimp 3 の読み込み](../../../assets/import-mailchimp-3.png)

1. クリック **[!UICONTROL Export]** を作成して、 `.csv` ファイル。

   次を追加する必要があります `primary key`, `date (mm/dd/yyyy)`、および `campaign name` 列をこのファイルに追加します。 必ずを実行してください `primary keys` は各行に一意です。

   ![mailchimp 4 の読み込み](../../../assets/import-mailchimp-4.png)

## クリックデータの書き出し {#clicks}

1. に戻ります。 `View Report` キャンペーンの画面。

1. という数字をクリックします `Clicked`.

   ![mailchimp 5 のインポート](../../../assets/import-mailchimp-5.png)

1. の下にある数字をクリックします `Total Clicks` または `Unique Clicks` 列。

   ![mailchimp 6 のインポート](../../../assets/import-mailchimp-6.png)

1. クリック **[!UICONTROL Export]** を作成して、 `.csv` ファイル。

   次を追加する必要があります `Primary Key`, `date (mm/dd/yyyy)`, `campaign name`、および `URL` 列をこのファイルに追加します。 完全な URL を追加する必要はありません。クリックされた内容が分かるだけです。

   ![mailchimp 7 を読み込みます](../../../assets/import-mailchimp-7.png)

1. メールでクリックされた各 URL に対して、手順 3 と 4 を繰り返し、すべてのデータを同じに組み合わせます `.csv` ファイルが終了しました。

## 送信済みデータを書き出し {#sent}

1. に移動します `Campaigns` タブ / [!DNL Mailchimp].

1. クリック **[!UICONTROL View Report]** キャンペーン名の隣です。

1. の横の数字をクリックします `Recipients`.

   ![mailchimp 8 のインポート](../../../assets/import-mailchimp-8.png)

1. クリック **[!UICONTROL Export]** を作成して、 `.csv` ファイル。

   次を追加する必要があります `Primary Key`, `date (mm/dd/yyyy)`、および `campaign name` 列をこのファイルに追加します。

   ![mailchimp 9 のインポート](../../../assets/import-mailchimp-9.png)

## へのアップロード用ファイルの準備 [!DNL Commerce Intelligence] {#upload}

各ファイル - `Opens`, `Clicks`、および `Sent`  – をにアップロードする必要があります [!DNL Commerce Intelligence] 別のファイルとして。 Adobeでは、次の命名規則を使用してファイルに名前を付けることをお勧めします。 `MailChimp\_ACTION\_DATE`. 置換 `ACTION` （を使用） `Open`, `Click`、または `Sent`、および置換 `DATE` （輸出年月日）

ファイルをアップロードする準備が整ったら、 [`File Upload` 機能](../connecting-data/using-file-uploader.md) ：データをData Warehouseに取り込みます。
