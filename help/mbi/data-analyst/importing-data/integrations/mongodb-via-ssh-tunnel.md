---
title: 接続 [!DNL MongoDB] ssh トンネル経由
description: 接続方法を学ぶ [!DNL MongoDB] ssh トンネル経由。
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# 接続 [!DNL MongoDB] ssh トンネル経由

を接続するには [!DNL MongoDB] データベース先 [!DNL Commerce Intelligence] ssh トンネルを経由して、次の操作を行う必要があります。

1. [を取得します [!DNL Commerce Intelligence] 公開鍵](#retrieve)
1. [へのアクセスを許可 [!DNL Commerce Intelligence] IP アドレス](#allowlist)
1. [Commerce Intelligence 用の Linux ユーザーの作成](#linux)
1. [を作成 [!DNL MongoDB] Commerce Intelligence のユーザー](#mongodb)
1. [接続およびユーザー情報の入力先 [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>この設定は技術的な性質上、Adobeでは、開発者に協力を求め、まだこの作業を行っていない場合は、支援を求めることをお勧めします。

## の取得 [!DNL Commerce Intelligence] 公開鍵 {#retrieve}

この `public key` を使用して、以下を認証します [!DNL Commerce Intelligence] `Linux` ユーザー。 次の節では、ユーザーの作成とキーの読み込みについて説明します。

1. に移動 **[!UICONTROL Data** > **Connections]** をクリックして、 **[!UICONTROL Add New Data Source]**.
1. 「」をクリックします [!DNL MONGODB] アイコン。
1. 後 [!DNL MongoDB] 資格情報ページが開きます。変更します `Encrypted` 切り替え `Yes`. SSH 設定フォームが表示されます。
1. この `public key` このフォームの下にあります。

このページは、チュートリアルの最後まで開いたままにしておきます。次の節と最後に必要になります。

少し迷った場合は、次の方法で移動できます [!DNL Commerce Intelligence] キーを取得するには：

![RJMetrics 公開鍵の取得](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## へのアクセスを許可 [!DNL Commerce Intelligence] IP アドレス {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 次のとおりです `54.88.76.97` および `34.250.211.151`ただし、そのページは [!DNL MongoDB] 資格情報ページ：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## の作成 `Linux` のユーザー [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>次の場合 `sshd_config` サーバーに関連付けられているファイルがデフォルトオプションに設定されず、特定のユーザーのみがサーバーアクセス権を持ちます。これにより、への接続に成功するのを防ぎます [!DNL Commerce Intelligence]. この場合、のようなコマンドを実行する必要があります。 `AllowUsers` を許可する `rjmetric` サーバーへのユーザーアクセス。

リアルタイム（または頻繁に更新される）のデータが含まれている限り、実稼動マシンまたはセカンダリマシンを使用できます。 このユーザーがに接続する権利を保持している限り、このユーザーを好きなように制限することができます。 [!DNL MongoDB] サーバー。

新しいユーザーを追加するには、次のコマンドを root で実行します。 `Linux` サーバー：

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

を覚えている `public key` 最初のセクションで取り出したのか？ ユーザーがデータベースに確実にアクセスできるようにするには、キーをに読み込む必要があります `authorized_keys`. キー全体をにコピーします `authorized_keys` ファイルの内容は次のとおりです。

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

ユーザーの作成を完了するには、/home/rjmetric ディレクトリの権限を変更して、SSH 経由でのアクセスを許可します。

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## の作成 [!DNL Commerce Intelligence] [!DNL MongoDB] ユーザー {#mongodb}

[!DNL MongoDB] サーバには 2 つの実行モードがあります。 [「auth」オプションを持つもの](#auth) `(mongod -- auth)` 1 つはなし、 [（デフォルト）](#default). を作成する手順 [!DNL MongoDB] ユーザーは、サーバーが使用しているモードによって異なります。 続行する前に、モードを確認してください。

### サーバーがを使用している場合 `Auth` オプション： {#auth}

複数のデータベースに接続する場合、にログインしてユーザーを追加できます。 [!DNL MongoDB] 管理者ユーザーとして、および次のコマンドを実行します。

>[!NOTE]
>
>使用可能なすべてのデータベースを表示するには、 [!DNL Commerce Intelligence] ユーザーが実行するには権限が必要です `listDatabases.`

このコマンドは、 [!DNL Commerce Intelligence] ユーザーアクセス `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

次のコマンドを使用して、 [!DNL Commerce Intelligence] ユーザーアクセス `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

これにより、次のような応答が出力されます。

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### サーバーでデフォルトオプションを使用している場合 {#default}

サーバーがを使用していない場合 `auth` モード、 [!DNL MongoDB] サーバーは、ユーザー名とパスワードがなくてもアクセスできます。 ただし、以下を確実にする必要があります `mongodb.conf` ファイル `(/etc/mongodb.conf)` には次の行があります。行が含まれていない場合は、追加した後にサーバーを再起動してください。

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

をバインドするには [!DNL MongoDB] サーバーを別のアドレスに変更する場合は、それに応じて次の手順でデータベースのホスト名を調整します。

## 接続およびユーザー情報の入力 [!DNL Commerce Intelligence] {#finish}

最後に、接続とユーザー情報をに入力する必要があります。 [!DNL Commerce Intelligence]. を残しましたか [!DNL MongoDB] 資格情報ページが開かれますか？ そうでない場合は、に移動します **[!UICONTROL Data > Connections]** をクリックして、 **[!UICONTROL Add New Data Source]**&#x200B;を選択し、続いて [!DNL MongoDB] アイコン。 を変更することを忘れないでください `Encrypted` 切り替え `Yes`.

このページに以下の情報を入力します。まず、 `Database Connection` セクション：

* `Host`: `127.0.0.1`
* `Username`：です [!DNL Commerce Intelligence] [!DNL MongoDB] ユーザー名（でなければなりません `rjmetric`）
* `Password`：です [!DNL Commerce Intelligence] [!DNL MongoDB] password
* `Port`：サーバー上の MongoDB のポート（`27017` デフォルト）
* `Database Name` （オプション）:1 つのデータベースへのアクセスのみを許可した場合は、そのデータベースの名前をここに指定します。

の下 `SSH Connection` セクション：

* `Remote Address`:SSH で接続するサーバーの IP アドレスまたはホスト名
* `Username`：です [!DNL Commerce Intelligence] Linux （SSH）ユーザー名（rjmetric にする）
* `SSH Port`：サーバー上の SSH ポート（デフォルトでは 22）

完了したら、 **[!UICONTROL Save Test]** をクリックして設定を完了します。

### 関連

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
