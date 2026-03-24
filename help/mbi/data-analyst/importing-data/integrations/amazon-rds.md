---
title: Amazon RDSの連携
description: RDS インスタンスを接続する手順を説明します。
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KAjnETtFvi9EHUDY8SJ-TSEhP3zooQel5ZlN-E3QxIg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 503
ht-degree: 0%

---

# [!DNL Amazon RDS]を接続

[!DNL Amazon Relational Database Services (RDS)]は、おそらく既に使い慣れているデータベース エンジン上で実行されるマネージド データベース サービスです。

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

[!DNL RDS] インスタンスを接続する手順は、使用するデータベースの種類と、暗号化された接続（[`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)など）を使用しているかどうかに応じて異なりますが、基本的な手順は次のとおりです。

## [!DNL Commerce Intelligence]にデータベースへのアクセスを許可

各データベースの資格情報ページ （**[!UICONTROL Manage Data** > **Integrations]**）に、R[!DNL RDS]を[!DNL Commerce Intelligence]に接続するために認証する必要があるIP アドレスを含むボックスが表示されます：`54.88.76.97`と`34.250.211.151`。 ここでは、IP アドレスボックスを強調表示した`MySQL credentials` ページを見ていきます。

![IP アドレス設定を示すAmazon RDS セキュリティグループの設定](../../../assets/RDS_IP.png)

[!DNL Commerce Intelligence]が[!DNL RDS] インスタンスに正常に接続するには、これらのIP アドレスをAWS管理コンソールを使用して適切なデータベースセキュリティグループに追加する必要があります。 これらのIP アドレスは、既存のグループに追加することも、グループを作成することもできます。重要なことは、グループが[!DNL Commerce Intelligence]に接続するインスタンスへのアクセスを許可されていることです。

[!DNL Commerce Intelligence]個のIP アドレスを追加する場合は、正確なIP アドレスであることを`/32`に示すために、アドレスの末尾に[!DNL Amazon]を追加してください。 心配しないでください。AWSのインターフェイスは、これが必要であることを明確にしています。

## `Linux`の[!DNL Commerce Intelligence] ユーザーを作成 {#linux}

>[!NOTE]
>
>この手順は、暗号化された接続を使用している場合にのみ必要です。 この方法の手順については、使用しているデータベースのセットアップ トピック（例：MySQL）を参照してください。 `Linux` ユーザーは、インターネット経由でデータを送信する最も安全な方法である`SSH tunnel`を作成できます。

## [!DNL Commerce Intelligence]のデータベースユーザーを作成

これは、使用するデータベースによって手順が異なるプロセスの一部です。 しかし、考え方は同じですが、データベースへのアクセスに使用される[!DNL Commerce Intelligence]のユーザーを作成します。 データベース [!DNL Commerce Intelligence] ユーザーの作成手順については、使用しているデータベースのセットアップ トピックを参照してください。

## 接続情報を[!DNL Commerce Intelligence]に入力

インスタンスへの[!DNL Commerce Intelligence] アクセスを許可し、ユーザーを作成した後、最後に行う必要があるのは、接続情報を[!DNL Commerce Intelligence]に入力することです。

`MySQL`、`Microsoft SQL`および`PostgreSQL`の資格情報ページには、`Integrations`をクリックして&#x200B;**[!UICONTROL Manage Data** > **Integrations]** ページ （**[!UICONTROL Add Integration]**）からアクセスできます。 統合のリストが表示されたら、使用しているデータベースのアイコンをクリックして、資格情報ページに移動します。 現在、必要な統合機能にアクセスできない場合は、Adobe アカウントチームにお問い合わせください。

接続の作成を完了するには、次の情報が必要です。

* RDS インスタンスの公開アドレス：[!DNL AWS]管理コンソールで確認できます。
* データベースインスタンスが使用するポート：一部のデータベースにはデフォルトのポートがあり、`Port` フィールドに自動的に入力されます。 この情報は、データベースの設定ドキュメントにも記載されています。
* [!DNL Commerce Intelligence]用に作成したユーザーのユーザー名とパスワード。

暗号化された接続を使用している場合は、データベース資格情報ページの`Encrypted` トグルを`Yes`に変更します。 これにより、暗号化を設定するための追加フォームが表示されます。

暗号化が有効になっている![SQL統合フォームで「はい」オプションが表示されている](../../../assets/sql-integration-encrypted-yes.png)


