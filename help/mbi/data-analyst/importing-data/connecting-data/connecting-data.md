---
title: データを接続
description: 同期マネージャーで同期可能なテーブルを参照するData Warehouseを説明します。
exl-id: 94beba8b-6a86-4af9-87fb-96b1cf8f8fa2
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '543'
ht-degree: 0%

---

# データを接続

In [!DNL MBI]、データソース `integrations`. 次の後： `integration` が正常に接続されたので、同期に使用できるテーブルをData Warehouseマネージャーで参照できます。

統合は、 `Connections` ページ（クリックするとアクセス可能） **[!UICONTROL Manage Data** > **Connections]**. ここで、
* アカウントに関連するすべての統合のリスト
* 統合タイプ
* ステータス ([!DNL Google Analytics] および [!DNL Data Import API] 接続には空のステータスフィールドがあります )
* 最後に接続テストを行った時刻 (`Last Connection` 「開始」列 ) が実行されました

![Data\_Sources\_Table.png](../../../assets/Data_Sources_Table.png)

## 統合のタイプ

データをに取り込む方法は 4 つあります。 [!DNL MBI]:データベースの接続、SaaS 統合の接続、 `.csv` ファイルに書き込むか、AdobeAPI を使用します。

## データベースの統合

![Database\_icons.jpg](../../../assets/Database_icons.jpg)

[!DNL MBI] は、次のような SQL ベースおよび NoSQL データベースをサポートします。 [MySQL](../../importing-data/integrations/mysql-via-ssh-tunnel.md), [Microsoft® SQL](../integrations/microsoft-sql-server.md), [MongoDB](../integrations/mongodb-via-ssh-tunnel.md)、および [PostgreSQL](../integrations/postgresql.md).

データベースを [!DNL MBI] Adobeでは、データベース資格情報を使用して、SSH トンネルなどの実証済みの暗号化方法を使用することをお勧めします。 これにより、データがData Warehouseに入り込む際に、安全で安全な状態を維持できます。

接続方法とデータベースの種類に応じて、設定を完了するには一部の技術的な専門知識が必要になる場合があります。

## `SaaS` 統合

![](../../../assets/SaaS_icons.jpg)

`SaaS` 統合は、 [[!DNL Google Adwords]](../integrations/google-adwords.md), [[!DNL Salesforce]](../integrations/salesforce.md)、および [[!DNL Zendesk]](../integrations/zendesk.md). サードパーティのデータはベンダーのサーバー上に存在するので、データベース内のデータと同様に直接アクセスすることはできません。

通常、 [!DNL MBI] は、単にアカウントの資格情報を入力するだけで簡単にできます。 一部のサービスでは、認証を完了するために API キーが必要になる場合があります。詳しくは、 [統合セクション](../integrations/integrations.md) 必要な資格情報の生成手順については、を参照してください。

## ファイルのアップロード

補足的なソースからData Warehouseにデータを取得する方法が不明な場合は、 [の使用 `File Upload` 機能](../connecting-data/using-file-uploader.md) は、日常的な意思決定に必要としないデータを取り込む良い方法です。 書式設定ルールに従って、すばやくアップロードできます `.csv` ファイルをData Warehouseに追加し、他のデータソースと結合します。

## [!DNL MBI] `Import API`

独自のソースからのデータ取得を自動化する場合は、 [!DNL MBI] `Import API`. 基本的には、データベースまたは `SaaS` 統合、 `Import API` 関数は最高の賭けです。

API を使用するには、多くの技術的な専門知識が必要です。小さな Ruby または PHP スクリプトを記述し、管理することに慣れている人は、資格を持つ以上の人です。

の使用を開始する方法について詳しくは、以下を参照してください。 `Import API`、 [開発者サイト](https://developer.adobe.com/commerce/services/reporting/) および [API キーの生成方法](https://developer.adobe.com/commerce/services/reporting/import-api/).

## 統合の追加

統合を追加するには、 **[!UICONTROL Manage Data** > **Connections]** 次に、 **[!UICONTROL Add a New Data Source]**. 追加する統合のアイコンをクリックし、ヘルプ記事の手順に従って設定します。

* [統合に関する FAQ](https://support.magento.com/hc/en-us/sections/360003161871-Integration-FAQ)
* [利用可能 ](../integrations/integrations.md)
* [テーブルの統合](../../../best-practices/consolidating-your-tables.md)
* [データベースへのアクセスの制限](../../../administrator/account-management/restrict-db-access.md)

**目的の統合が表示されていない場合は、** 一部の統合は、アカウントで表示できるように、アクティブ化する必要があります。 例えば、 [!DNL Facebook]  — が、リストには表示されていない。 [サポートチケットを提出する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

**統合のエラーステータスが表示される場合**、パニックに陥らない — [トラブルシューティング節](https://support.magento.com/hc/en-us/sections/360003078151) を参照してください。
