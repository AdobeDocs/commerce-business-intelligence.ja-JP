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

ま [!DNL Adobe Commerce Intelligence]、データソースは `integrations` と呼ばれます。 `integration` が正常に接続されると、同期に使用できるテーブルをData Warehouseマネージャーで参照できるようになります。

統合の追加や管理には `Connections` ページを使用します。このページにアクセスするには、「**[!UICONTROL Manage Data** > **Connections]**」をクリックします。 ここでは、次のようになります。

* アカウントに接続されているすべての統合のリスト

* 統合タイプ

* ステータス（[!DNL Google Analytics] と [!DNL Data Import API] の接続には、空白のステータスフィールドがあります）

* 最後に接続テストが実行された時刻（`Last Connection Started` 列）

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## 統合のタイプ

データを [!DNL Commerce Intelligence] に取り込む方法は 4 つあります。データベースに接続する、SaaSAdobeに接続する、`.csv` ファイルをアップロードする、統合 API を使用する、です。

## データベースの統合

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL Commerce Intelligence] では、[MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md)、[Microsoft SQL](../integrations/microsoft-sql-server.md) [、&lbrace;MongoDB](../integrations/mongodb-via-ssh-tunnel.md)、&lbrace;PostgreSQL[&#128279;](../integrations/postgresql.md) など、SQL ベースのデータベースと NoSQL データベースをサポ  トしています。

データベース資格情報を使用してデータベースを [!DNL Commerce Intelligence] に直接接続できますが、Adobeでは SSH トンネルなどの実証済みの暗号化方式を使用することをお勧めします。 これにより、データがData Warehouseに取り込まれる際に、データの安全が確保されます。

接続方法とデータベースの種類によっては、設定を完了するために技術的な専門知識が必要になる場合があります。

## `SaaS` 統合

![](../../../assets/SaaS_icons.jpg)spree-commerce-logo.png

`SaaS` の統合は、[[!DNL Google Adwords]](../integrations/google-adwords.md)、[[!DNL Salesforce]](../integrations/salesforce.md)、[[!DNL Zendesk]](../integrations/zendesk.md) などのサービスです。 サードパーティのデータはベンダーのサーバー上に存在するので、データベース内のデータを使用する場合とは異なり、直接アクセスすることはできません。

通常、[!DNL Commerce Intelligence] での統合設定は、アカウントの資格情報を入力するのと同じくらい簡単です。 一部のサービスでは、認証を完了するために API キーが必要になる場合があります。 必要な資格情報の生成手順については、[ 統合の節 ](../integrations/integrations.md) を参照してください。

## ファイルのアップロード

補足ソースからData Warehouseにデータを取り込む方法がわからない場合は、 [`File Upload` 機能の使用 ](../connecting-data/using-file-uploader.md) は、日常の意思決定に必要のないデータを取り込む優れた方法です。 書式設定ルールに従って、`.csv` ファイルをすばやくData Warehouseにアップロードし、他のデータソースと結合できます。

## [!DNL Commerce Intelligence] `Import API`

独自のソースの 1 つからデータを自動的に取得する場合は、[!DNL Commerce Intelligence] `Import API` を使用できます。 基本的に、データベースや `SaaS` 統合にない場合は、`Import API` 関数が最適です。

この API を使用するには、少し技術的な専門知識が必要です。小さな Ruby や PHP のスクリプトを書いたり管理したりすることに慣れている人は、資格を超えています。

`Import API` の使用を開始する方法について詳しくは、[ 開発者サイト ](https://developer.adobe.com/commerce/services/reporting/) および [API キーの生成方法 ](https://developer.adobe.com/commerce/services/reporting/import-api/) を参照してください。

## 統合の追加

統合を追加するには、「**[!UICONTROL Manage Data** > **Connections]**」をクリックし、「**[!UICONTROL Add a New Data Source]**」をクリックします。 追加する統合のアイコンをクリックし、ヘルプトピックの指示に従って設定します。

* [ 統合に関する FAQ](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [利用可能 ](../integrations/integrations.md)
* [テーブルの統合](../../../best-practices/consolidating-your-tables.md)
* [データベースへのアクセスの制限](../../../administrator/account-management/restrict-db-access.md)

**必要な統合が表示されない場合は、** アカウントに表示されるようにするには、いくつかの統合をアクティベートする必要があります。 [!DNL Facebook] のようなものを探しているがリストに表示されない場合は、[ サポートチケットを送信 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) してください。

**統合のエラーステータスが表示された場合**、[ トラブルシューティングの節 ](https://support.magento.com/hc/en-us/sections/360003078151) のヘルプを参照してください。
