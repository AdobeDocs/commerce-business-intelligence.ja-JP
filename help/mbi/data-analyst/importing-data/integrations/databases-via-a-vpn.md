---
title: VPN 経由でデータベースに接続
description: SSH トンネルではなく VPN 経由でデータベースに接続する方法を説明します。
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# VPN 経由でデータベースに接続

Adobeでは、 `SSH tunnel`を使用する場合、暗号化された `VPN` 物事を安全に保つための接続。 A `VPN` は、任意のデータベース統合に使用でき、操作を簡単にするために、プロセスは、 `SSH tunnel`:

1. [の作成 [!DNL Commerce Intelligence] データベースユーザー](#database)
1. [の作成 [!DNL Commerce Intelligence] VPN ユーザ](#vpn)
1. [次へのアクセスを許可： [!DNL Commerce Intelligence] IP アドレス](#allowlist)
1. [接続と VPN ユーザ情報を Commerce Intelligence に入力します。](#finish)

データベースの資格情報に加えて、VPN ユーザーが情報をラップするための資格情報を入力する必要があります。 VPN ユーザはすべて機能しますが、Adobeは、 [!DNL Commerce Intelligence] ユーザーを参照してください。ユーザーは、アカウント上でユーザーを簡単に追跡できます。

## 用のデータベースユーザーの作成 [!DNL Commerce Intelligence] {#database}

データベースユーザーを作成するプロセスは、接続するデータベースの種類に応じて異なります。 各データベースタイプの手順を確認するには、以下のリンクをクリックします。

* [Microsoft SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## の作成 `VPN` のユーザー [!DNL Commerce Intelligence] {#vpn}

前述のように、任意の有効な `VPN` ユーザーは機能しますが、Adobeでは、 [!DNL Commerce Intelligence] を使用します。

## 次へのアクセスを許可： [!DNL Commerce Intelligence] IP アドレス {#allowlist}

接続が成功するには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 これらは `54.88.76.97` および `34.250.211.151`ですが、それはまた、 `credentials` 任意のデータベース統合のページ：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 接続の入力と `VPN` ユーザ情報を [!DNL Commerce Intelligence] {#finish}

まとめるには、接続とユーザー情報を次のように入力する必要があります。 [!DNL Commerce Intelligence]. データベースを離れましたか？ `credentials` ページが開いているか？ そうでない場合は、に移動します。 **[!UICONTROL Manage Data** > **Connections]**. クリック **[!UICONTROL Add New Data Source]**&#x200B;をクリックし、接続するデータベースのアイコンをクリックします。 忘れずに `Encrypted` 切り替える `Yes`.

このページに、以下の情報を入力します。 `Database Connection` セクション：

* `Username`：のユーザー名 [!DNL Commerce Intelligence] データベースユーザー
* `Password`：のパスワード [!DNL Commerce Intelligence] データベースユーザー
* `Port`：サーバー上のデータベースのポート。 デフォルトは次のとおりです。
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`：デフォルトでは localhost です。 `127.0.0.1`が含まれますが、サーバーのパブリック IP アドレスまたはローカルエリアネットワークアドレスの場合もあります。
* `Database Name (optional)`:1 つのデータベースへのアクセスのみを許可する場合（データベースユーザーの作成手順で指定）は、ここにそのデータベースの名前を入力します。

の下 `Encryption Connection` セクション：

* `Encryption Type`：これをに設定します。 `Cisco IPsec VPN`
* `Gateway Address`:VPN サーバーの IP アドレス
* `Group Name`：グループ認証に使用するグループの名前
* `Group Secret`：グループに対応するパスワード。
* `Username`: [!DNL Commerce Intelligence] `VPN` ユーザー名
* `Password`: [!DNL Commerce Intelligence] `VPN` ユーザーのパスワード

完了したら、「 **[!UICONTROL Save & Test]** をクリックして設定を完了します。
