---
title: SSH トンネル経由  [!DNL MySQL]  接続
description: SSH トンネル経由で接続する方法  [!DNL MySQL]  説明します。
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# [!DNL MySQL] 経由で [!DNL SSH Tunnel] に接続

* [&#x200B; [!DNL Commerce Intelligence]  公開鍵の取得](#retrieve)
* [&#x200B; [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可](#allowlist)
* [Linux ユーザーを作成する  [!DNL Commerce Intelligence]](#linux)
* [&#x200B; [!DNL MySQL]  のユ  [!DNL Commerce Intelligence] ザーを作成](#mysql)
* [接続およびユーザー情報の入力先  [!DNL Commerce Intelligence]](#finish)

## ジャンプ

* [[!DNL MySQL] via &#x200B;](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

[!DNL MySQL] を使用して [!DNL Commerce Intelligence] データベースを `SSH tunnel` に接続するには、次の操作を行う必要があります。

1. [!DNL Commerce Intelligence] `public key` の取得
1. [!DNL Commerce Intelligence] `IP address` へのアクセスを許可
1. `Linux` の [!DNL Commerce Intelligence] ユーザーの作成
1. `MySQL` の [!DNL Commerce Intelligence] ユーザーの作成
1. [!DNL Commerce Intelligence] に接続およびユーザー情報を入力


## [!DNL Commerce Intelligence] 公開鍵の取得 {#retrieve}

`public key` は、[!DNL Commerce Intelligence] `Linux` ユーザーの認証に使用されます。 次の節では、ユーザーを作成してキーを読み込みます。

1. **[!UICONTROL Manage Data** > **Connections]** に移動し、「**[!UICONTROL Add New Data Source]**」をクリックします。
1. `MySQL` アイコンをクリックします。
1. `MySQL credentials` ページが開いたら、「`Encrypted`」切り替えスイッチを「`Yes`」に設定します。 SSH 設定フォームが表示されます。
1. `public key` はこのフォームの下にあります。

このページは、チュートリアルの最後まで開いたままにしておきます。次の節と最後に必要になります。

[!DNL Commerce Intelligence] 内を移動してキーを取得する方法を次に示します。

![SSH トンネルを介した MySQL 接続のアニメーションによるデモ &#x200B;](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可します {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 それらは `54.88.76.97` と `34.250.211.151` ですが、`MySQL credentials` のページにもあります。 上記のGIFの青いボックスを参照してください。

## [!DNL Linux] 用の [!DNL Commerce Intelligence] ユーザーの作成 {#linux}

リアルタイム（または頻繁に更新される）のデータが含まれている限り、実稼動マシンまたはセカンダリマシンを使用できます。 [&#x200B; サーバーへの接続権が保持されている限り、好きなように &#x200B;](../../../administrator/account-management/restrict-db-access.md) このユーザーを制限 `MySQL` することができます。

1. 新しいユーザーを追加するには、[!DNL Linux] サーバーで次のコマンドを root として実行します。

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 最初のセクションで取得した `public key` を覚えていますか？ ユーザーがデータベースにアクセスできるようにするには、キーを `authorized\_keys` に読み込む必要があります。

   次のように、キー全体を `authorized\_keys` ファイルにコピーします。

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. ユーザーの作成を完了するには、`/home/rjmetric` ディレクトリの権限を変更して、`SSH` 経由でのアクセスを許可します。

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>サーバーに関連付けられている `sshd\_config` ファイルが既定のオプションに設定されていない場合は、特定のユーザーのみがサーバーにアクセスできます。これにより、[!DNL Commerce Intelligence] への接続に成功できなくなります。 このような場合、`AllowUsers` ユーザーにサーバーへのアクセスを許可するには、`rjmetric` のようなコマンドを実行する必要があります。

## [!DNL MySQL] 用の [!DNL Commerce Intelligence] ユーザーの作成 {#mysql}

組織では別のプロセスが必要になる場合がありますが、このユーザーを作成する最も簡単な方法は、権限を付与する権限を持つユーザーとして [!DNL MySQL] にログインしたときに次のクエリを実行することです。

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

`secure password here` を安全なパスワードに置き換えます。これは、`SSH` パスワードとは異なる場合があります。

このユーザーが特定のデータベース、テーブル、または列のデータにアクセスするのを制限するには、代わりに、許可されたデータへのアクセスのみを許可する GRANT クエリを実行します。

## [!DNL Commerce Intelligence] への接続およびユーザー情報の入力 {#finish}

まとめるには、接続とユーザー情報を [!DNL Commerce Intelligence] に入力する必要があります。 `MySQL credentials` のページは開いたままにしておきましたか。 そうでない場合は、**[!UICONTROL Data** > **Connections]** に移動して「**[!UICONTROL Add New Data Source]**」をクリックし、次に「[!DNL MySQL]」アイコンをクリックします。 「`Encrypted`」トグルを `Yes` に設定することを忘れないでください。

このページに、`Database Connection` のセクションから始まる次の情報を入力します。

* `Username`:[!DNL Commerce Intelligence] [!DNL MySQL] ユーザーのユーザー名
* `Password`:[!DNL Commerce Intelligence] [!DNL MySQL] ユーザーのパスワード
* `Port`：サーバー上の [!DNL MySQL] ポート（デフォルトでは 3306）
* `Host` デフォルトでは、localhost です。 一般に、これは [!DNL MySQL] サーバーのバインド アドレス値です。デフォルトでは `127.0.0.1 (localhost)` ですが、ローカル ネットワーク アドレス （`192.168.0.1` など）またはサーバーのパブリック IP アドレスの場合もあります。

  この値は、`my.cnf` を読み取る行の下の `/etc/my.cnf` ファイル（`\[mysqld\]` にあります）にあります。 このファイルで bind-address 行がコメントアウトされている場合、サーバーは外部からの接続の試行から保護されます。

`SSH Connection` のセクションで以下を実行します。

* `Remote Address`: トンネル先のサーバー [!DNL Commerce Intelligence] の IP アドレスまたはホスト名
* `Username`:[!DNL Commerce Intelligence] SSH （[!DNL Linux]）ユーザーのユーザー名
* `SSH Port`：サーバーの SSH ポート（デフォルトでは 22）

完了したら、「**[!UICONTROL Save & Test]**」をクリックして設定を完了します。

## 関連：

* [&#x200B; 統合の再認証 &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
