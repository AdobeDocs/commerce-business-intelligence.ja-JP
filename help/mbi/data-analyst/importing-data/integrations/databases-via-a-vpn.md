---
title: VPN経由でデータベースを接続する
description: SSH トンネルではなくVPN経由でデータベースを接続する方法を説明します。
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/0B7swwGIgBemitnx8Q4tyN8VtqwzcA-DYZdXHqzyNAk
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: efc8727dd67a9ffcd7a8a1059ea93df8c6344599
workflow-type: tm+mt
source-wordcount: 414
ht-degree: 0%

---

# VPN経由でデータベースを接続する

Adobeでは、`SSH tunnel`を使用してデータベースを接続することをお勧めしますが、暗号化された`VPN`接続を使用してセキュリティを維持することもできます。 SSH ホスト キーの登録、エラー、SSH トンネル接続に関するトラブルシューティングについては、[SSH ホスト キーの検証](ssh-host-key-verification.md)を参照してください。 `VPN`は、任意のデータベース統合に使用できます。また、物事をシンプルに保つために、プロセスは`SSH tunnel`を設定するのとほぼ同じです。

1. [&#x200B; [!DNL Commerce Intelligence]  データベースユーザーの作成](#database)
1. [&#x200B; [!DNL Commerce Intelligence] VPN ユーザーの作成](#vpn)
1. [&#x200B; [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可](#allowlist)
1. [Commerce Intelligenceに接続とVPN ユーザー情報を入力します](#finish)

データベースの資格情報に加えて、VPN ユーザーの資格情報を入力して処理を終了する必要があります。 どのVPN ユーザーでも機能しますが、Adobeでは、アカウントのユーザーを簡単に追跡できるため、[!DNL Commerce Intelligence] ユーザーを作成することをお勧めします。

## [!DNL Commerce Intelligence]のデータベース ユーザーを作成しています {#database}

データベースユーザーを作成するプロセスは、接続するデータベースの種類によって異なります。 各データベースタイプの手順を確認するには、以下のリンクをクリックします。

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## [!DNL Commerce Intelligence]の`VPN` ユーザーを作成しています {#vpn}

前述のように、有効な`VPN` ユーザーは機能しますが、[!DNL Commerce Intelligence]の使用のみを目的としたユーザーの作成をAdobeで推奨します。

## [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可 {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 `54.88.76.97`と`34.250.211.151`ですが、データベース統合の`credentials` ページにも表示されます。

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## 接続と`VPN` ユーザー情報を[!DNL Commerce Intelligence]に入力しています {#finish}

最後に、接続とユーザー情報を[!DNL Commerce Intelligence]に入力する必要があります。 データベース `credentials` ページを開いたままにしましたか？ そうでない場合は、**[!UICONTROL Manage Data** > **Connections]**&#x200B;に移動します。 **[!UICONTROL Add New Data Source]**&#x200B;をクリックし、接続しているデータベースのアイコンをクリックします。 `Encrypted` トグルを`Yes`に変更することを忘れないでください。

`Database Connection` セクションから始めて、このページに次の情報を入力します。

* `Username`: [!DNL Commerce Intelligence] データベースユーザーのユーザー名
* `Password`: [!DNL Commerce Intelligence] データベースユーザーのパスワード
* `Port`: サーバー上のデータベースのポート。 デフォルトは次のとおりです。
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: デフォルトでは、これはlocalhost `127.0.0.1`ですが、サーバーのパブリック IP アドレスまたはローカル エリア ネットワーク アドレスの場合もあります。
* `Database Name (optional)`: 1つのデータベースへのアクセスのみを許可した場合（これはデータベースユーザーの作成手順で指定します）、そのデータベースの名前をここに入力します。

`Encryption Connection` セクションの下：

* `Encryption Type`：これを`Cisco IPsec VPN`に設定
* `Gateway Address`: VPN サーバーのIP アドレス
* `Group Name`: グループ認証に使用されるグループの名前
* `Group Secret`: グループに対応するパスワード。
* `Username`: [!DNL Commerce Intelligence] `VPN` ユーザー名
* `Password`: [!DNL Commerce Intelligence] `VPN` ユーザーパスワード

完了したら、**[!UICONTROL Save & Test]**&#x200B;をクリックして設定を完了します。

