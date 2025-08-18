---
title: Connect Microsoft SQL Server
description: Microsoft SQL データベースをに 4 つの手順で接続  [!DNL Commerce Intelligence]  る方法を説明します。
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# サーバー [!DNL Microsoft SQL] 接続

>[!NOTE]
>
>[ 管理者権限 ](../../../administrator/user-management/user-management.md) が必要です。

![](../../../assets/MicrosoftSQLServer-logo.png)

このトピックでは、[!DNL Microsoft SQL] データベースを [!DNL Commerce Intelligence] に接続する方法を 4 段階で説明します。 このプロセスには、サーバー接続と SQL に関連する技術的な専門知識が必要であり、チームの開発者のサポートが必要になる場合があります。

[!DNL Commerce Intelligence] は、[!DNL Amazon RDS]、[!DNL EC2]、[!DNL Microsoft SQL Azure] およびその他のほとんどのクラウドサーバープロバイダーをサポートしています。 特定のホストに関するご質問については、[ サポートチケットを送信 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)、この情報の提供をアドビに依頼してください。

システムは、データベースに対して SELECT クエリを実行する必要があります。 この処理は、最初はデータベース構造のスナップショットを取得するために行われ、その後、定期的に残業してデータを最新の状態に保ちます。 更新は増分更新なので、Adobeでは、更新の頻度と時間を制限して、サーバーに不要な負荷がかかるのを防ぎます。

これを行う最善の方法は、TCP/IP 経由でデータベースサーバーに接続することです。 SELECT クエリのみを実行できるユーザーを作成します（オプションで、指定したテーブルからのみデータを選択できます）。 これは、[!DNL Commerce Intelligence] に接続している各サーバーについて行う必要があります。

## `Microsoft SQL` を [!DNL Commerce Intelligence] に接続しています：

1. TCP/IP および混合モード認証での接続がサーバーで許可されていることを確認してください。

1. ファイアウォールで、サーバーの専用 IP 接続が許可されていることを確認してください。

   サーバーへの接続に使用する IP アドレスは、`Settings` ページの「接続」セクションで確認できます。

1. データベースサーバーへのログインに使用するユーザーを作成します。 `UI` または `query` を使用する 2 つのオプションがあります。
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) （2 番目の例）

1. [!DNL Commerce Intelligence] の下の **[!UICONTROL Manage Data** > **Connections]** に、サーバーの IP アドレス、ユーザー名およびパスワードを入力します。

   ![](../../../assets/manage-data-connections.png)

1. 「**[!UICONTROL Add a Data Source]**」をクリックします。

1. `Microsoft SQL` データベースに接続し、新しい `Connections` ページのフィールドに資格情報を入力する場合に選択します。

   `Windows Azure` を使用している場合は、データベース名も指定する必要があります。
