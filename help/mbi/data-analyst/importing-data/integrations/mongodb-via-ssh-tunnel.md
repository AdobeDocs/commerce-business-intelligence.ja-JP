---
title: SSH トンネル経由で [!DNL MongoDB] 接続
description: SSH トンネル経由で [!DNL MongoDB] 接続する方法を説明します。
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/fYXQ353R-dPB-rSeYCR2w0c8Lp5I0HoVYh1A3UAI6aI
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
source-git-commit: 3a6b80d7bcfa5db4d86ab4da81239e3ea804f6ad
workflow-type: tm+mt
source-wordcount: 686
ht-degree: 0%

---

# SSH トンネル経由で[!DNL MongoDB]を接続

SSH トンネルを介して[!DNL MongoDB] データベースを[!DNL Commerce Intelligence]に接続するには、次の操作を行う必要があります。

1. [&#x200B; [!DNL Commerce Intelligence] 公開鍵を取得](#retrieve)
1. [&#x200B; [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可](#allowlist)
1. [Commerce IntelligenceのLinux ユーザーの作成](#linux)
1. [Commerce Intelligence用に [!DNL MongoDB]  ユーザーを作成](#mongodb)
1. [接続とユーザー情報を [!DNL Commerce Intelligence]に入力します](#finish)

>[!NOTE]
>
>この設定は技術的な性質上、まだ実行したことがない場合は、開発者経由でサポートを受けることをお勧めします。

## [!DNL Commerce Intelligence]公開鍵を取得しています {#retrieve}

`public key`は、[!DNL Commerce Intelligence] `Linux` ユーザーの認証に使用されます。 次の節では、ユーザーの作成とキーの読み込みについて説明します。

1. **[!UICONTROL Data** > **Connections]**&#x200B;に移動し、**[!UICONTROL Add New Data Source]**&#x200B;をクリックします。
1. [!DNL MONGODB] アイコンをクリックします。
1. [!DNL MongoDB]資格情報ページが開いたら、`Encrypted` トグルを`Yes`に変更します。 SSH設定フォームが表示されます。
1. `public key`はこのフォームの下にあります。

このページをチュートリアル全体を通して開いたままにします。次のセクションと最後に必要になります。

少し迷っている場合は、[!DNL Commerce Intelligence]を移動してキーを取得する方法を次に示します。

![RJMetrics公開鍵を取得しています](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可 {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 `54.88.76.97`と`34.250.211.151`ですが、[!DNL MongoDB]資格情報ページにも表示されます。

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## [!DNL Commerce Intelligence]の`Linux` ユーザーを作成しています {#linux}

>[!IMPORTANT]
>
>サーバーに関連付けられている`sshd_config` ファイルが既定のオプションに設定されていない場合、特定のユーザーのみがサーバーアクセスを持っています。これにより、[!DNL Commerce Intelligence]への接続が正常に行われなくなります。 このような場合、`rjmetric` ユーザーがサーバーにアクセスできるようにするには、`AllowUsers`のようなコマンドを実行する必要があります。

これは、リアルタイム（または頻繁に更新される）データを含む限り、実稼動マシンまたはセカンダリマシンにすることができます。 このユーザーは、[!DNL MongoDB] サーバーに接続する権利を保持している限り、任意の方法で制限できます。

新しいユーザーを追加するには、次のコマンドを`Linux` サーバー上のルートとして実行します。

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

最初のセクションで取得した`public key`を覚えていますか？ ユーザーがデータベースにアクセスできるようにするには、キーを`authorized_keys`に読み込む必要があります。 キー全体を次のように`authorized_keys` ファイルにコピーします。

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

ユーザーの作成を完了するには、/home/rjmetric ディレクトリの権限を変更して、SSH経由でのアクセスを許可します。

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## [!DNL Commerce Intelligence] [!DNL MongoDB] ユーザーを作成しています {#mongodb}

[!DNL MongoDB] サーバーには2つの実行モードがあります – [1つは「認証」オプション &#x200B;](#auth) `(mongod -- auth)`を持ち、もう1つは持たず、[はデフォルト &#x200B;](#default)です。 [!DNL MongoDB] ユーザーを作成する手順は、サーバーが使用しているモードによって異なります。 続行する前に、必ずモードを確認してください。

### サーバーで`Auth` オプションを使用している場合： {#auth}

複数のデータベースに接続する場合は、管理者ユーザーとして[!DNL MongoDB]にログインし、次のコマンドを実行することで、ユーザーを追加できます。

>[!NOTE]
>
>使用可能なすべてのデータベースを表示するには、[!DNL Commerce Intelligence] ユーザーが`listDatabases.`を実行するための権限が必要です

このコマンドは、[!DNL Commerce Intelligence] ユーザーに`to all databases`へのアクセス権を付与します。

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

このコマンドを使用して、[!DNL Commerce Intelligence] ユーザーに`to a single database`へのアクセス権を付与します。

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

次のような応答が出力されます。

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### サーバーでデフォルトのオプションが使用されている場合 {#default}

サーバーが`auth` モードを使用しない場合、ユーザー名とパスワードがなくても[!DNL MongoDB] サーバーにアクセスできます。 ただし、`mongodb.conf` ファイル `(/etc/mongodb.conf)`に次の行が含まれていることを確認する必要があります。そうでない場合は、追加した後にサーバーを再起動してください。

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

[!DNL MongoDB] サーバーを別のアドレスにバインドするには、次の手順でデータベースのホスト名を調整します。

## 接続とユーザー情報を[!DNL Commerce Intelligence]に入力しています {#finish}

最後に、接続とユーザー情報を[!DNL Commerce Intelligence]に入力する必要があります。 [!DNL MongoDB]資格情報ページを開いたままにしましたか？ そうでない場合は、**[!UICONTROL Data > Connections]**&#x200B;に移動して&#x200B;**[!UICONTROL Add New Data Source]**&#x200B;をクリックし、[!DNL MongoDB] アイコンをクリックします。 `Encrypted` トグルを`Yes`に変更することを忘れないでください。

`Database Connection` セクションから始めて、このページに次の情報を入力します。

* `Host`: `127.0.0.1`
* `Username`: [!DNL Commerce Intelligence] [!DNL MongoDB] ユーザー名（`rjmetric`である必要があります）
* `Password`: [!DNL Commerce Intelligence] [!DNL MongoDB] パスワード
* `Port`: MongoDBのサーバー上のポート （`27017` デフォルト）
* `Database Name` （オプション）: 1つのデータベースへのアクセスのみを許可した場合は、ここでデータベースの名前を指定します。

`SSH Connection` セクションの下：

* `Remote Address`: SSH接続するサーバーのIP アドレスまたはホスト名
* `Username`: [!DNL Commerce Intelligence] Linux （SSH） ユーザー名（rjmetricにする必要があります）
* `SSH Port`: サーバー上のSSH ポート （既定では22）

完了したら、**[!UICONTROL Save & Test]**&#x200B;をクリックして設定を完了します。

>[!NOTE]
>
>SSH ホストキーの登録、更新、エラーメッセージ、およびトラブルシューティングについては、[SSH ホストキー検証](ssh-host-key-verification.md)を参照してください。

## 関連 {#related}

* [SSH ホスト キーの検証](ssh-host-key-verification.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
