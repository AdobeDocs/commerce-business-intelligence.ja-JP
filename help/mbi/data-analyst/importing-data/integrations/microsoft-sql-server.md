---
title: Microsoft&reg;&reg；を接続SQL Server
description: Microsoft&reg；の接続方法を学ぶSQL データベースの宛先 [!DNL MBI] 4 段階のプロセスで
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Microsoft® SQL Server に接続

>[!NOTE]
>
>必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

この記事では、 `Microsoft SQL` データベースへ [!DNL MBI] 4 段階のプロセスで このプロセスには、サーバー接続と SQL に関する技術的な専門知識が必要です。また、チームの開発者のサポートが必要になる場合があります。

MBI サポート [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft®; SQL Azure]、およびその他のほとんどのクラウドサーバープロバイダー。 特定のホストに関する質問がある場合は、 [サポートチケットを提出する](../../../guide-overview.md) この情報を提供して欲しいと頼む

システムは、データベースに対して SELECT クエリを実行する必要があります。 最初は、データベース構造のスナップショットを取得し、データを最新の状態に保つために定期的に時間がかかります。 更新は増分で、Adobeは更新の頻度と時間を制限して、サーバーへの不要な負荷を防ぎます。

これを行う最善の方法は、TCP/IP 経由でデータベースサーバに接続することです。 SELECT クエリのみを実行できるユーザーを作成します（また、オプションで、指定したテーブルからのデータのみを選択できます）。 これは、接続先の各サーバに対して実行する必要があります [!DNL MBI].

## 接続中 `Microsoft SQL` から [!DNL MBI]:

1. サーバーで、TCP/IP と混合モード認証を介した接続が許可されていることを確認します。

1. ファイアウォールで、サーバーの専用 IP が接続できることを確認します。

   サーバーへの接続に使用される IP アドレスは、 `Settings` ページ。

1. データベースサーバーへのログインに使用するユーザーを作成します。 2 つの選択肢があります。次のいずれか `UI` または経由 `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) （2 番目の例）

1. サーバーの IP アドレス、ユーザー名、パスワードを [!DNL MBI] under **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. クリック **[!UICONTROL Add a Data Source]**.

1. 選択して `Microsoft SQL` データベースにログインし、新しい `Connections` ページ。

   次を使用する場合： `Windows Azure`に値を指定する場合は、データベース名も指定する必要があります。
