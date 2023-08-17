---
title: Amazon RDS の接続
description: RDS インスタンスを接続する手順を説明します。
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# 接続 [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] は、おそらく既にご存知のデータベースエンジン上で動作する、管理対象のデータベースサービスです。

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

接続の手順 [!DNL RDS] インスタンスは、使用しているデータベースの種類と、暗号化された接続 ( [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)) ですが、以下に基本事項を示します。

## 許可 [!DNL Commerce Intelligence] データベースにアクセスするには

認証情報ページ (**[!UICONTROL Manage Data** > **Integrations]**) をクリックすると、R への接続を許可する必要がある IP アドレスが記載されたボックスが表示されます[!DNL RDS] から [!DNL Commerce Intelligence]: `54.88.76.97` および `34.250.211.151`. 以下に、 `MySQL credentials` 「IP アドレス」ボックスがハイライト表示されたページ

![](../../../assets/RDS_IP.png)

の場合 [!DNL Commerce Intelligence] を正常に接続するには、 [!DNL RDS] 例えば、AWS管理コンソールから、これらの IP アドレスを適切なデータベースセキュリティグループに追加する必要があります。 これらの IP アドレスは、既存のグループに追加することも、既存のグループを作成することもできます。重要なのは、接続先のインスタンスへのアクセスをグループが許可されていることです [!DNL Commerce Intelligence].

を追加する場合、 [!DNL Commerce Intelligence] IP アドレスを使用する場合は、必ず `/32` を指定するアドレスの末尾に [!DNL Amazon] 正確な IP アドレスであることを示します。 AWSのインターフェイスでは、これが必要であることが明確になっています。

## の作成 `Linux` のユーザー [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>この手順は、暗号化された接続を使用する場合にのみ必要です。 この方法については、使用しているデータベースの設定トピックを参照してください（例： MySQL）。 The `Linux` ユーザーが `SSH tunnel`：インターネット経由でデータを送信する最も安全な方法です。

## のデータベースユーザーを作成します。 [!DNL Commerce Intelligence]

これは、使用しているデータベースに応じて、手順が異なるプロセスの一部です。 ただし、ユーザーを作成して [!DNL Commerce Intelligence] データベースへのアクセスに使用する データベースの作成手順 [!DNL Commerce Intelligence] 使用しているデータベースの設定トピックに「 」というユーザーが表示されます。

## 次の場所に接続情報を入力 [!DNL Commerce Intelligence]

君が許した後で [!DNL Commerce Intelligence] インスタンスにアクセスしてユーザーを作成しました。最後に、次の場所に接続情報を入力する必要があります。 [!DNL Commerce Intelligence].

次の資格情報ページ： `MySQL`, `Microsoft SQL`、および `PostgreSQL` は、 `Integrations` ページ (**[!UICONTROL Manage Data** > **Integrations]**) をクリックして、 **[!UICONTROL Add Integration]**. 統合のリストが表示されたら、使用しているデータベースのアイコンをクリックして資格情報ページに移動します。 現在、必要な統合にアクセスできない場合は、Adobeアカウントチームにお問い合わせください。

接続の作成を完了するには、次の情報が必要です。

* RDS インスタンスのパブリックアドレス：これは、 [!DNL AWS] 管理コンソール。
* データベースインスタンスが使用するポート：一部のデータベースにはデフォルトのポートがあり、これにより `Port` フィールドに入力します。 この情報は、データベースのセットアップドキュメントにも記載されています。
* 作成したユーザーのユーザー名とパスワード [!DNL Commerce Intelligence].

暗号化された接続を使用している場合は、 `Encrypted` データベース資格情報ページをに切り替えます。 `Yes`. 暗号化を設定するための追加のフォームが表示されます。

![](../../../assets/sql-integration-encrypted-yes.png)


