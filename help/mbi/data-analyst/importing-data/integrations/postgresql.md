---
title: SSH トンネルを介した PostgreSQL の接続
description: PostgreSQL データベースをに接続する方法を説明します。 [!DNL MBI] SSH トンネルを介して送信されます。
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 0%

---

# 接続 `PostgreSQL` 経由 `SSH` トンネル

次の手順で `PostgreSQL` データベースへ [!DNL MBI] 経由 `SSH tunnel`を使用する場合は、自分（または技術を持っていない場合はチーム）が次のいくつかの操作を実行する必要があります。

1. [の取得 [!DNL MBI] 公開鍵](#retrieve)
1. [次へのアクセスを許可： [!DNL MBI] IP アドレス](#allowlist)
1. [Linux の作成](#linux)
1. [用の Postgres ユーザーの作成 [!DNL MBI] ](#postgres)
1. [MBI に接続とユーザー情報を入力](#finish)

それは聞こえるほど複雑ではない。 はじめに。

## の取得 [!DNL MBI] `public key` {#retrieve}

この `public key` は、 [!DNL MBI] Linux®ユーザー。 次の節では、ユーザーを作成し、キーをインポートします。

1. に移動します。 **[!UICONTROL Manage Data** > **Connections]** をクリックし、 **[!UICONTROL Add a Data Source]**.
1. 次をクリック： `PostgreSQL` アイコン
1. 次の期間の後 `PostgreSQL credentials` ページを開く、 `Encrypted` 切り替える `Yes`. これにより、 `SSH` 設定フォーム。
1. この `public key` はこのフォームの下に配置されています。

このページはチュートリアル全体で開いたままにしておきます。次のセクションで、最後にこのページを開く必要があります。

少し迷ったら、次の操作を実行します。 [!DNL MBI] キーを取得するには：

![RJMetrics 公開鍵の取得](../../../assets/get-mbi-public-key.gif)

## 次へのアクセスを許可： [!DNL MBI] IP アドレス {#allowlist}

接続が成功するには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 これは `54.88.76.97/32`ですが、それはまた、 `PostgreSQL` 認証情報ページ。 上のGIFの青いボックスが見える それだ！

## の作成 `Linux` のユーザー [!DNL MBI] {#linux}

リアルタイム（または頻繁に更新される）データが含まれる限り、実稼動マシンまたはセカンダリマシンにすることができます。 次のことが可能です。 [このユーザーを制限](../../../administrator/account-management/restrict-db-access.md) PostgreSQL サーバに接続する権限を保持している限り、好きなように。

1. 新しいユーザーを追加するには、次のコマンドを root として `Linux` サーバ：

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. を記憶する `public key` 最初の部分で取り戻したの？ ユーザーがデータベースに確実にアクセスできるようにするには、キーを `authorized\_keys`.

   キー全体を `authorized\_keys` ファイルの内容は次のとおりです。

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. ユーザーの作成を完了するには、 `/home/rjmetric` 経由でのアクセスを許可するディレクトリ `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
```

>[!IMPORTANT]
>
>この `sshd\_config` サーバーに関連付けられたファイルがデフォルトのオプションに設定されていない場合は、特定のユーザーだけがサーバーにアクセスできます。これにより、 [!DNL MBI]. このような場合、 `AllowUsers` rjmetric ユーザーにサーバーへのアクセスを許可する。

## の作成 [!DNL MBI] Postgres ユーザー {#postgres}

組織では異なるプロセスが必要になる場合がありますが、このユーザーを作成する最も簡単な方法は、権限を付与する権限を持つユーザーとして Postgres にログインしたときに、次のクエリを実行することです。 ユーザーは、 [!DNL MBI] はへのアクセス権を付与されています。

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

置換 `secure password` セキュリティで保護された独自のパスワードを使用します。SSH パスワードとは異なる場合があります。 また、 `database name` および `schema name` を、データベース内の適切な名前に置き換えます。

複数のデータベースまたはスキーマを接続する場合は、必要に応じてこのプロセスを繰り返します。

## 次の場所に接続とユーザー情報を入力 [!DNL MBI] {#finish}

まとめるには、接続とユーザー情報を次のように入力する必要があります。 [!DNL MBI]. PostgreSQL 資格情報ページを開いたままにしましたか？ そうでない場合は、に移動します。 **[!UICONTROL Manage Data > Connections]** をクリックし、 **[!UICONTROL Add a Data Source]**、PostgreSQL アイコンの順にクリックします。 忘れずに `Encrypted` 切り替える `Yes`.

このページに、「データベース接続」セクションから始まる次の情報を入力します。

* `Username`:RJMetrics Postgres ユーザー名（rjmetric である必要があります）
* `Password`:RJMetrics Postgres パスワード
* `Port`:サーバー上の PostgreSQL ポート（デフォルトは 5432）
* `Host`: 127.0.0.1

の下 `SSH Connection`:

* `Remote Address`:SSH で接続するサーバーの IP アドレスまたはホスト名
* `Username`:SSH ログイン名（rjmetric である必要があります）
* `SSH Port`:サーバー上の SSH ポート（デフォルトでは 22）

それだ！ 完了したら、「 **保存してテスト** をクリックして設定を完了します。

### 関連

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
