---
title: Connect Microsoft SQL Server
description: 4段階のプロセスで、Microsoft SQL データベースを[!DNL Commerce Intelligence]に接続する方法について説明します。
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
TQID: 'https://experienceleague.adobe.com/mJFBPJE334m7V8klJk-1xKAfsU4u4ObcwWDZzylJohM'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
  - id: c38ccf61-5a4f-5140-ad2b-c3434e82ed6d
    internal-label: SQL Report Builder
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%
---
# [!DNL Microsoft SQL] サーバーを接続

>[!NOTE]
>
>[管理者権限](../../../administrator/user-management/user-management.md)が必要です。

![Microsoft SQL Server ロゴ &#x200B;](../../../assets/MicrosoftSQLServer-logo.png)

このトピックでは、4段階のプロセスで[!DNL Microsoft SQL] データベースを[!DNL Commerce Intelligence]に接続する方法について説明します。 このプロセスには、サーバー接続とSQLに関する技術的な専門知識が必要であり、チームの開発者のサポートが必要になる場合があります。

[!DNL Commerce Intelligence]は、[!DNL Amazon RDS]、[!DNL EC2]、[!DNL Microsoft SQL Azure]およびその他のほとんどのクラウドサーバープロバイダーをサポートしています。 特定のホストに関する質問がある場合は、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/ja/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies)を送信して、この情報の提供を依頼してください。

システムは、データベースでSELECT クエリを実行する必要があります。 これは最初にデータベース構造のスナップショットを取得するために行われ、次にデータを最新の状態に保つために定期的に超過時間が発生します。 アップデートは段階的に行われ、Adobeはアップデートの頻度と時間を制限して、サーバーへの不要な負荷を防ぎます。

これを行う最善の方法は、TCP/IP経由でデータベースサーバーに接続することです。 SELECT クエリのみを実行できるユーザーを作成します（オプションで、指定したテーブルからのみデータを選択できます）。 これは、[!DNL Commerce Intelligence]に接続している各サーバーに対して実行する必要があります。

## `Microsoft SQL`を[!DNL Commerce Intelligence]に接続中：

1. サーバーがTCP/IPおよび混合モード認証を介した接続を許可していることを確認してください。

1. ファイアウォールで、サーバーの専用IPが接続できることを確認します。

   サーバーへの接続に使用されるIP アドレスは、`Settings` ページの「接続」セクションにあります。

1. データベースサーバーにログインするユーザーを作成します。 `UI`または`query`のいずれかを使用して2つのオプションがあります。
   * `UI`
   * `Query`

1. **[!UICONTROL Manage Data** > **Connections]**&#x200B;の[!DNL Commerce Intelligence]にサーバーのIP アドレス、ユーザー名、パスワードを入力します。

   ![&#x200B; データベース統合を表示するデータ接続の管理ページ &#x200B;](../../../assets/manage-data-connections.png)

1. **[!UICONTROL Add a Data Source]**&#x200B;をクリックします。

1. 選択して`Microsoft SQL` データベースを接続し、新しい`Connections` ページのフィールドに資格情報を入力します。

   `Windows Azure`を使用している場合は、データベース名も指定する必要があります。
