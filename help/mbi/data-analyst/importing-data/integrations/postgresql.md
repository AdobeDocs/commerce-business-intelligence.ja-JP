---
title: SSH トンネルを介した PostgreSQL の接続
description: SSH トンネルを介して PostgreSQL データベースをCommerce Intelligenceに接続する方法を説明します。
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# [!DNL PostgreSQL] 経由で [!DNL SSH Tunnel] に接続

[!DNL PostgreSQL] を使用して [!DNL Commerce Intelligence] データベースを `SSH tunnel` に接続するには、次の操作を行う必要があります。

1. [ [!DNL Commerce Intelligence]  公開鍵の取得](#retrieve)
1. [ [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可](#allowlist)
1. [ [!DNL Linux]  のユ  [!DNL Commerce Intelligence] ザーを作成](#linux)
1. [ [!DNL PostgreSQL]  のユ  [!DNL Commerce Intelligence] ザーを作成](#postgres)
1. [接続およびユーザー情報の入力先  [!DNL Commerce Intelligence]](#finish)

## [!DNL Commerce Intelligence] [!DNL public key] の取得 {#retrieve}

`public key` は、[!DNL Commerce Intelligence] [!DNL Linux] ユーザーの認証に使用されます。 ここでは、ユーザーを作成し、キーを読み込みます。

1. **[!UICONTROL Manage Data** > **Connections]** に移動し、「**[!UICONTROL Add a Data Source]**」をクリックします。
1. [!DNL PostgreSQL] アイコンをクリックします。
1. `PostgreSQL credentials` ページが開いたら、「`Encrypted`」切り替えスイッチを「`Yes`」に設定します。 `SSH` 設定フォームが表示されます。
1. `public key` はこのフォームの下にあります。

このページは、チュートリアルの最後まで開いたままにしておきます。次の節と最後に必要になります。

以下に、キーを取得するために [!DNL Commerce Intelligence] 内を移動する方法を示します。

![RJMetrics 公開鍵の取得 ](../../../assets/get-mbi-public-key.gif)

## [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可します {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 これは `54.88.76.97/32` ですが、`PostgreSQL` 資格情報ページにも表示されます。 上記のGIFの青いボックスを参照してください。

## [!DNL Linux] 用の [!DNL Commerce Intelligence] ユーザーの作成 {#linux}

リアルタイム（または頻繁に更新される）のデータが含まれている限り、実稼動マシンまたはセカンダリマシンを使用できます。 [ サーバーへの接続権が保持されている限り、好きなように ](../../../administrator/account-management/restrict-db-access.md) このユーザーを制限 [!DNL PostgreSQL] することができます。

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
```

>[!IMPORTANT]
>
>サーバーに関連付けられている `sshd\_config` ファイルが既定のオプションに設定されていない場合は、特定のユーザーのみがサーバーにアクセスできます。これにより、[!DNL Commerce Intelligence] への接続に成功できなくなります。 このような場合、rjmetric ユーザーにサーバーへのアクセスを許可するには、`AllowUsers` などのコマンドを実行する必要があります。

## [!DNL Commerce Intelligence] [!DNL Postgres] ユーザーの作成 {#postgres}

組織では別のプロセスが必要になる場合がありますが、このユーザーを作成する最も簡単な方法は、権限を付与する権限を持つユーザーとして Postgres にログインしたときに次のクエリを実行することです。 また、ユーザーは、アクセス権が付与され [!DNL Commerce Intelligence] スキーマを所有している必要があります。

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

`secure password` を、SSH パスワードとは異なる独自のセキュアなパスワードに置き換えます。 また、`database name` と `schema name` をデータベース内の適切な名前に置き換える必要があります。

複数のデータベースまたはスキーマを接続する場合は、必要に応じてこのプロセスを繰り返します。

## [!DNL Commerce Intelligence] への接続およびユーザー情報の入力 {#finish}

まとめるには、接続とユーザー情報を [!DNL Commerce Intelligence] に入力する必要があります。 [!DNL PostgreSQL] 資格情報ページを開いたままにしましたか？ そうでない場合は、**[!UICONTROL Manage Data > Connections]** に移動して「**[!UICONTROL Add a Data Source]**」をクリックし、次に「[!DNL PostgreSQL]」アイコンをクリックします。 「`Encrypted`」トグルを `Yes` に設定することを忘れないでください。

このページに、`Database Connection` のセクションから始まる次の情報を入力します。

* `Username`:RJMetrics Postgres ユーザー名（rjmetric にする）
* `Password`:RJMetrics Postgres パスワード
* `Port`：サーバー上の PostgreSQL ポート（デフォルトでは 5432）
* `Host`: 127.0.0.1

`SSH Connection` の下：

* `Remote Address`:SSH で接続するサーバーの IP アドレスまたはホスト名
* `Username`:SSH ログイン名（rjmetric）
* `SSH Port`：サーバーの SSH ポート（デフォルトでは 22）

完了したら、**保存してテスト** をクリックして設定を完了します。

### 関連

* [ 統合の再認証 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
