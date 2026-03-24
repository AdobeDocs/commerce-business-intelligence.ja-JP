---
title: SSH トンネル経由で [!DNL MySQL] 接続
description: SSH トンネル経由で [!DNL MySQL] 接続する方法を説明します。
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
TQID: https://experienceleague.adobe.com/WhcwNz65oubtSKnVGeoHfbEVbPvo1fq-RvpAcP96NEc
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 615
ht-degree: 0%

---

# [!DNL MySQL]経由で[!DNL SSH Tunnel]に接続

* [&#x200B; [!DNL Commerce Intelligence] 公開鍵を取得](#retrieve)
* [&#x200B; [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可](#allowlist)
* [&#x200B; [!DNL Commerce Intelligence]のLinux ユーザーを作成](#linux)
* [&#x200B; [!DNL MySQL] の [!DNL Commerce Intelligence] ユーザーを作成](#mysql)
* [接続とユーザー情報を [!DNL Commerce Intelligence]に入力します](#finish)

## に移動

* [[!DNL MySQL]経由 &#x200B;](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL]経由で [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

[!DNL MySQL] データベースを[!DNL Commerce Intelligence]経由で`SSH tunnel`に接続するには、次の操作を行う必要があります。

1. [!DNL Commerce Intelligence] `public key`を取得
1. [!DNL Commerce Intelligence] `IP address`へのアクセスを許可
1. `Linux`の[!DNL Commerce Intelligence] ユーザーを作成
1. `MySQL`の[!DNL Commerce Intelligence] ユーザーを作成
1. 接続とユーザー情報を[!DNL Commerce Intelligence]に入力してください


## [!DNL Commerce Intelligence]公開鍵を取得しています {#retrieve}

`public key`は、[!DNL Commerce Intelligence] `Linux` ユーザーの認証に使用されます。 次のセクションでは、ユーザーを作成し、キーを読み込みます。

1. **[!UICONTROL Manage Data** > **Connections]**&#x200B;に移動し、**[!UICONTROL Add New Data Source]**&#x200B;をクリックします。
1. `MySQL` アイコンをクリックします。
1. `MySQL credentials` ページが開いたら、`Encrypted` トグルを`Yes`に設定します。 SSH設定フォームが表示されます。
1. `public key`はこのフォームの下にあります。

このページをチュートリアル全体を通して開いたままにします。次のセクションと最後に必要になります。

[!DNL Commerce Intelligence]を移動してキーを取得する方法は次のとおりです。

![SSH トンネルを介したMySQL接続のアニメーションデモ &#x200B;](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可 {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 `54.88.76.97`と`34.250.211.151`ですが、`MySQL credentials` ページにもあります。 上のGIFの青いボックスを参照してください。

## [!DNL Linux]の[!DNL Commerce Intelligence] ユーザーを作成しています {#linux}

これは、リアルタイム（または頻繁に更新される）データを含む限り、実稼動マシンまたはセカンダリマシンにすることができます。 [&#x200B; サーバーに接続する権利を保持している限り、このユーザー](../../../administrator/account-management/restrict-db-access.md)を任意の方法で`MySQL`制限できます。

1. 新しいユーザーを追加するには、次のコマンドを[!DNL Linux] サーバー上のルートとして実行します。

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. 最初のセクションで取得した`public key`を覚えていますか？ ユーザーがデータベースにアクセスできるようにするには、キーを`authorized\_keys`に読み込む必要があります。

   キー全体を次のように`authorized\_keys` ファイルにコピーします。

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. ユーザーの作成を完了するには、`/home/rjmetric` ディレクトリの権限を変更して、`SSH`経由のアクセスを許可します。

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>サーバーに関連付けられている`sshd\_config` ファイルが既定のオプションに設定されていない場合、特定のユーザーのみがサーバーアクセスを持っています。これにより、[!DNL Commerce Intelligence]への接続が正常に行われなくなります。 このような場合、`AllowUsers` ユーザーがサーバーにアクセスできるようにするには、`rjmetric`のようなコマンドを実行する必要があります。

## [!DNL MySQL]の[!DNL Commerce Intelligence] ユーザーを作成しています {#mysql}

組織には別のプロセスが必要になる場合がありますが、このユーザーを作成する最も簡単な方法は、権限を付与する権限を持つユーザーとして[!DNL MySQL]にログインしたときに次のクエリを実行することです。

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

`secure password here`を安全なパスワードに置き換えます。これは、`SSH` パスワードとは異なる場合があります。

このユーザーが特定のデータベース、テーブル、または列内のデータにアクセスすることを制限するには、代わりに、許可するデータへのアクセスのみを許可するGRANT クエリを実行できます。

## 接続とユーザー情報を[!DNL Commerce Intelligence]に入力しています {#finish}

最後に、接続とユーザー情報を[!DNL Commerce Intelligence]に入力する必要があります。 `MySQL credentials` ページを開いたままにしましたか？ そうでない場合は、**[!UICONTROL Data** > **Connections]**&#x200B;に移動して&#x200B;**[!UICONTROL Add New Data Source]**&#x200B;をクリックし、[!DNL MySQL] アイコンをクリックします。 `Encrypted` トグルを`Yes`に設定することを忘れないでください。

`Database Connection` セクションから始めて、このページに次の情報を入力します。

* `Username`: [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーのユーザー名
* `Password`: [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーのパスワード
* `Port`: サーバー上の[!DNL MySQL] ポート （既定では3306）
* `Host` デフォルトでは、これはlocalhostです。 一般に、これは[!DNL MySQL] サーバーのバインド アドレス値です。デフォルトは`127.0.0.1 (localhost)`ですが、一部のローカル ネットワーク アドレス （例：`192.168.0.1`）またはサーバーのパブリック IP アドレスにすることもできます。

  値は、`my.cnf`を読み込む行の下の`/etc/my.cnf` ファイル（`\[mysqld\]`にある）にあります。 そのファイルでバインドアドレス行がコメントアウトされると、サーバーは外部からの接続試行から保護されます。

`SSH Connection` セクション：

* `Remote Address`: サーバー[!DNL Commerce Intelligence]のIP アドレスまたはホスト名は、にトンネルされます
* `Username`: [!DNL Commerce Intelligence] SSH （[!DNL Linux]） ユーザーのユーザー名
* `SSH Port`: サーバーのSSH ポート （既定では22）

完了したら、**[!UICONTROL Save & Test]**&#x200B;をクリックして設定を完了します。

## 関連：

* [統合を再認証しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
