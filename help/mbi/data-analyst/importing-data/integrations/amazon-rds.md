---
title: Connect Amazon RDS
description: RDS インスタンスを接続する手順を説明します。
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Connect [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] は、既に使い慣れたデータベースエンジンで実行されるマネージドデータベースサービスです。

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

[!DNL RDS] インスタンスに接続する手順は、使用するデータベースのタイプと、暗号化された接続（[`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md) など）を使用しているかどうかによって異なりますが、これが基本です。

## データベースへのアクセスを [!DNL Commerce Intelligence] に承認する

各データベースの資格情報ページ（**[!UICONTROL Manage Data** > **Integrations]**）に、R[!DNL RDS] を [!DNL Commerce Intelligence]:`54.88.76.97` および `34.250.211.151` に接続するために認証する必要がある IP アドレスを含むボックスが表示されます。 次に、IP アドレスボックスがハイライト表示された `MySQL credentials` ページを見てみましょう。

![](../../../assets/RDS_IP.png)

[!DNL Commerce Intelligence] が [!DNL RDS] インスタンスに正常に接続するには、AWS Management Console を介して適切なデータベースセキュリティグループにこれらの IP アドレスを追加する必要があります。 これらの IP アドレスは、既存のグループに追加することも、作成することもできます。重要なのは、[!DNL Commerce Intelligence] に接続するインスタンスへのアクセスをグループに許可されているということです。

[!DNL Commerce Intelligence] の IP アドレスを追加する場合は、アドレスの末尾に `/32` を追加して、それが正確な IP アドレスであ [!DNL Amazon] ことを示してください。 AWS インターフェイスは、これが必要であることを明確にします。

## [!DNL Commerce Intelligence] の `Linux` ユーザーの作成 {#linux}

>[!NOTE]
>
>この手順が必要になるのは、暗号化された接続を使用している場合のみです。 この方法については、使用しているデータベース（例：MySQL）の設定トピックを参照してください。 `Linux` ユーザーを使用すると、`SSH tunnel` を作成できます。これは、インターネットを介してデータを送信する最も安全な方法です。

## [!DNL Commerce Intelligence] 用のデータベースユーザーの作成

これは、使用しているデータベースに応じて手順が異なる、プロセスの一部です。 考え方は同じですが、データベースへのアクセスに使用する [!DNL Commerce Intelligence] 用のユーザーを作成します。 ユーザー [!DNL Commerce Intelligence] データベースを作成する手順については、使用しているデータベースの設定に関するトピックを参照してください。

## [!DNL Commerce Intelligence] に接続情報を入力

インスタンスへのアクセス権を [!DNL Commerce Intelligence] に付与し、ユーザーを作成したら、接続情報を [!DNL Commerce Intelligence] に入力する必要があります。

`MySQL`、`Microsoft SQL`、`PostgreSQL` の資格情報ページには、「**[!UICONTROL Add Integration]**」をクリックして、`Integrations` ページ（**[!UICONTROL Manage Data** > **Integrations]**）からアクセスできます。 統合のリストが表示されたら、使用しているデータベースのアイコンをクリックして、資格情報ページに移動します。 現在、必要な統合へのアクセス権がない場合は、Adobeアカウントチームにお問い合わせください。

接続の作成を完了するには、次の情報が必要です。

* RDS インスタンスのパブリックアドレス：これは、[!DNL AWS] 管理コンソールにあります。
* データベースインスタンスが使用するポート：一部のデータベースにはデフォルトのポートがあり、`Port` フィールドに自動的に入力されます。 この情報は、データベースの設定ドキュメントでも確認できます。
* [!DNL Commerce Intelligence] 用に作成したユーザーのユーザー名とパスワード。

暗号化された接続を使用している場合、データベース資格情報ページの「`Encrypted`」切替スイッチを「`Yes`」に変更します。 暗号化を設定するための追加フォームが表示されます。

![](../../../assets/sql-integration-encrypted-yes.png)


