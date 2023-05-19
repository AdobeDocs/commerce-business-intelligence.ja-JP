---
title: 接続中 [!DNL MySQL] SSH トンネル経由
description: 接続方法の詳細 [!DNL MySQL] SSH トンネル経由。
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 0%

---

# 接続 [!DNL MySQL] 経由 [!DNL SSH Tunnel]

* [の取得 [!DNL Commerce Intelligence] 公開鍵](#retrieve)
* [次へのアクセスを許可： [!DNL Commerce Intelligence] IP アドレス](#allowlist)
* [用の Linux ユーザーの作成 [!DNL Commerce Intelligence]](#linux)
* [の作成 [!DNL MySQL] のユーザー [!DNL Commerce Intelligence]](#mysql)
* [接続とユーザー情報をに入力します。 [!DNL Commerce Intelligence]](#finish)

## ジャンプ先

* [[!DNL MySQL] 経由 ](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] 経由 [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

次の手順で [!DNL MySQL] データベースへ [!DNL Commerce Intelligence] 経由 `SSH tunnel`を使用する場合は、次のいくつかの操作を行う必要があります。

1. の取得 [!DNL Commerce Intelligence] `public key`
1. 次へのアクセスを許可： [!DNL Commerce Intelligence] `IP address`
1. の作成 `Linux` のユーザー [!DNL Commerce Intelligence]
1. の作成 `MySQL` のユーザー [!DNL Commerce Intelligence]
1. 接続とユーザー情報をに入力します。 [!DNL Commerce Intelligence]


## の取得 [!DNL Commerce Intelligence] 公開鍵 {#retrieve}

この `public key` は、 [!DNL Commerce Intelligence] `Linux` ユーザー。 次の節では、ユーザーを作成し、キーをインポートします。

1. に移動します。 **[!UICONTROL Manage Data** > **Connections]** をクリックし、 **[!UICONTROL Add New Data Source]**.
1. 次をクリック： `MySQL` アイコン
1. 次の期間の後 `MySQL credentials` ページを開く、 `Encrypted` 切り替える `Yes`. SSH セットアップフォームが表示されます。
1. この `public key` はこのフォームの下に配置されています。

このページはチュートリアル全体で開いたままにしておきます。次のセクションで、最後にこのページを開く必要があります。

ナビゲーションの方法を次に示します [!DNL Commerce Intelligence] キーを取得するには：

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## 次へのアクセスを許可： [!DNL Commerce Intelligence] IP アドレス {#allowlist}

接続が成功するには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 これらは `54.88.76.97` および `34.250.211.151` しかし彼らもまた `MySQL credentials` ページ。 上記のGIFの青いボックスを確認します。

## の作成 [!DNL Linux] のユーザー [!DNL Commerce Intelligence] {#linux}

リアルタイム（または頻繁に更新される）データが含まれる限り、実稼動マシンまたはセカンダリマシンにすることができます。 次のことが可能です。 [このユーザーを制限](../../../administrator/account-management/restrict-db-access.md) どのようにしても、 `MySQL` サーバー。

1. 新しいユーザーを追加するには、次のコマンドを root として [!DNL Linux] サーバ：

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. を記憶する `public key` 最初の部分で検索したの？ ユーザーがデータベースに確実にアクセスできるようにするには、キーを `authorized\_keys`.

   キー全体を `authorized\_keys` ファイルの内容は次のとおりです。

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. ユーザーの作成を完了するには、 `/home/rjmetric` 経由でのアクセスを許可するディレクトリ `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>この `sshd\_config` サーバーに関連付けられたファイルがデフォルトのオプションに設定されていない場合は、特定のユーザーだけがサーバーにアクセスできます。これにより、 [!DNL Commerce Intelligence]. このような場合、 `AllowUsers` 許す `rjmetric` ユーザーがサーバーにアクセスできること。

## の作成 [!DNL MySQL] のユーザー [!DNL Commerce Intelligence] {#mysql}

組織では異なるプロセスが必要になる場合がありますが、このユーザーを作成する最も簡単な方法は、にログインしたときに次のクエリを実行することです [!DNL MySQL] 権限を付与する権限を持つユーザーとして：

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

置換 `secure password here` セキュリティで保護されたパスワードを使用します。 `SSH` パスワード。

このユーザーが特定のデータベース、テーブル、または列のデータにアクセスできないように制限するには、代わりに、許可したデータに対するアクセスのみを許可する GRANT クエリを実行します。

## 次の場所に接続とユーザー情報を入力 [!DNL Commerce Intelligence] {#finish}

まとめるには、接続とユーザー情報を次のように入力する必要があります。 [!DNL Commerce Intelligence]. あなたは `MySQL credentials` ページが開いているか そうでない場合は、に移動します。 **[!UICONTROL Data** > **Connections]** をクリックし、 **[!UICONTROL Add New Data Source]**、 [!DNL MySQL] アイコン 忘れずに `Encrypted` 切り替える `Yes`.

このページに、以下の情報を入力します。 `Database Connection` セクション：

* `Username`:のユーザー名 [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー
* `Password`:のパスワード [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー
* `Port`: [!DNL MySQL] サーバー上のポート（デフォルトは 3306）
* `Host` デフォルトでは、localhost です。 一般に、バインドアドレスの値は [!DNL MySQL] サーバー（デフォルトは） `127.0.0.1 (localhost)`は、一部のローカルネットワークアドレス ( 例： `192.168.0.1`) またはサーバーのパブリック IP アドレス。

   この値は、 `my.cnf` 次の場所にあるファイル： `/etc/my.cnf`) を `\[mysqld\]`. バインドアドレス行がそのファイルでコメントアウトされている場合、外部接続の試行からサーバーが保護されます。

内 `SSH Connection` セクション：

* `Remote Address`:サーバーの IP アドレスまたはホスト名 [!DNL Commerce Intelligence] ～に通じる
* `Username`:のユーザー名 [!DNL Commerce Intelligence] SSH ([!DNL Linux]) ユーザー
* `SSH Port`:サーバー上の SSH ポート（デフォルトでは 22）

完了したら、「 **[!UICONTROL Save & Test]** をクリックして設定を完了します。

## 関連：

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
