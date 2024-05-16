---
title: データの接続
description: Data Warehouseマネージャーで同期に使用できるテーブルを参照する方法を説明します。
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# データの接続

対象： [!DNL Adobe Commerce Intelligence]の場合、データソースは次のように呼ばれます `integrations`. 後 `integration` が正常に接続されました。Data Warehouseマネージャーで同期に使用できるテーブルを参照できます。

統合は、を使用して追加および管理されます `Connections` ページ（クリックするとアクセスできます） **[!UICONTROL Manage Data** > **Connections]**. ここでは、次のようになります。

* アカウントに接続されているすべての統合のリスト

* 統合タイプ

* ステータス （[!DNL Google Analytics] および [!DNL Data Import API] 接続に空白のステータスフィールドがある）

* 最後の接続テスト （`Last Connection Started` 列）が実行されました

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## 統合のタイプ

データをに送信する方法は 4 つあります [!DNL Commerce Intelligence]：データベースへの接続、SaaS 統合への接続、のアップロード `.csv` ファイルを開くか、AdobeAPI を使用します。

## データベースの統合

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] 次のような SQL ベースおよび NoSQL データベースをサポート [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [MICROSOFT SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md)、および [PostgreSQL](../integrations/postgresql.md).

データベースをに直接接続できる間 [!DNL Commerce Intelligence] Adobeでは、データベース資格情報を使用して、SSH トンネルなどの実証済みの暗号化方式を使用することをお勧めします。 これにより、データがData Warehouseに取り込まれる際に、データの安全が確保されます。

接続方法とデータベースの種類によっては、設定を完了するために技術的な専門知識が必要になる場合があります。

## `SaaS` 統合

![](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS` 統合は、次のようなサービスです [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md)、および [[!DNL Zendesk]](../integrations/zendesk.md). サードパーティのデータはベンダーのサーバー上に存在するので、データベース内のデータを使用する場合とは異なり、直接アクセスすることはできません。

通常は、での統合の設定 [!DNL Commerce Intelligence] は、アカウントの資格情報を入力するのと同じくらい簡単です。 一部のサービスでは、認証を完了するために API キーが必要になる場合があります。 を確認してください。 [統合セクション](../integrations/integrations.md) 必要な認証情報の生成手順については、を参照してください。

## ファイルのアップロード

補足ソースからData Warehouseにデータを取り込む方法がわからない場合は、 [使用， `File Upload` 機能](../connecting-data/using-file-uploader.md) は、日常の意思決定に必要のないデータを取り込むための優れた方法です。 書式設定ルールに従って、すばやくアップロードできます `.csv` ファイルをData Warehouseに取り込み、他のデータソースと結合する。

## [!DNL Commerce Intelligence] `Import API`

独自のソースの 1 つからデータを自動的に取得する場合は、 [!DNL Commerce Intelligence] `Import API`. 基本的に、データベースまたは `SaaS` 統合、 `Import API` 機能が最善の策です。

この API を使用するには、少し技術的な専門知識が必要です。小さな Ruby や PHP のスクリプトを書いたり管理したりすることに慣れている人は、資格を超えています。

を使い始める方法の詳細 `Import API`を確認してください。 [開発者サイト](https://developer.adobe.com/commerce/services/reporting/) および [api キーの生成方法](https://developer.adobe.com/commerce/services/reporting/import-api/).

## 統合の追加

統合を追加するには、をクリックします **[!UICONTROL Manage Data** > **Connections]** 次に、をクリックします **[!UICONTROL Add a New Data Source]**. 追加する統合のアイコンをクリックし、ヘルプトピックの指示に従って設定します。

* [統合に関するよくある質問](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [利用可能 ](../integrations/integrations.md)
* [テーブルの統合](../../../best-practices/consolidating-your-tables.md)
* [データベースへのアクセスの制限](../../../administrator/account-management/restrict-db-access.md)

**必要な統合が表示されない場合は、** アカウントに表示されるようにするには、いくつかの統合をアクティベートする必要があります。 次のようなものを探している場合： [!DNL Facebook] ただし、この一覧には記載されていません。 [サポートチケットを送信](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

**統合のエラーステータスが表示される場合**&#x200B;を確認してください。 [トラブルシューティング節](https://support.magento.com/hc/en-us/sections/360003078151) ヘルプを参照してください。
