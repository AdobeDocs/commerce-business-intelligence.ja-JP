---
title: Microsoft SQL Server に接続
description: Microsoft SQL データベースをに接続する方法を説明します。 [!DNL MBI] 4 段階のプロセスで
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Microsoft SQL Server に接続

>[!NOTE]
>
>必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

この記事では、 `Microsoft SQL` データベースへ [!DNL MBI] 4 段階のプロセスで このプロセスには、サーバー接続と SQL に関する技術的な専門知識が必要です。また、チームの開発者のサポートが必要になる場合があります。

サポート [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure]、およびその他のほとんどのクラウドサーバープロバイダー。 特定のホストに関する質問がある場合は、 [サポートチケットを提出する](../../../guide-overview.md) この情報を提供して欲しいと頼む

システムは、お使いのデータベースに対して SELECT クエリを実行する必要があります。 最初は、データベース構造のスナップショットを取得し、定期的な時間を経てデータを最新の状態に保ちます。 アップデートは増分です。アドビは、更新の頻度と時間を制限して、サーバーに不要な負荷がかからないようにします。

これを行う最善の方法は、TCP/IP 経由でデータベースサーバに接続することです。 SELECT クエリのみを実行できるユーザーを作成します（また、オプションで、指定したテーブルからのデータのみを選択できます）。 これは、接続先の各サーバーに対して実行する必要があります [!DNL MBI].

## 接続中 `Microsoft SQL` から [!DNL MBI]:

1. サーバーで、TCP/IP と混合モード認証を介した接続が許可されていることを確認します。

1. ファイアウォールで、サーバーの専用 IP が接続できることを確認してください。

   お使いのサーバーに接続するために使用する IP アドレスは、 `Settings` ページ。

1. データベースサーバーへのログインに使用するユーザーを作成します。  2 つの選択肢があります。次のいずれか `UI` または経由 `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) （2 番目の例）

1. サーバーの IP アドレス、ユーザー名、パスワードを [!DNL MBI] under **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. クリック **[!UICONTROL Add a Data Source]**.

1. 選択して `Microsoft SQL` データベースにログインし、新しい `Connections` ページ。

   次を使用する場合： `Windows Azure`に値を指定する場合は、データベース名も指定する必要があります。
