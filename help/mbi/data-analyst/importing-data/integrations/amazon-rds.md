---
title: Amazon RDS の接続
description: RDS インスタンスを接続する手順を説明します。
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Amazon RDS の接続

Amazon Relational Database Services (RDS) は、既にご存知のデータベースエンジンで動作する管理データベースサービスです。 [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md), [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)、および [[!DNL PostgreSQ]](../integrations/postgresql.md).

RDS インスタンスを接続する手順は、使用しているデータベースの種類（各データベースの詳細な手順については、上のリンクを使用）や、暗号化された接続 ( [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)) ですが、次に基本事項を示します。

## 許可 [!DNL MBI] データベースにアクセスするには

資格情報ページ (**[!UICONTROL Manage Data** > **Integrations]**) をクリックすると、RDS を MBI に接続するために認証する必要がある IP アドレスが含まれているボックスが表示されます。 `54.88.76.97` および `34.250.211.151`. 以下に、 `MySQL credentials` ページで、「IP アドレス」ボックスがハイライト表示されています。

![](../../../assets/RDS_IP.png)

の場合 [!DNL MBI] RDS インスタンスに正常に接続するには、AWS管理コンソールから、これらの IP アドレスを適切なデータベースセキュリティグループに追加する必要があります。 これらの IP アドレスは、既存のグループに追加することも、新しい IP アドレスを作成することもできます。重要なのは、接続先のインスタンスへのアクセスがグループに許可されていることです [!DNL MBI].

を [!DNL MBI] IP アドレス、必ず `/32` を指定し、Amazonに対して、正確な IP アドレスであることを示します。 心配するな。AWSインターフェイスでは、これが必要であることが明確になります。

## の作成 `Linux` のユーザー [!DNL MBI] {#linux}

>[!NOTE]
>
>この手順は、暗号化された接続を使用する場合にのみ必要です。 この方法の手順については、使用しているデータベースの設定に関する記事を参照してください ( 例：MySQL)。 この `Linux` ユーザーが、 `SSH tunnel`：インターネット経由でデータを送信する最も安全な方法です。

## MBI 用のデータベースユーザーの作成

これは、使用しているデータベースに応じて、手順が異なるプロセスの一部です。 でも、アイデアは同じです。次のユーザーを作成します： [!DNL MBI] データベースへのアクセスに使用する データベースの作成手順 [!DNL MBI] ユーザーは、使用しているデータベースの設定記事に記載されています。

## MBI に接続情報を入力

君が許した後 [!DNL MBI] インスタンスにアクセスしてユーザーを作成しました。最後に、次の場所に接続情報を入力する必要があります。 [!DNL MBI].

次の資格情報ページ： `MySQL`, `Microsoft SQL`、および `PostgreSQL` が `Integrations` ページ (**[!UICONTROL Manage Data** > **Integrations]**) をクリックして **[!UICONTROL Add Integration]**. 統合のリストが表示されたら、使用しているデータベースのアイコンをクリックして資格情報ページに移動します。 現在、必要な統合にアクセスできない場合は、CSM に問い合わせてください。

接続の作成を完了するには、次の情報が必要です。

* RDS インスタンスのパブリックアドレス：これは、AWS管理コンソールで確認できます。
* データベースインスタンスが使用するポート：一部のデータベースにはデフォルトポートがあり、これは自動的に `Port` フィールドに入力します。 この情報は、データベースのセットアップドキュメントにも記載されています。
* 作成したユーザーのユーザー名とパスワード [!DNL MBI].

暗号化された接続を使用している場合は、 `Encrypted` データベース資格情報ページをに切り替えます。 `Yes`. これにより、暗号化を設定するための追加のフォームが表示されます。

![](../../../assets/sql-integration-encrypted-yes.png)

それだけだ！ RDS インスタンスの接続が完了しました。
