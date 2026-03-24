---
title: Connect Microsoft SQL Server
description: 4段階のプロセスで、Microsoft SQL データベースを [!DNL Commerce Intelligence] に接続する方法について説明します。
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
TQID: https://experienceleague.adobe.com/mJFBPJE334m7V8klJk-1xKAfsU4u4ObcwWDZzylJohM
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 306
ht-degree: 0%

---

# [!DNL Microsoft SQL] サーバーを接続

>[!NOTE]
>
>[管理者権限](../../../administrator/user-management/user-management.md)が必要です。

![Microsoft SQL Server ロゴ &#x200B;](../../../assets/MicrosoftSQLServer-logo.png)

このトピックでは、4段階のプロセスで[!DNL Microsoft SQL] データベースを[!DNL Commerce Intelligence]に接続する方法について説明します。 このプロセスには、サーバー接続とSQLに関する技術的な専門知識が必要であり、チームの開発者のサポートが必要になる場合があります。

[!DNL Commerce Intelligence]は、[!DNL Amazon RDS]、[!DNL EC2]、[!DNL Microsoft SQL Azure]およびその他のほとんどのクラウドサーバープロバイダーをサポートしています。 特定のホストに関する質問がある場合は、[&#x200B; サポートチケット &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)を送信して、この情報の提供を依頼してください。

システムは、データベースでSELECT クエリを実行する必要があります。 これは最初にデータベース構造のスナップショットを取得するために行われ、次にデータを最新の状態に保つために定期的に超過時間が発生します。 アップデートは段階的に行われ、Adobeはアップデートの頻度と時間を制限して、サーバーへの不要な負荷を防ぎます。

これを行う最善の方法は、TCP/IP経由でデータベースサーバーに接続することです。 SELECT クエリのみを実行できるユーザーを作成します（オプションで、指定したテーブルからのみデータを選択できます）。 これは、[!DNL Commerce Intelligence]に接続している各サーバーに対して実行する必要があります。

## `Microsoft SQL`を[!DNL Commerce Intelligence]に接続中：

1. サーバーがTCP/IPおよび混合モード認証を介した接続を許可していることを確認してください。

1. ファイアウォールで、サーバーの専用IPが接続できることを確認します。

   サーバーへの接続に使用されるIP アドレスは、`Settings` ページの「接続」セクションにあります。

1. データベースサーバーにログインするユーザーを作成します。 `UI`または`query`のいずれかを使用して2つのオプションがあります。
   * `UI`
   * `Query`

1. [!DNL Commerce Intelligence]の&#x200B;**[!UICONTROL Manage Data** > **Connections]**&#x200B;にサーバーのIP アドレス、ユーザー名、パスワードを入力します。

   ![&#x200B; データベース統合を表示するデータ接続の管理ページ &#x200B;](../../../assets/manage-data-connections.png)

1. **[!UICONTROL Add a Data Source]**&#x200B;をクリックします。

1. 選択して`Microsoft SQL` データベースを接続し、新しい`Connections` ページのフィールドに資格情報を入力します。

   `Windows Azure`を使用している場合は、データベース名も指定する必要があります。
