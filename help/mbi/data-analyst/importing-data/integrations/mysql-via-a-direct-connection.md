---
title: 直接接続を介したMySQLの接続
description: 直接接続を介して [!DNL MongoDB] 接続する方法を説明します。
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/HkKVLKV9RpLIWN-YY5GggdnlHeBB2Xg9odAbSZklHGE
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 376
ht-degree: 0%

---

# 直接接続を介して[!DNL MySQL]に接続

## このトピックでは

* [ [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可](#allowlist)
* [ [!DNL MySQL] の [!DNL Commerce Intelligence] ユーザーを作成](#steptwo)
* [接続情報を [!DNL Commerce Intelligence]に入力](#stepthree)

## に移動

* [[!DNL MySQL]経由 ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL]経由で [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe]では、[SSH](../integrations/mysql-via-ssh-tunnel.md)またはその他の形式の暗号化を使用してデータを保護することをお勧めします。 このオプションを使用しない場合でも、このトピックの手順を使用して、[!DNL Commerce Intelligence]をデータベースに直接接続できます。

このトピックでは、[!DNL MySQL] データベースを[!DNL Commerce Intelligence]に直接接続する方法について説明します。 これらの設定は、[!DNL Adobe Commerce]またはMySQLを使用するその他のe コマースデータベースでも使用できます。

## [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可 {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 `54.88.76.97`と`34.250.211.151`ですが、[!DNL MySQL]資格情報ページにも表示されます。

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## [!DNL MySQL]の[!DNL Commerce Intelligence] ユーザーを作成

`MySQL`の[!DNL Commerce Intelligence] ユーザーを作成する最も簡単な方法は、`MySQL`権限で`GRANT`にログインしたときに次のクエリを実行することです。 `Commerce Intelligence IP Address`を[!DNL Commerce Intelligence] IP アドレスに置き換え、`secure password`を選択した安全なパスワードに置き換えます。

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

このユーザーが特定のデータベース、テーブル、または列内のデータにアクセスすることを制限するには、代わりに、許可されたデータへのアクセスのみを許可する`GRANT` クエリを実行できます。

**同じユーザーとパスワードを使用して、必要なすべてのIPに対してGRANT クエリを再実行します。**

## Commerce Intelligenceに接続情報を入力

最後に、接続とユーザー情報を[!DNL Commerce Intelligence]に入力する必要があります。 [!DNL MySQL]資格情報ページを開いたままにしましたか？ そうでない場合は、**[!UICONTROL Data** > **Connections]**&#x200B;に移動して&#x200B;**[!UICONTROL Add New Data Source]**&#x200B;をクリックし、[!DNL MySQL] アイコンをクリックします。 `Encrypted` トグルを`Yes`に変更することを忘れないでください。

`Database Connection` セクションから始めて、このページに次の情報を入力します。

* `Connection Nickname`：統合の名前を入力します（例：E コマースストア）
* `Username`: [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーのユーザー名
* `Password`: [!DNL Commerce Intelligence] [!DNL MySQL] ユーザーのパスワード
* `Port`: サーバー上のMySQLのポート （`3306` デフォルト）
* `Host`: デフォルトでは、これはlocalhostです。 一般に、これは[!DNL MySQL] サーバーのバインド アドレス値です。デフォルトは`127.0.0.1 (localhost)`ですが、一部のローカル ネットワーク アドレス （例：`192.168.0.1`）またはサーバーのパブリック IP アドレスにすることもできます。

  値は、`my.cnf`を読み込む行の下の`/etc/my.cnf` ファイル（`\[mysqld\]`にある）にあります。 そのファイルでバインドアドレス行がコメントアウトされると、サーバーは外部からの接続試行から保護されます。

完了したら、**[!UICONTROL Save & Test]**&#x200B;をクリックして設定を完了します。

## 関連ドキュメント

* [統合を再認証しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
