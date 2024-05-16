---
title: Connect Microsoft SQL Server
description: Microsoft SQL データベースをに接続する方法について説明します [!DNL Commerce Intelligence] 4 段階のプロセスで行います。
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 接続 [!DNL Microsoft SQL] サーバー

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

このトピックでは、を接続する方法について説明します [!DNL Microsoft SQL] データベース先 [!DNL Commerce Intelligence] 4 段階のプロセスで行います。 このプロセスには、サーバー接続と SQL に関連する技術的な専門知識が必要であり、チームの開発者のサポートが必要になる場合があります。

[!DNL Commerce Intelligence] のサポート [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure]、およびその他のほとんどのクラウドサーバープロバイダー。 特定のホストについて質問がある場合は、 [サポートチケットを送信](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) お問い合わせ。

システムは、データベースに対して SELECT クエリを実行する必要があります。 この処理は、最初はデータベース構造のスナップショットを取得するために行われ、その後、定期的に残業してデータを最新の状態に保ちます。 更新は増分更新なので、Adobeでは、更新の頻度と時間を制限して、サーバーに不要な負荷がかかるのを防ぎます。

これを行う最善の方法は、TCP/IP 経由でデータベースサーバーに接続することです。 SELECT クエリのみを実行できるユーザーを作成します（オプションで、指定したテーブルからのみデータを選択できます）。 これは、接続先の各サーバーについて行う必要があります [!DNL Commerce Intelligence].

## 接続中 `Microsoft SQL` 対象： [!DNL Commerce Intelligence]:

1. TCP/IP および混合モード認証での接続がサーバーで許可されていることを確認してください。

1. ファイアウォールで、サーバーの専用 IP 接続が許可されていることを確認してください。

   サーバーへの接続に使用する IP アドレスは、の「接続」セクションにあります `Settings` ページ。

1. データベースサーバーへのログインに使用するユーザーを作成します。 次の 2 つのオプションがあります。どちらか一方を使用します `UI` または経由 `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) （2 番目の例）

1. サーバーの IP アドレス、ユーザー名およびパスワードをに入力します。 [!DNL Commerce Intelligence] 未満 **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. クリック **[!UICONTROL Add a Data Source]**.

1. を選択してを接続します `Microsoft SQL` データベースに移動し、新しいフィールドに資格情報を入力します。 `Connections` ページ。

   を使用している場合 `Windows Azure`データベース名も指定する必要があります。
