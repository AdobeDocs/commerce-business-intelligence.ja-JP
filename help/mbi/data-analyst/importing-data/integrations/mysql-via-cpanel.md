---
title: cPanel を使用した MySQL の接続
description: cPanel を使用して MySQL を接続する方法を説明します。
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# cPanel を使用した MySQL の接続

* [の作成 [!DNL MBI] cPanel の MySQL ユーザー](#cpanel)
* [MBI に接続とユーザー情報を入力](#finish)

## ジャンプ先

* [SSH トンネル経由の MySQL](../integrations/mysql-via-ssh-tunnel.md)
* [直接接続を介した MySQL](../integrations/mysql-via-a-direct-connection.md)

* **`MySQL via cPanel`**

>[!IMPORTANT]
>
>データの保護には、SSH などの暗号化を使用することを強くお勧めします。 これがオプションでない場合、直接接続できます [!DNL MBI] をデータベースに追加する場合は、この記事の手順を使用します。

この記事では、MySQL データベースを [!DNL MBI] cPanel を使用」と表示されます。 このプロセスは、接続にも使用できます [!DNL Magento] 、およびその他の MySQL ベースの e コマースデータベースを [!DNL MBI].

1. の作成 [!DNL MBI] の MySQL ユーザー `cPanel`
1. 次の場所に接続とユーザー情報を入力 [!DNL MBI]

はじめに。

## の作成 [!DNL MBI] の MySQL ユーザー `cPanel` {#cpanel}

1. ログイン先 [`cPanel`](../../../data-analyst/importing-data/integrations/mysql-via-cpanel.md) ホスティングプロバイダー経由。
1. クリック **[!UICONTROL MySQL Databases]**( `Database` 」セクションに入力します。
1. 下にスクロールして `Add New User` セクションを開き、次の用のユーザーを作成します。 [!DNL MBI]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. クリック **[!UICONTROL Create User]**.
1. ユーザーを作成したら、そのユーザーをデータベースに関連付ける必要があります。 に戻ります。 `Add New User` セクション — 設定を参照 `Add User to Database?` それが私たちに必要なことです。
1. 内 `User` このセクションのドロップダウンで、作成したユーザーを選択します。
1. 内 `Database` このセクションのドロップダウンで、接続先のデータベースを選択します [!DNL MBI].
1. クリック **[!UICONTROL Add]**.
1. 権限のチェックリストが表示されたら、の横にあるチェックボックスをオンにします。 `SELECT`  — これだけです [!DNL MBI] は、データベースに接続する必要があります。

## 次の場所に接続とユーザー情報を入力 [!DNL MBI] {#finish}

まとめるには、接続とユーザー情報を次のように入力する必要があります。 [!DNL MBI]. MySQL 資格情報ページを開いたままにしましたか？ そうでない場合は、に移動します。 **[!UICONTROL Manage Data** > **Connections]** をクリックし、 **[!UICONTROL Add New Data Source]**、 MySQL アイコンの順にクリックします。

このページの `Database Connection` セクション：

* `Username`:のユーザー名 [!DNL MBI] MySQL ユーザー
* `Password`:のパスワード [!DNL MBI] MySQL ユーザー
* `Port`:サーバー上の MySQL のポート (`3306` （デフォルト）
* `Host`:のパブリックアドレス `MySQL` server [!DNL MBI] がに接続します。 これは通常、ログインに使用する URL です `cPanel`.

を使用している場合、 [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)を使用する場合は、暗号化情報も入力する必要があります。 を `Encrypted` 切り替える `Yes` をクリックしてフォームを表示します。

* `Connection Type`:これを `SSH Tunnel`
* `Remote Address`:サーバーの IP アドレスまたはホスト名 [!DNL MBI] ～に通じる
* `Username`:のユーザー名 [!DNL MBI] `SSH (Linux)` ユーザー： [説明](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) （まだの場合）
* `SSH Port`:サーバーの SSH ポート (`22` （デフォルト）

それだ！ 完了したら、「 **[!UICONTROL Save & Test]** をクリックして設定を完了します。

## 関連：

* [統合の再認証](https://support.magento.com/hc/en-us/articles/360016733151)
