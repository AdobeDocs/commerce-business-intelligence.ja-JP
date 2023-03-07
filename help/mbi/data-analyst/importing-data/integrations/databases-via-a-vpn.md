---
title: VPN 経由でデータベースに接続
description: SSH トンネルではなく VPN 経由でデータベースに接続する方法を説明します。
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# VPN 経由でデータベースに接続

Adobeでは、SSH トンネルを使用してデータベースに接続することを推奨しますが、暗号化された VPN 接続を使用して、セキュリティを確保することもできます。 A `VPN` は、任意のデータベース統合に使用でき、操作を簡単にするために、プロセスは `SSH tunnel`:

1. [の作成 [!DNL MBI] データベースユーザ](#database)
1. [の作成 [!DNL MBI] VPN ユーザ](#vpn)
1. [次へのアクセスを許可： [!DNL MBI] IP アドレス](#allowlist)
1. [MBI に接続と VPN ユーザー情報を入力します](#finish)

データベースの資格情報に加えて、VPN ユーザーが情報をラップするための資格情報を入力する必要があります。 VPN ユーザはすべて機能しますが、Adobeは、 [!DNL MBI] ユーザー — アカウントでのユーザーの追跡が容易になります。

## 用のデータベースユーザーの作成 [!DNL MBI] {#database}

データベースユーザーを作成するプロセスは、接続するデータベースの種類に応じて異なります。 各データベースタイプの手順を確認するには、以下のリンクをクリックします。

* [Microsoft](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## の作成 `VPN` のユーザー [!DNL MBI] {#vpn}

前述のように、任意の有効な `VPN` ユーザーは機能しますが、Adobeでは、 [!DNL MBI] を使用します。

## 次へのアクセスを許可： [!DNL MBI] IP アドレス {#allowlist}

接続が成功するには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 これらは `54.88.76.97` および `34.250.211.151`ですが、それはまた、 `credentials` 任意のデータベース統合のページ：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 接続の入力と `VPN` ユーザ情報を [!DNL MBI] {#finish}

まとめるには、接続とユーザー情報を次のように入力する必要があります。 [!DNL MBI]. データベースを離れましたか？ `credentials` ページが開いているか そうでない場合は、に移動します。 **[!UICONTROL Manage Data** > **Connections]** をクリックし、 **[!UICONTROL Add New Data Source]**&#x200B;をクリックし、次に、接続するデータベースのアイコンをクリックします。 忘れずに `Encrypted` 切り替える `Yes`.

このページに、以下の情報を入力します。 `Database Connection` セクション：

* `Username`:のユーザー名 [!DNL MBI] データベースユーザ
* `Password`:のパスワード [!DNL MBI] データベースユーザ
* `Port`:サーバー上のデータベースのポート。 デフォルトは次のとおりです。
* `MicrosoftSQL`: `1433`
* `MongoDB`: `27017`
* `MySQL`: `3306`
* `PostgreSQL`: `5432`
* `Host`:デフォルトでは localhost です。 `127.0.0.1`が含まれますが、サーバーのパブリック IP アドレスまたはローカルエリアネットワークアドレスの場合もあります。
* `Database Name (optional)`:1 つのデータベースへのアクセスのみを許可する場合は（これはデータベースユーザーの作成手順で指定します）、ここにそのデータベースの名前を入力します。

以下 `Encryption Connection` セクション：

* `Encryption Type`:これを `Cisco IPsec VPN`
* `Gateway Address`:VPN サーバーの IP アドレス
* `Group Name`:グループ認証に使用するグループの名前
* `Group Secret`:グループに対応するパスワード。
* `Username`:この [!DNL MBI] `VPN` ユーザー名
* `Password`:この [!DNL MBI] `VPN` ユーザーのパスワード

それだ！ 完了したら、「 **[!UICONTROL Save & Test]** をクリックして設定を完了します。
