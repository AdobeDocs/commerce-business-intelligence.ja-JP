---
title: MailChimp データのインポート
description: MailChimp データを [!DNL Commerce Intelligence]に読み込む方法について説明します。
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/HJJYKfqc1sbslQimSNituG6Pm6wi6QpU-vn6GtKvV-Y
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 274
ht-degree: 0%

---

# [!DNL Mailchimp] データの読み込み

キャンペーン活動の全体像を把握するには、[!DNL Mailchimp]件の電子メールキャンペーンデータを[!DNL Commerce Intelligence]にインポートできます。 インポートを完了するには、お持ちの各[!DNL Mailchimp] キャンペーンに対して次の操作を行う必要があります。

## Export Opens data {#opens}

1. [!DNL Mailchimp]にログインしたら、「`Campaigns`」タブに移動します。

   ![mailchimp 1](../../../assets/import-mailchimp-1.png)のインポート

1. キャンペーン名の横にある「**[!UICONTROL View Report]**」をクリックします。

   ![mailchimp 2](../../../assets/import-mailchimp-2.png)のインポート

1. **[!UICONTROL Opened]**&#x200B;番号をクリックします。

   ![mailchimp 3](../../../assets/import-mailchimp-3.png)のインポート

1. **[!UICONTROL Export]**&#x200B;をクリックして、`.csv` ファイルを保存します。

   このファイルに`primary key`、`date (mm/dd/yyyy)`、`campaign name`列を追加する必要があります。 `primary keys`が各行に一意であることを確認してください。

   ![mailchimp 4](../../../assets/import-mailchimp-4.png)のインポート

## クリック数データの書き出し {#clicks}

1. キャンペーンの`View Report`画面に戻ります。

1. `Clicked`の番号をクリックします。

   ![mailchimp 5](../../../assets/import-mailchimp-5.png)のインポート

1. `Total Clicks`または`Unique Clicks`列の下にある番号のいずれかをクリックします。

   ![mailchimp 6](../../../assets/import-mailchimp-6.png)のインポート

1. **[!UICONTROL Export]**&#x200B;をクリックして、`.csv` ファイルを保存します。

   このファイルには、`Primary Key`、`date (mm/dd/yyyy)`、`campaign name`および`URL`列を追加する必要があります。 完全なURLを追加する必要はなく、クリックされた内容を知らせるだけです。

   ![mailchimp 7](../../../assets/import-mailchimp-7.png)のインポート

1. 電子メールでクリックされたURLごとに手順3と4を繰り返し、完了時にすべてのデータを同じ`.csv` ファイルに結合します。

## 送信したデータの書き出し {#sent}

1. [!DNL Mailchimp]の`Campaigns` タブに移動します。

1. キャンペーン名の横にある「**[!UICONTROL View Report]**」をクリックします。

1. `Recipients`の横にある数字をクリックします。

   ![mailchimp 8](../../../assets/import-mailchimp-8.png)のインポート

1. **[!UICONTROL Export]**&#x200B;をクリックして、`.csv` ファイルを保存します。

   このファイルに`Primary Key`、`date (mm/dd/yyyy)`、`campaign name`列を追加する必要があります。

   ![mailchimp 9](../../../assets/import-mailchimp-9.png)のインポート

## [!DNL Commerce Intelligence]にアップロードするファイルの準備 {#upload}

各ファイル （`Opens`、`Clicks`、`Sent`）は、個別のファイルとして[!DNL Commerce Intelligence]にアップロードする必要があります。 Adobeでは、この命名規則を使用してファイルに名前を付けることをお勧めします：`MailChimp\_ACTION\_DATE`。 `ACTION`を`Open`、`Click`または`Sent`に置き換え、`DATE`を書き出し日に置き換えます。

ファイルをアップロードする準備ができたら、[`File Upload`機能](../connecting-data/using-file-uploader.md)を使用してデータをData Warehouseに取り込みます。
