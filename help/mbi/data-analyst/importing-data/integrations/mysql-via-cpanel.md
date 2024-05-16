---
title: cPanel を介した MySQL の接続
description: cPanel を使用して MySQL に接続する方法を説明します。
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# 接続 [!DNL MySQL] 経由 [!DNL cPanel]

* [を作成 [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー： [!DNL cPanel]](#cpanel)
* [接続およびユーザー情報の入力先 [!DNL Commerce Intelligence]](#finish)

## 移動先

* [[!DNL MySQL] ssh トンネル経由](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] 直接接続による](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] ssh またはその他の形式の暗号化を使用してデータを保護することをお勧めします。 このオプションが選択できない場合でも、直接接続できます [!DNL Commerce Intelligence] をデータベースに追加するには、このトピックの手順を使用します。

このトピックでは、を直接接続する方法について説明します [!DNL MySQL] データベース先 [!DNL Commerce Intelligence] 使用 [!DNL cPanel]. このプロセスを使用してを接続することもできます [!DNL Adobe Commerce] およびその他の MySQL ベースの e コマースデータベースのすべて [!DNL Commerce Intelligence].

1. を作成 [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー： [!DNL cPanel]
1. 接続およびユーザー情報の入力先 [!DNL Commerce Intelligence]

今すぐ始めましょう。

## の作成 [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー： [!DNL cPanel] {#cpanel}

1. へのログイン [!DNL cPanel] ホスティングプロバイダーを使用。
1. クリック **[!UICONTROL [!DNL MySQL] Databases]**、にあります。 `Database` セクション。
1. にスクロール ダウンします。 `Add New User` セクションと用のユーザーの作成 [!DNL Commerce Intelligence]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. クリック **[!UICONTROL Create User]**.
1. ユーザーを作成したので、次はデータベースに関連付ける必要があります。 に戻る `Add New User` セクション – の設定を参照してください `Add User to Database?` それが必要なものです。
1. が含まれる `User` このセクションのドロップダウンで、作成したユーザーを選択します。
1. が含まれる `Database` このセクションのドロップダウンで、接続先のデータベースを選択します [!DNL Commerce Intelligence].
1. クリック **[!UICONTROL Add]**.
1. 権限のチェックリストが表示されたら、の横にあるチェックボックスをオンにします。 `SELECT`  – これだけです [!DNL Commerce Intelligence] データベースに接続する必要があります。

## 接続およびユーザー情報の入力 [!DNL Commerce Intelligence] {#finish}

最後に、接続とユーザー情報をに入力する必要があります。 [!DNL Commerce Intelligence]. を残しましたか [!DNL MySQL] 資格情報ページが開かれますか？ そうでない場合は、に移動します **[!UICONTROL Manage Data** > **Connections]** をクリックして、 **[!UICONTROL Add New Data Source]**&#x200B;を選択し、続いて [!DNL MySQL] アイコン。

このページに次の情報を `Database Connection` セクション：

* `Username`：のユーザー名 [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー
* `Password`：のパスワード [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー
* `Port`：サーバー上の MySQL のポート（`3306` デフォルト）
* `Host`：のパブリックアドレス `MySQL` サーバー [!DNL Commerce Intelligence] はに接続します。 これは通常、ログインに使用する URL です `[!DNL cPanel]`.

を使用する場合 [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)：暗号化情報を入力する必要があります。 を `Encrypted` 切り替え `Yes` フォームを表示します。

* `Connection Type`：これをに設定 `SSH Tunnel`
* `Remote Address`：サーバーの IP アドレスまたはホスト名 [!DNL Commerce Intelligence] ～にトンネルを通す
* `Username`：のユーザー名 [!DNL Commerce Intelligence] `SSH (Linux)` ユーザー、を参照 [指示](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) （まだ行っていない場合は、これを行う方法）
* `SSH Port`：サーバーの SSH ポート（`22` デフォルト）

完了したら、 **[!UICONTROL Save & Test]** をクリックして設定を完了します。

## 関連：

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
