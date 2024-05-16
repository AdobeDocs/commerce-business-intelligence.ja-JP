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

# 接続 [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] は、既に使い慣れたデータベースエンジンで実行されるマネージドデータベースサービスです。

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

を接続する手順 [!DNL RDS] インスタンスは、使用しているデータベースのタイプと、暗号化された接続を使用しているかどうかによって異なります（ [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)）が、基本は次のとおりです。

## を承認する [!DNL Commerce Intelligence] データベースにアクセスするには

資格情報ページ（**[!UICONTROL Manage Data** > **Integrations]**）を選択すると、接続 R に認証する必要のある IP アドレスを含むボックスが表示されます。[!DNL RDS] 対象： [!DNL Commerce Intelligence]: `54.88.76.97` および `34.250.211.151`. を見てみましょう。 `MySQL credentials` ip アドレスボックスをハイライトしたページ：

![](../../../assets/RDS_IP.png)

の場合 [!DNL Commerce Intelligence] を使用してと正常に接続するには [!DNL RDS] インスタンスでは、これらの IP アドレスをAWS Management Console 経由で適切なデータベースセキュリティグループに追加する必要があります。 これらの IP アドレスは、既存のグループに追加することも、作成することもできます。重要なのは、接続先のインスタンスにグループがアクセスする権限を持っていることです [!DNL Commerce Intelligence].

を追加する場合 [!DNL Commerce Intelligence] IP アドレス、必ず以下を追加します `/32` を示すアドレスの末尾に追加されます [!DNL Amazon] 正確な IP アドレスであること。 AWS インターフェイスは、これが必要であることを明確にします。

## を作成 `Linux` のユーザー [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>この手順が必要になるのは、暗号化された接続を使用している場合のみです。 この方法については、使用しているデータベース（例：MySQL）の設定トピックを参照してください。 この `Linux` ユーザーにより、以下を作成できます： `SSH tunnel`（インターネット経由でデータを送信する最も安全な方法です）。

## のデータベースユーザーを作成 [!DNL Commerce Intelligence]

これは、使用しているデータベースに応じて手順が異なる、プロセスの一部です。 考え方は同じですが、のユーザーを作成します [!DNL Commerce Intelligence] データベースにアクセスするために使用されます。 データベース作成手順 [!DNL Commerce Intelligence] ユーザーは、使用しているデータベースの設定トピックで確認できます。

## 接続情報をに入力 [!DNL Commerce Intelligence]

付与した後 [!DNL Commerce Intelligence] インスタンスにアクセスし、ユーザーを作成したら、接続情報をに入力する必要はありません。 [!DNL Commerce Intelligence].

の資格情報ページ `MySQL`, `Microsoft SQL`、および `PostgreSQL` 経由でアクセスできます `Integrations` ページ （**[!UICONTROL Manage Data** > **Integrations]**）をクリックします。 **[!UICONTROL Add Integration]**. 統合のリストが表示されたら、使用しているデータベースのアイコンをクリックして、資格情報ページに移動します。 現在、必要な統合へのアクセス権がない場合は、Adobeアカウントチームにお問い合わせください。

接続の作成を完了するには、次の情報が必要です。

* RDS インスタンスのパブリックアドレス：これは、次の場所にあります。 [!DNL AWS] 管理コンソール。
* データベースインスタンスが使用するポート：一部のデータベースにはデフォルトのポートがあり、自動的に次の値が入力されます `Port` フィールド。 この情報は、データベースの設定ドキュメントでも確認できます。
* 作成したユーザーのユーザー名とパスワード [!DNL Commerce Intelligence].

暗号化された接続を使用している場合、 `Encrypted` データベース資格情報ページをに切り替えます。 `Yes`. 暗号化を設定するための追加フォームが表示されます。

![](../../../assets/sql-integration-encrypted-yes.png)


