---
title: 接続 [!DNL MongoDB] SSH トンネル経由
description: 接続方法を学ぶ [!DNL MongoDB] SSH トンネル経由。
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# 接続 [!DNL MongoDB] SSH トンネル経由

次の手順で [!DNL MongoDB] データベースへ [!DNL Commerce Intelligence] SSH トンネルを介して、次の操作を行う必要があります。

1. [を取得する [!DNL Commerce Intelligence] 公開鍵](#retrieve)
1. [次へのアクセスを許可： [!DNL Commerce Intelligence] IP アドレス](#allowlist)
1. [Commerce Intelligence 用の Linux ユーザーの作成](#linux)
1. [の作成 [!DNL MongoDB] コマースインテリジェンス用のユーザー](#mongodb)
1. [接続とユーザー情報をに入力します。 [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>この設定は技術的な性質上、Adobeでは、開発者をループして、これをおこなったことがない場合に役立てることをお勧めします。

## の取得 [!DNL Commerce Intelligence] 公開鍵 {#retrieve}

The `public key` を認証するために使用します。 [!DNL Commerce Intelligence] `Linux` ユーザー。 次の節では、ユーザーの作成とキーの読み込みの手順を説明します。

1. に移動します。 **[!UICONTROL Data** > **Connections]** をクリックします。 **[!UICONTROL Add New Data Source]**.
1. 次をクリック： [!DNL MONGODB] アイコン。
1. 次の期間の後に [!DNL MongoDB] 認証情報ページが開きます。 `Encrypted` 切り替える `Yes`. SSH セットアップフォームが表示されます。
1. The `public key` はこのフォームの下に配置されています。

このページは、チュートリアル全体で開いたままにしておきます。次のセクションで、最後におこなう必要があります。

少し迷ったら、次の操作を実行します。 [!DNL Commerce Intelligence] キーを取得するには：

![RJMetrics 公開鍵の取得](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## 次へのアクセスを許可： [!DNL Commerce Intelligence] IP アドレス {#allowlist}

接続が成功するには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 これらは `54.88.76.97` および `34.250.211.151`ですが、それはまた、 [!DNL MongoDB] 認証情報ページ：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## の作成 `Linux` のユーザー [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>次の場合、 `sshd_config` サーバーに関連付けられたファイルがデフォルトのオプションに設定されていない場合は、特定のユーザーだけがサーバーにアクセスできます。これにより、 [!DNL Commerce Intelligence]. このような場合、次のようなコマンドを実行する必要があります。 `AllowUsers` 許可する `rjmetric` ユーザーがサーバーにアクセスできること。

リアルタイム（または頻繁に更新される）データが含まれる限り、実稼動マシンまたはセカンダリマシンにすることができます。 このユーザーは、 [!DNL MongoDB] サーバー。

新しいユーザーを追加するには、次のコマンドを root として `Linux` サーバ：

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

次を記憶する： `public key` 最初の部分で取り戻したの？ ユーザーがデータベースに確実にアクセスできるようにするには、キーを `authorized_keys`. キー全体を `authorized_keys` ファイルの内容は次のとおりです。

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

ユーザーの作成を完了するには、/home/rjmetric ディレクトリの権限を変更して、SSH を介したアクセスを許可します。

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## の作成 [!DNL Commerce Intelligence] [!DNL MongoDB] ユーザー {#mongodb}

[!DNL MongoDB] サーバは 2 つの実行モードを持つ — [1 つは「auth」オプションを持つもの](#auth) `(mongod -- auth)` 一人はいなかった [（これはデフォルト）](#default). を作成する手順 [!DNL MongoDB] ユーザーは、サーバーが使用しているモードによって異なります。 続行する前に、モードを確認してください。

### サーバーが `Auth` オプション： {#auth}

複数のデータベースに接続する場合は、にログインしてユーザーを追加できます。 [!DNL MongoDB] 管理者ユーザーとして、次のコマンドを実行します。

>[!NOTE]
>
>使用可能なすべてのデータベースを表示するには、 [!DNL Commerce Intelligence] ユーザーはを実行する権限が必要です `listDatabases.`

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

### サーバーがデフォルトのオプションを使用している場合 {#default}

サーバーが `auth` モード、 [!DNL MongoDB] ユーザー名やパスワードがなくても、サーバーにアクセスできます。 ただし、 `mongodb.conf` ファイル `(/etc/mongodb.conf)` には次の行があります。追加しない場合は、サーバーを追加した後で再起動します。

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

バインドするには [!DNL MongoDB] サーバーを別のアドレスに変更する場合は、次の手順でデータベースのホスト名を調整します。

## 次の場所に接続とユーザー情報を入力 [!DNL Commerce Intelligence] {#finish}

まとめるには、接続とユーザー情報を次のように入力する必要があります。 [!DNL Commerce Intelligence]. あなたは [!DNL MongoDB] 認証情報ページを開きますか？ そうでない場合は、に移動します。 **[!UICONTROL Data > Connections]** をクリックします。 **[!UICONTROL Add New Data Source]**&#x200B;を、 [!DNL MongoDB] アイコン。 忘れずに `Encrypted` 切り替える `Yes`.

このページに、以下の情報を入力します。 `Database Connection` セクション：

* `Host`: `127.0.0.1`
* `Username`: [!DNL Commerce Intelligence] [!DNL MongoDB] ユーザー名 ( `rjmetric`)
* `Password`: [!DNL Commerce Intelligence] [!DNL MongoDB] パスワード
* `Port`：サーバー上の MongoDB のポート (`27017` （デフォルト）
* `Database Name` （オプション）:1 つのデータベースへのアクセスのみを許可する場合は、そのデータベースの名前をここに指定します。

の下 `SSH Connection` セクション：

* `Remote Address`:SSH で接続するサーバーの IP アドレスまたはホスト名
* `Username`: [!DNL Commerce Intelligence] Linux(SSH) ユーザー名 (rjmetric)
* `SSH Port`：サーバー上の SSH ポート（デフォルトは 22）

完了したら、「 **[!UICONTROL Save Test]** をクリックして設定を完了します。

### 関連

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
