---
title: 接続中 [!DNL MySQL] ssh トンネル経由
description: 接続方法を学ぶ [!DNL MySQL] ssh トンネル経由。
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# 接続 [!DNL MySQL] 経由 [!DNL SSH Tunnel]

* [を取得します [!DNL Commerce Intelligence] 公開鍵](#retrieve)
* [へのアクセスを許可 [!DNL Commerce Intelligence] IP アドレス](#allowlist)
* [用の Linux ユーザーの作成 [!DNL Commerce Intelligence]](#linux)
* [を作成 [!DNL MySQL] のユーザー [!DNL Commerce Intelligence]](#mysql)
* [接続およびユーザー情報の入力先 [!DNL Commerce Intelligence]](#finish)

## ジャンプ

* [[!DNL MySQL] 経由 ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] 経由 [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

を接続するには [!DNL MySQL] データベース先 [!DNL Commerce Intelligence] 経由 `SSH tunnel`次の手順を実行する必要があります。

1. を取得します [!DNL Commerce Intelligence] `public key`
1. へのアクセスを許可 [!DNL Commerce Intelligence] `IP address`
1. を作成 `Linux` のユーザー [!DNL Commerce Intelligence]
1. を作成 `MySQL` のユーザー [!DNL Commerce Intelligence]
1. 接続およびユーザー情報の入力先 [!DNL Commerce Intelligence]


## の取得 [!DNL Commerce Intelligence] 公開鍵 {#retrieve}

この `public key` を使用して、以下を認証します [!DNL Commerce Intelligence] `Linux` ユーザー。 次の節では、ユーザーを作成してキーを読み込みます。

1. に移動 **[!UICONTROL Manage Data** > **Connections]** をクリックして、 **[!UICONTROL Add New Data Source]**.
1. 「」をクリックします `MySQL` アイコン。
1. 後 `MySQL credentials` ページが開いたら、 `Encrypted` 切り替え `Yes`. SSH 設定フォームが表示されます。
1. この `public key` このフォームの下にあります。

このページは、チュートリアルの最後まで開いたままにしておきます。次の節と最後に必要になります。

次の方法で操作できます [!DNL Commerce Intelligence] キーを取得するには：

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## へのアクセスを許可 [!DNL Commerce Intelligence] IP アドレス {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 次のとおりです `54.88.76.97` および `34.250.211.151` しかし、それらは `MySQL credentials` ページ。 上のGIFの青いボックスを参照してください。

## の作成 [!DNL Linux] のユーザー [!DNL Commerce Intelligence] {#linux}

リアルタイム（または頻繁に更新される）のデータが含まれている限り、実稼動マシンまたはセカンダリマシンを使用できます。 いいよ [このユーザーを制限](../../../administrator/account-management/restrict-db-access.md) 好きなように、それが接続する権利を保持している限り `MySQL` サーバー。

1. 新しいユーザーを追加するには、次のコマンドを root で実行します。 [!DNL Linux] サーバー：

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. を覚えている `public key` 最初のセクションで取り出したのか？ ユーザーがデータベースに確実にアクセスできるようにするには、キーをに読み込む必要があります `authorized\_keys`.

   キー全体をにコピーします `authorized\_keys` ファイルの内容は次のとおりです。

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. ユーザーの作成を完了するには、権限を `/home/rjmetric` 経由でアクセスを許可するディレクトリ `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>次の場合 `sshd\_config` サーバーに関連付けられているファイルがデフォルトオプションに設定されず、特定のユーザーのみがサーバーアクセス権を持ちます。これにより、への接続に成功するのを防ぎます [!DNL Commerce Intelligence]. この場合、のようなコマンドを実行する必要があります。 `AllowUsers` を許可する `rjmetric` サーバーへのユーザーアクセス。

## の作成 [!DNL MySQL] のユーザー [!DNL Commerce Intelligence] {#mysql}

組織では別のプロセスが必要になる場合がありますが、このユーザーを作成する最も簡単な方法は、にログインしたときに次のクエリを実行することです [!DNL MySQL] 権限を付与できるユーザーとして、次の権限があります。

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

置換 `secure password here` と異なる場合がある安全なパスワードを使用します。 `SSH` パスワード。

このユーザーが特定のデータベース、テーブル、または列のデータにアクセスするのを制限するには、代わりに、許可されたデータへのアクセスのみを許可する GRANT クエリを実行します。

## 接続およびユーザー情報の入力 [!DNL Commerce Intelligence] {#finish}

最後に、接続とユーザー情報をに入力する必要があります。 [!DNL Commerce Intelligence]. を残しましたか `MySQL credentials` ページを開きますか？ そうでない場合は、に移動します **[!UICONTROL Data** > **Connections]** をクリックして、 **[!UICONTROL Add New Data Source]**&#x200B;を選択し、続いて [!DNL MySQL] アイコン。 設定を忘れないでください `Encrypted` 切り替え `Yes`.

このページに以下の情報を入力します。まず、 `Database Connection` セクション：

* `Username`：のユーザー名 [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー
* `Password`：のパスワード [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー
* `Port`: [!DNL MySQL] サーバーのポート （デフォルトは 3306）
* `Host` デフォルトでは、localhost です。 通常、これはユーザのバインド アドレスの値です [!DNL MySQL] サーバー（デフォルトでは） `127.0.0.1 (localhost)`ただし、ローカルネットワークアドレス（例：）も指定できます `192.168.0.1`）またはサーバーのパブリック IP アドレス。

  値は、 `my.cnf` ファイル （の場所： `/etc/my.cnf`）を表す行の下 `\[mysqld\]`. このファイルで bind-address 行がコメントアウトされている場合、サーバーは外部からの接続の試行から保護されます。

が含まれる `SSH Connection` セクション：

* `Remote Address`：サーバーの IP アドレスまたはホスト名 [!DNL Commerce Intelligence] ～にトンネルを通す
* `Username`：のユーザー名 [!DNL Commerce Intelligence] SSH （[!DNL Linux]） ユーザー
* `SSH Port`：サーバーの SSH ポート（デフォルトでは 22）

完了したら、 **[!UICONTROL Save & Test]** をクリックして設定を完了します。

## 関連：

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
