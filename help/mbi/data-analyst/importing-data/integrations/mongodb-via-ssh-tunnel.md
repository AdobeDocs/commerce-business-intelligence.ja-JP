---
title: SSH トンネル経由  [!DNL MongoDB]  接続
description: SSH トンネルを介して接続する方法  [!DNL MongoDB]  説明します。
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# SSH トンネル経由の [!DNL MongoDB] の接続

SSH トンネルを使用して [!DNL MongoDB] データベースを [!DNL Commerce Intelligence] に接続するには、次の手順を実行する必要があります。

1. [ [!DNL Commerce Intelligence]  公開鍵の取得](#retrieve)
1. [ [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可](#allowlist)
1. [Commerce Intelligence用の Linux ユーザーの作成](#linux)
1. [Commerce Intelligence用  [!DNL MongoDB]  ユーザーの作成](#mongodb)
1. [接続およびユーザー情報の入力先  [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>この設定は技術的な性質上、Adobeでは、開発者に協力を求めることをお勧めします。これまでにこれをおこなわなかった場合は、

## [!DNL Commerce Intelligence] 公開鍵の取得 {#retrieve}

`public key` は、[!DNL Commerce Intelligence] `Linux` ユーザーの認証に使用されます。 次の節では、ユーザーの作成とキーの読み込みについて説明します。

1. **[!UICONTROL Data** > **Connections]** に移動し、「**[!UICONTROL Add New Data Source]**」をクリックします。
1. [!DNL MONGODB] アイコンをクリックします。
1. [!DNL MongoDB] 資格情報ページが開いたら、「`Encrypted`」切り替えスイッチを `Yes` に変更します。 SSH 設定フォームが表示されます。
1. `public key` はこのフォームの下にあります。

このページは、チュートリアルの最後まで開いたままにしておきます。次の節と最後に必要になります。

少し迷った場合は、[!DNL Commerce Intelligence] を移動してキーを取得する方法を次に示します。

![RJMetrics 公開鍵の取得 ](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可します {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 これらは `54.88.76.97` と `34.250.211.151` ですが、[!DNL MongoDB] の資格情報ページにも表示されます。

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## `Linux` 用の [!DNL Commerce Intelligence] ユーザーの作成 {#linux}

>[!IMPORTANT]
>
>サーバーに関連付けられている `sshd_config` ファイルが既定のオプションに設定されていない場合は、特定のユーザーのみがサーバーにアクセスできます。これにより、[!DNL Commerce Intelligence] への接続に成功できなくなります。 このような場合、`AllowUsers` ユーザーにサーバーへのアクセスを許可するには、`rjmetric` のようなコマンドを実行する必要があります。

リアルタイム（または頻繁に更新される）のデータが含まれている限り、実稼動マシンまたはセカンダリマシンを使用できます。 [!DNL MongoDB] サーバーへの接続権限を保持している限り、このユーザーを好きなように制限することができます。

新しいユーザーを追加するには、`Linux` サーバーで次のコマンドを root として実行します。

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

最初のセクションで取得した `public key` を覚えていますか？ ユーザーがデータベースにアクセスできるようにするには、キーを `authorized_keys` に読み込む必要があります。 次のように、キー全体を `authorized_keys` ファイルにコピーします。

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

ユーザーの作成を完了するには、/home/rjmetric ディレクトリの権限を変更して、SSH 経由でのアクセスを許可します。

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## [!DNL Commerce Intelligence] [!DNL MongoDB] ユーザーの作成 {#mongodb}

[!DNL MongoDB] サーバーには 2 つの実行モードがあります [1 つは「認証」オプションを使用したもの ](#auth)`(mongod -- auth)` もう 1 つは [ デフォルト ](#default) を使用したもの）。 [!DNL MongoDB] ユーザーを作成する手順は、サーバーで使用しているモードによって異なります。 続行する前に、モードを確認してください。

### サーバーで `Auth` オプションを使用する場合： {#auth}

複数のデータベースに接続する場合、管理者ユーザーとして [!DNL MongoDB] にログインし、次のコマンドを実行することでユーザーを追加できます。

>[!NOTE]
>
>使用可能なすべてのデータベースを表示するには、[!DNL Commerce Intelligence] ユーザーが `listDatabases.` を実行する権限が必要です

このコマンドは、[!DNL Commerce Intelligence] ユーザーに次のアクセス権 `to all databases` 付与します。

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

次のコマンドを使用して、[!DNL Commerce Intelligence] のユーザーに `to a single database` のアクセス権を付与します。

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

サーバーが `auth` モードを使用しない場合、ユーザー名とパスワードがなくても [!DNL MongoDB] サーバーにアクセスできます。 ただし、`mongodb.conf` ファイル `(/etc/mongodb.conf)` に次の行が含まれていることを確認する必要があります。行が含まれていない場合は、追加した後にサーバーを再起動します。

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

[!DNL MongoDB] サーバーを別のアドレスにバインドするには、次の手順でデータベースホスト名を適宜調整します。

## [!DNL Commerce Intelligence] への接続およびユーザー情報の入力 {#finish}

まとめるには、接続とユーザー情報を [!DNL Commerce Intelligence] に入力する必要があります。 [!DNL MongoDB] 資格情報ページを開いたままにしましたか？ そうでない場合は、**[!UICONTROL Data > Connections]** に移動して「**[!UICONTROL Add New Data Source]**」をクリックし、次に「[!DNL MongoDB]」アイコンをクリックします。 `Encrypted` の切り替えを `Yes` に変更することを忘れないでください。

このページに、`Database Connection` のセクションから始まる次の情報を入力します。

* `Host`: `127.0.0.1`
* `Username`:[!DNL Commerce Intelligence] [!DNL MongoDB] ユーザー名（`rjmetric` にする必要があります）
* `Password`:[!DNL Commerce Intelligence] [!DNL MongoDB] のパスワード
* `Port`：サーバー上の MongoDB のポート（デフォルトでは `27017`）
* `Database Name` （オプション）:1 つのデータベースへのアクセスのみを許可した場合は、そのデータベースの名前をここに指定します。

「`SSH Connection`」セクションで、

* `Remote Address`:SSH で接続するサーバーの IP アドレスまたはホスト名
* `Username`:[!DNL Commerce Intelligence] Linux （SSH）のユーザー名（rjmetric）
* `SSH Port`：サーバー上の SSH ポート（デフォルトでは 22）

完了したら、「**[!UICONTROL Save Test]**」をクリックして設定を完了します。

### 関連

* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
