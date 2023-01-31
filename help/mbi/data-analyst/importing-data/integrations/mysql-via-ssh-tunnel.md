---
title: SSH トンネルを介した MySQL の接続
description: SSH トンネルを介した MySQL の接続方法を説明します。
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# 接続 `MySQL` 経由 `SSH Tunnel`

* [の取得 [!DNL MBI] 公開鍵](#retrieve)
* [次へのアクセスを許可： [!DNL MBI] IP アドレス](#allowlist)
* [用の Linux ユーザーの作成 [!DNL MBI]](#linux)
* [MySQL ユーザーの作成 [!DNL MBI]](#mysql)
* [接続とユーザー情報をに入力します。 [!DNL MBI]](#finish)

## ジャンプ先

* `MySQL via SSH tunnel`
* [&#39;MySQL&#39;](../integrations/mysql-via-a-direct-connection.md)
* [&#39;MySQL&#39;](../integrations/mysql-via-cpanel.md)

次の手順で `MySQL` データベースへ [!DNL MBI] 経由 `SSH tunnel`を使用する場合、あなた（または技術を持っていない場合はチーム）は、次のいくつかの操作を実行する必要があります。

1. の取得 [!DNL MBI] `public key`
1. 次へのアクセスを許可： [!DNL MBI] `IP address`
1. の作成 `Linux` のユーザー [!DNL MBI]
1. の作成 `MySQL` のユーザー [!DNL MBI]
1. 接続とユーザー情報をに入力します。 [!DNL MBI]

それは聞こえるほど複雑ではない。 始めましょう。

## の取得 [!DNL MBI] 公開鍵 {#retrieve}

この `public key` は、 [!DNL MBI] `Linux` ユーザー。 次の節では、ユーザーを作成し、キーをインポートします。

1. に移動します。 **[!UICONTROL Manage Data** > **Connections]** をクリックし、 **[!UICONTROL Add New Data Source]**.
1. 次をクリック： `MySQL` アイコン
1. 次の期間の後 `MySQL credentials` ページを開く、 `Encrypted` 切り替える `Yes`. これにより、SSH セットアップフォームが表示されます。
1. この `public key` はこのフォームの下に配置されています。

このページはチュートリアル全体で開いたままにしておきます。次のセクションで、最後にこのページを開く必要があります。

少し迷ったら、次の操作を実行します [!DNL MBI] キーを取得するには：

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## 次へのアクセスを許可： [!DNL MBI] IP アドレス {#allowlist}

接続が成功するには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 これらは `54.88.76.97` および `34.250.211.151` しかし、彼らはまた `MySQL credentials` ページ。 上のGIFの青いボックスが見える それだ！

## の作成 `Linux` のユーザー [!DNL MBI] {#linux}

リアルタイム（または頻繁に更新される）データが含まれる限り、実稼動マシンまたはセカンダリマシンにすることができます。 次のことが可能です。 [このユーザーを制限](../../../administrator/account-management/restrict-db-access.md) どのようにしても、 `MySQL` サーバー。

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
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>この `sshd\_config` サーバーに関連付けられたファイルがデフォルトのオプションに設定されていない場合、特定のユーザーだけがサーバーにアクセスできます。これにより、 [!DNL MBI]. このような場合、 `AllowUsers` 許す `rjmetric` ユーザーがサーバーにアクセスできること。

## の作成 `MySQL` のユーザー [!DNL MBI] {#mysql}

組織では異なるプロセスが必要になる場合がありますが、このユーザーを作成する最も簡単な方法は、にログインしたときに次のクエリを実行することです `MySQL` 権限を付与する権限を持つユーザーとして：

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

置換 `secure password here` セキュリティで保護されたパスワードを使用します。 `SSH` パスワード。

このユーザーが特定のデータベース、テーブル、または列のデータにアクセスできないように制限するには、代わりに、許可したデータに対するアクセスのみを許可する GRANT クエリを実行します。

## 次の場所に接続とユーザー情報を入力 [!DNL MBI] {#finish}

まとめるには、接続とユーザー情報を次のように入力する必要があります。 [!DNL MBI]. あなたは `MySQL credentials` ページが開いているか そうでない場合は、に移動します。 **[!UICONTROL Data** > **Connections]** をクリックし、 **[!UICONTROL Add New Data Source]**、 MySQL アイコンの順にクリックします。 忘れずに `Encrypted` 切り替える `Yes`.

このページに、「データベース接続」セクションから始まる次の情報を入力します。

* `Username`:のユーザー名 [!DNL MBI] MySQL ユーザー
* `Password`:のパスワード [!DNL MBI] MySQL ユーザー
* `Port`:サーバー上の MySQL のポート（デフォルトでは 3306）
* `Host` デフォルトでは、localhost になります。 一般的に、MySQL サーバーのバインドアドレスの値になります（デフォルトはです）。 `127.0.0.1 (localhost)`は、一部のローカルネットワークアドレス ( 例： `192.168.0.1`) またはサーバーのパブリック IP アドレス。

   この値は、 `my.cnf` ファイル ( 通常は `/etc/my.cnf`) を `\[mysqld\]`. バインドアドレス行がそのファイルでコメントアウトされている場合、外部接続の試行からサーバーが保護されます。

内 `SSH Connection` セクション：

* `Remote Address`:サーバーの IP アドレスまたはホスト名 [!DNL MBI] ～に通じる
* `Username`:のユーザー名 [!DNL MBI] SSH(Linux) ユーザー
* `SSH Port`:サーバー上の SSH ポート（デフォルトでは 22）

それだ！ 完了したら、「 **[!UICONTROL Save & Test]** をクリックして設定を完了します。

## 関連：

* [統合の再認証](https://support.magento.com/hc/en-us/articles/360016733151)
