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

Adobeでは、`SSH tunnel` を使用してデータベースを接続することをお勧めしていますが、暗号化された `VPN` 接続を使用して安全を確保することもできます。 `VPN` は、任意のデータベース統合に使用できます。物事を簡単にするために、プロセスは `SSH tunnel` の設定とほぼ同じです。

1. [データベースユーザ  [!DNL Commerce Intelligence]  の作成](#database)
1. [VPN ユーザ  [!DNL Commerce Intelligence]  の作成](#vpn)
1. [ [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可](#allowlist)
1. [Commerce Intelligenceへの接続と VPN ユーザー情報の入力](#finish)

データベースの資格情報に加えて、VPN ユーザーの資格情報を入力して内容を確認する必要があります。 どの VPN ユーザーでも機能しますが、Adobeでは、アカウント上のユーザーを簡単に追跡できるため、[!DNL Commerce Intelligence] ユーザーを作成することをお勧めします。

## [!DNL Commerce Intelligence] 用のデータベースユーザーの作成 {#database}

データベースユーザーを作成するプロセスは、接続するデータベースのタイプによって異なります。 各データベースのタイプの手順を確認するには、以下のリンクをクリックしてください。

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## `VPN` 用の [!DNL Commerce Intelligence] ユーザーの作成 {#vpn}

前述のように、有効な `VPN` ユーザーであれば誰でも機能しますが、Adobeでは、[!DNL Commerce Intelligence] 用のためにのみユーザーを作成することをお勧めします。

## [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可 {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 これらは `54.88.76.97` および `34.250.211.151` ですが、あらゆるデータベース統合に関して `credentials` ページにも表示されます。

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 接続の入力とユーザー情報の `VPN` への [!DNL Commerce Intelligence] 入 {#finish}

まとめるには、接続とユーザー情報を [!DNL Commerce Intelligence] に入力する必要があります。 データベースの `credentials` ページを開いたままにしましたか。 そうでない場合は、**[!UICONTROL Manage Data** > **Connections]** に移動します。 [**[!UICONTROL Add New Data Source]**] をクリックし、接続するデータベースのアイコンをクリックします。 `Encrypted` の切り替えを `Yes` に変更することを忘れないでください。

このページに、`Database Connection` のセクションから始まる次の情報を入力します。

* `Username`:[!DNL Commerce Intelligence] データベースユーザーのユーザー名
* `Password`:[!DNL Commerce Intelligence] データベースユーザーのパスワード
* `Port`: サーバー上のデータベースのポート。 デフォルト：
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: デフォルトでは、これは localhost `127.0.0.1` ですが、サーバーのパブリック IP アドレスまたはローカルエリアネットワークアドレスである場合もあります。
* `Database Name (optional)`: 1 つのデータベースへのアクセスのみを許可した場合（これはデータベース・ユーザーの作成ステップで指定されます）、そのデータベースの名前をここに入力します。

「`Encryption Connection`」セクションで、

* `Encryption Type`：これを `Cisco IPsec VPN` に設定
* `Gateway Address`: VPN サーバーの IP アドレス
* `Group Name`: グループ認証に使用されるグループの名前
* `Group Secret`: グループに対応するパスワード。
* `Username`:[!DNL Commerce Intelligence] `VPN` のユーザー名
* `Password`:[!DNL Commerce Intelligence] `VPN` ユーザーパスワード

完了したら、「**[!UICONTROL Save & Test]**」をクリックして設定を完了します。
