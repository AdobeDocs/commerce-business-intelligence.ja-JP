---
title: VPN 経由でデータベースを接続する
description: SSH トンネルではなく VPN を介してデータベースに接続する方法を説明します。
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# VPN 経由でデータベースを接続する

Adobeでは、を使用してデータベースを接続することをお勧めしていますが、 `SSH tunnel`暗号化されたを使用することもできます `VPN` 安全を保つための接続。 A `VPN` を任意のデータベース統合に使用できます。また、処理を簡単にするために、 `SSH tunnel`:

1. [を作成 [!DNL Commerce Intelligence] データベースユーザー](#database)
1. [を作成 [!DNL Commerce Intelligence] VPN ユーザー](#vpn)
1. [へのアクセスを許可 [!DNL Commerce Intelligence] IP アドレス](#allowlist)
1. [接続と VPN ユーザー情報をCommerce Intelligence に入力します。](#finish)

データベースの資格情報に加えて、VPN ユーザーの資格情報を入力して内容を確認する必要があります。 どの VPN ユーザーでも機能しますが、Adobeでは [!DNL Commerce Intelligence] ユーザー（アカウントのユーザーを追跡しやすくするため）

## のデータベースユーザーの作成 [!DNL Commerce Intelligence] {#database}

データベースユーザーを作成するプロセスは、接続するデータベースのタイプによって異なります。 各データベースのタイプの手順を確認するには、以下のリンクをクリックしてください。

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## の作成 `VPN` のユーザー [!DNL Commerce Intelligence] {#vpn}

前述のように、すべて有効 `VPN` ユーザーは機能しますが、Adobeでは以下のみを目的としてユーザーを作成することをお勧めします [!DNL Commerce Intelligence] を使用します。

## へのアクセスを許可 [!DNL Commerce Intelligence] IP アドレス {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 次のとおりです `54.88.76.97` および `34.250.211.151`ただし、そのページは `credentials` 任意のデータベース統合のページ：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 接続の開始および `VPN` ユーザー情報の送信先 [!DNL Commerce Intelligence] {#finish}

最後に、接続とユーザー情報をに入力する必要があります。 [!DNL Commerce Intelligence]. データベースから移動したか `credentials` ページを開きますか？ そうでない場合は、に移動します **[!UICONTROL Manage Data** > **Connections]**. クリック **[!UICONTROL Add New Data Source]**&#x200B;接続するデータベースのアイコンをクリックします。 を変更することを忘れないでください `Encrypted` 切り替え `Yes`.

このページに以下の情報を入力します。まず、 `Database Connection` セクション：

* `Username`：のユーザー名 [!DNL Commerce Intelligence] データベースユーザー
* `Password`：のパスワード [!DNL Commerce Intelligence] データベースユーザー
* `Port`：サーバー上のデータベースのポート。 デフォルト：
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`：デフォルトでは、localhost です `127.0.0.1`ただし、サーバーのパブリック IP アドレスやローカルエリアネットワークアドレスの場合もあります。
* `Database Name (optional)`:1 つのデータベースへのアクセスのみを許可した場合は（これはデータベースユーザーの作成手順で指定します）、そのデータベースの名前をここに入力します。

の下 `Encryption Connection` セクション：

* `Encryption Type`：これをに設定 `Cisco IPsec VPN`
* `Gateway Address`:VPN サーバーの IP アドレス
* `Group Name`：グループ認証に使用されるグループの名前
* `Group Secret`：グループに対応するパスワード。
* `Username`：です [!DNL Commerce Intelligence] `VPN` ユーザー名
* `Password`：です [!DNL Commerce Intelligence] `VPN` ユーザーパスワード

完了したら、 **[!UICONTROL Save & Test]** をクリックして設定を完了します。
