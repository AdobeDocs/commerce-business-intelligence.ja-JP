---
title: cPanel を使用した MySQL の接続
description: cPanel を使用して MySQL を接続する方法を説明します。
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 1%

---

# 接続 [!DNL MySQL] 経由 [!DNL cPanel]

* [の作成 [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーイン [!DNL cPanel]](#cpanel)
* [次の場所に接続とユーザー情報を入力 [!DNL Commerce Intelligence]](#finish)

## ジャンプ先

* [[!DNL MySQL] SSH トンネル経由](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] 直接接続経由](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] では、データを保護するために SSH などの暗号化を使用することをお勧めします。 これがオプションでない場合、直接接続できます [!DNL Commerce Intelligence] をデータベースに追加します。

このトピックでは、 [!DNL MySQL] データベースへ [!DNL Commerce Intelligence] using [!DNL cPanel]. このプロセスは、接続にも使用できます [!DNL Adobe Commerce] 、およびその他の MySQL ベースの e コマースデータベースを [!DNL Commerce Intelligence].

1. の作成 [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーイン [!DNL cPanel]
1. 次の場所に接続とユーザー情報を入力 [!DNL Commerce Intelligence]

基本を学ぶ.

## の作成 [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーイン [!DNL cPanel] {#cpanel}

1. にログインします。 [!DNL cPanel] ホスティングプロバイダー経由。
1. クリック **[!UICONTROL [!DNL MySQL] Databases]**&#x200B;に含まれています。 `Database` 」セクションに入力します。
1. 下にスクロールして、 `Add New User` セクションを開き、次の用のユーザーを作成します。 [!DNL Commerce Intelligence]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. クリック **[!UICONTROL Create User]**.
1. ユーザーを作成したら、そのユーザーをデータベースに関連付ける必要があります。 に戻ります。 `Add New User` セクション — 設定を参照 `Add User to Database?` それがあなたが必要とするものです。
1. Adobe Analytics の `User` このセクションのドロップダウンで、作成したユーザーを選択します。
1. Adobe Analytics の `Database` このセクションのドロップダウンで、接続先のデータベースを選択します [!DNL Commerce Intelligence].
1. クリック **[!UICONTROL Add]**.
1. 権限のチェックリストが表示されたら、の横にあるチェックボックスをオンにします。 `SELECT`  — これだけです [!DNL Commerce Intelligence] は、データベースに接続する必要があります。

## 次の場所に接続とユーザー情報を入力 [!DNL Commerce Intelligence] {#finish}

まとめるには、接続とユーザー情報を次のように入力する必要があります。 [!DNL Commerce Intelligence]. あなたは [!DNL MySQL] 認証情報ページを開きますか？ そうでない場合は、に移動します。 **[!UICONTROL Manage Data** > **Connections]** をクリックします。 **[!UICONTROL Add New Data Source]**&#x200B;を、 [!DNL MySQL] アイコン。

このページの `Database Connection` セクション：

* `Username`：のユーザー名 [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー
* `Password`：のパスワード [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー
* `Port`：サーバー上の MySQL のポート (`3306` （デフォルト）
* `Host`：のパブリックアドレス `MySQL` server [!DNL Commerce Intelligence] に接続します。 これは通常、ログインに使用する URL です `[!DNL cPanel]`.

を使用している場合、 [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)を使用する場合は、暗号化情報を入力する必要があります。 を設定します。 `Encrypted` 切り替える `Yes` をクリックしてフォームを表示します。

* `Connection Type`：これをに設定します。 `SSH Tunnel`
* `Remote Address`：サーバーの IP アドレスまたはホスト名 [!DNL Commerce Intelligence] ～に通じる
* `Username`：のユーザー名 [!DNL Commerce Intelligence] `SSH (Linux)` ユーザー、詳しくは、 [instructions](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) （まだの場合）、この方法を使用する方法について説明します。
* `SSH Port`：サーバー上の SSH ポート (`22` （デフォルト）

完了したら、「 **[!UICONTROL Save & Test]** をクリックして設定を完了します。

## 関連：

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
