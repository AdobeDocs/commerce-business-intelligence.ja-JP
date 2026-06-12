---
title: cPanelを介したMySQLの接続
description: cPanelを介してMySQLを接続する方法を説明します。
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
TQID: https://experienceleague.adobe.com/Ou9gOlYKFuoYQHTi7zhyecvfGlKEKF2eRSr5vctsW1s
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 3a6b80d7bcfa5db4d86ab4da81239e3ea804f6ad
workflow-type: tm+mt
source-wordcount: 400
ht-degree: 0%

---

# [!DNL cPanel]経由で[!DNL MySQL]に接続

* [&#x200B; [!DNL cPanel]で [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーを作成](#cpanel)
* [&#x200B; [!DNL Commerce Intelligence]への接続とユーザー情報の入力](#finish)

## に移動

* [SSH トンネル経由で[!DNL MySQL]](../integrations/mysql-via-ssh-tunnel.md)
* [直接接続による[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe]では、データを保護するためにSSHまたはその他の形式の暗号化を使用することをお勧めします。 このオプションを使用しない場合でも、このトピックの手順を使用して、[!DNL Commerce Intelligence]をデータベースに直接接続できます。

このトピックでは、[!DNL cPanel]を使用して[!DNL MySQL] データベースを[!DNL Commerce Intelligence]に直接接続する方法について説明します。 このプロセスは、[!DNL Adobe Commerce]やその他のMySQL ベースのe コマースデータベースを[!DNL Commerce Intelligence]に接続するためにも使用できます。

1. [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーを[!DNL cPanel]に作成します
1. 接続とユーザー情報を[!DNL Commerce Intelligence]に入力してください

今すぐ始める。

## [!DNL cPanel]で[!DNL Commerce Intelligence] [!DNL MySQL] ユーザーを作成しています {#cpanel}

1. ホスティングプロバイダーを介して[!DNL cPanel]にログインします。
1. 「`Database`」セクションにある「**[!UICONTROL [!DNL MySQL] Databases]**」をクリックします。
1. `Add New User` セクションまでスクロールして、[!DNL Commerce Intelligence]のユーザーを作成します。

   ユーザーフォームの作成を示す![cPanel MySQL データベースインターフェイス &#x200B;](../../../assets/create-mbi-mysql-user-cpanel.png)

1. **[!UICONTROL Create User]**&#x200B;をクリックします。
1. ユーザーを作成したら、そのユーザーをデータベースに関連付ける必要があります。 「`Add New User`」セクションに戻ります。「`Add User to Database?`」の設定を参照してください。
1. このセクションの`User` ドロップダウンで、作成したユーザーを選択します。
1. このセクションの`Database` ドロップダウンで、[!DNL Commerce Intelligence]に接続するデータベースを選択します。
1. **[!UICONTROL Add]**&#x200B;をクリックします。
1. 権限のチェックリストが表示されたら、`SELECT`の横にあるチェックボックスをオンにします。これは、[!DNL Commerce Intelligence]がデータベースに接続する必要があるすべてです。

## 接続とユーザー情報を[!DNL Commerce Intelligence]に入力しています {#finish}

最後に、接続とユーザー情報を[!DNL Commerce Intelligence]に入力する必要があります。 [!DNL MySQL]資格情報ページを開いたままにしましたか？ そうでない場合は、**[!UICONTROL Manage Data** > **Connections]**&#x200B;に移動して&#x200B;**[!UICONTROL Add New Data Source]**&#x200B;をクリックし、[!DNL MySQL] アイコンをクリックします。

このページの`Database Connection` セクションに次の情報を入力します。

* `Username`: [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーのユーザー名
* `Password`: [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーのパスワード
* `Port`: サーバー上のMySQLのポート （`3306` デフォルト）
* `Host`: `MySQL` サーバー[!DNL Commerce Intelligence]の公開アドレスが接続しています。 これは通常、`[!DNL cPanel]`へのログインに使用するURLです。

[`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)を使用している場合、暗号化情報を入力する必要があります。 `Encrypted` トグルを`Yes`に設定して、フォームを表示します。

* `Connection Type`：これを`SSH Tunnel`に設定
* `Remote Address`: サーバー[!DNL Commerce Intelligence]のIP アドレスまたはホスト名は、にトンネルされます
* `Username`: [!DNL Commerce Intelligence] `SSH (Linux)` ユーザーのユーザー名。まだ使用していない場合は、[手順](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md)を参照してください）
* `SSH Port`: サーバー上のSSH ポート （`22` デフォルト）

完了したら、**[!UICONTROL Save & Test]**&#x200B;をクリックして設定を完了します。

>[!NOTE]
>
>SSH トンネルを使用する場合は、登録、更新、エラーメッセージ、およびトラブルシューティングについては、[SSH ホストキー検証](ssh-host-key-verification.md)を参照してください。

## 関連 {#related}

* [SSH ホスト キーの検証](ssh-host-key-verification.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
