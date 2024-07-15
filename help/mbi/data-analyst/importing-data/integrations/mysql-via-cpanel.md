---
title: cPanel を介した MySQL の接続
description: cPanel を使用して MySQL に接続する方法を説明します。
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# [!DNL cPanel] 経由で [!DNL MySQL] に接続

* [ [!DNL cPanel] での  [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーの作成](#cpanel)
* [接続およびユーザー情報の入力先  [!DNL Commerce Intelligence]](#finish)

## 移動先

* [SSH トンネル経由の [!DNL MySQL]](../integrations/mysql-via-ssh-tunnel.md)
* [直接接続を介した [!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] では、データを保護するために SSH またはその他の形式の暗号化を使用することをお勧めします。 これがオプションでない場合でも、このトピックの手順を使用して、[!DNL Commerce Intelligence] をデータベースに直接接続できます。

このトピックでは、[!DNL cPanel] を使用して [!DNL MySQL] データベースを [!DNL Commerce Intelligence] に直接接続する手順について説明します。 このプロセスは、[!DNL Adobe Commerce] やその他の MySQL ベースの e コマースデータベースを [!DNL Commerce Intelligence] に接続する場合にも使用できます。

1. [!DNL cPanel] での [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーの作成
1. [!DNL Commerce Intelligence] に接続およびユーザー情報を入力

今すぐ始めましょう。

## [!DNL cPanel] での [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーの作成 {#cpanel}

1. ホスティングプロバイダーを通じて [!DNL cPanel] にログインします。
1. 「`Database`」セクションの「**[!UICONTROL [!DNL MySQL] Databases]**」をクリックします。
1. `Add New User` のセクションまでスクロールし、[!DNL Commerce Intelligence] のユーザーを作成します。

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. 「**[!UICONTROL Create User]**」をクリックします。
1. ユーザーを作成したので、次はデータベースに関連付ける必要があります。 `Add New User` のセクションに戻ります – `Add User to Database?` の設定を参照してくださいそれが必要なものです。
1. このセクションの `User` ドロップダウンで、作成したユーザーを選択します。
1. このセクションの `Database` ドロップダウンで、[!DNL Commerce Intelligence] に接続するデータベースを選択します。
1. 「**[!UICONTROL Add]**」をクリックします。
1. 権限のチェックリストが表示されたら、「`SELECT`」の横にあるチェックボックスをオンにします。これだけで、データベースに接続 [!DNL Commerce Intelligence] る必要があります。

## [!DNL Commerce Intelligence] への接続およびユーザー情報の入力 {#finish}

まとめるには、接続とユーザー情報を [!DNL Commerce Intelligence] に入力する必要があります。 [!DNL MySQL] 資格情報ページを開いたままにしましたか？ そうでない場合は、**[!UICONTROL Manage Data** > **Connections]** に移動して「**[!UICONTROL Add New Data Source]**」をクリックし、次に「[!DNL MySQL]」アイコンをクリックします。

このページの「`Database Connection`」セクションに、次の情報を入力します。

* `Username`:[!DNL Commerce Intelligence] [!DNL MySQL] ユーザーのユーザー名
* `Password`:[!DNL Commerce Intelligence] [!DNL MySQL] ユーザーのパスワード
* `Port`: サーバー上の MySQL のポート （デフォルトでは `3306`）
* `Host`：接続先の `MySQL` サーバーのパブリック アドレス [!DNL Commerce Intelligence] す。 これは、通常、`[!DNL cPanel]` へのログインに使用する URL です。

[`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md) を使用している場合は、暗号化情報を入力する必要があります。 フォームを表示するには、「`Encrypted`」切替スイッチを「`Yes`」に設定します。

* `Connection Type`：これを `SSH Tunnel` に設定
* `Remote Address`: トンネル先のサーバー [!DNL Commerce Intelligence] の IP アドレスまたはホスト名
* `Username`:[!DNL Commerce Intelligence] `SSH (Linux)` ユーザーのユーザー名。[ 手順 ](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) まだの場合は、その方法）を参照してください
* `SSH Port`：サーバーの SSH ポート（デフォルトでは `22`）

完了したら、「**[!UICONTROL Save & Test]**」をクリックして設定を完了します。

## 関連：

* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
