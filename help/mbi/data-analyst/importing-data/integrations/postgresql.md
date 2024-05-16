---
title: SSH トンネルを介した PostgreSQL の接続
description: SSH トンネルを介して PostgreSQL データベースをCommerce Intelligence に接続する方法を説明します。
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 0%

---

# 接続 [!DNL PostgreSQL] 経由 [!DNL SSH Tunnel]

を接続するには [!DNL PostgreSQL] データベース先 [!DNL Commerce Intelligence] 経由 `SSH tunnel`次の手順を実行する必要があります。

1. [を取得します [!DNL Commerce Intelligence] 公開鍵](#retrieve)
1. [へのアクセスを許可 [!DNL Commerce Intelligence] IP アドレス](#allowlist)
1. [を作成 [!DNL Linux] のユーザー [!DNL Commerce Intelligence]](#linux)
1. [を作成 [!DNL PostgreSQL] のユーザー [!DNL Commerce Intelligence]](#postgres)
1. [接続およびユーザー情報の入力先 [!DNL Commerce Intelligence]](#finish)

## の取得 [!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

この `public key` を使用して、以下を認証します [!DNL Commerce Intelligence] [!DNL Linux] ユーザー。 ここでは、ユーザーを作成し、キーを読み込みます。

1. に移動 **[!UICONTROL Manage Data** > **Connections]** をクリックして、 **[!UICONTROL Add a Data Source]**.
1. 「」をクリックします [!DNL PostgreSQL] アイコン。
1. 後 `PostgreSQL credentials` ページが開いたら、 `Encrypted` 切り替え `Yes`. 次が表示されます `SSH` フォームを設定します。
1. この `public key` このフォームの下にあります。

このページは、チュートリアルの最後まで開いたままにしておきます。次の節と最後に必要になります。

以下に、のナビゲーション方法を示します [!DNL Commerce Intelligence] キーを取得するには：

![RJMetrics 公開鍵の取得](../../../assets/get-mbi-public-key.gif)

## へのアクセスを許可 [!DNL Commerce Intelligence] IP アドレス {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 このプロパティは `54.88.76.97/32`ただし、そのページは `PostgreSQL` 資格情報ページ。 上のGIFの青いボックスを参照してください。

## の作成 [!DNL Linux] のユーザー [!DNL Commerce Intelligence] {#linux}

リアルタイム（または頻繁に更新される）のデータが含まれている限り、実稼動マシンまたはセカンダリマシンを使用できます。 いいよ [このユーザーを制限](../../../administrator/account-management/restrict-db-access.md) 好きなように、それが接続する権利を保持している限り [!DNL PostgreSQL] サーバー。

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
```

>[!IMPORTANT]
>
>次の場合 `sshd\_config` サーバーに関連付けられているファイルがデフォルトオプションに設定されず、特定のユーザーのみがサーバーアクセス権を持ちます。これにより、への接続に成功するのを防ぎます [!DNL Commerce Intelligence]. この場合、のようなコマンドを実行する必要があります。 `AllowUsers` を使用して、プライマリユーザーがサーバーにアクセスできるようにします。

## の作成 [!DNL Commerce Intelligence] [!DNL Postgres] ユーザー {#postgres}

組織では別のプロセスが必要になる場合がありますが、このユーザーを作成する最も簡単な方法は、権限を付与する権限を持つユーザーとして Postgres にログインしたときに次のクエリを実行することです。 また、ユーザーは、というスキーマを所有している必要があります。 [!DNL Commerce Intelligence] は、へのアクセス権を付与されています。

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

置換 `secure password` ssh パスワードとは異なる独自の安全なパスワードを使用します。 また、を置き換えてください。 `database name` および `schema name` 使用するデータベース内の適切な名前。

複数のデータベースまたはスキーマを接続する場合は、必要に応じてこのプロセスを繰り返します。

## 接続およびユーザー情報の入力 [!DNL Commerce Intelligence] {#finish}

最後に、接続とユーザー情報をに入力する必要があります。 [!DNL Commerce Intelligence]. を残しましたか [!DNL PostgreSQL] 資格情報ページが開かれますか？ そうでない場合は、に移動します **[!UICONTROL Manage Data > Connections]** をクリックして、 **[!UICONTROL Add a Data Source]**&#x200B;を選択し、続いて [!DNL PostgreSQL] アイコン。 設定を忘れないでください `Encrypted` 切り替え `Yes`.

このページに以下の情報を入力します。まず、 `Database Connection` セクション：

* `Username`:RJMetrics Postgres のユーザー名（rjmetric）
* `Password`:RJMetrics Postgres パスワード
* `Port`：サーバー上の PostgreSQL ポート（デフォルトでは 5432）
* `Host`:127.0.0.1

次の下 `SSH Connection`:

* `Remote Address`:SSH で接続するサーバーの IP アドレスまたはホスト名
* `Username`:SSH ログイン名（rjmetric）
* `SSH Port`：サーバーの SSH ポート（デフォルトでは 22）

完了したら、 **保存してテスト** をクリックして設定を完了します。

### 関連

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
