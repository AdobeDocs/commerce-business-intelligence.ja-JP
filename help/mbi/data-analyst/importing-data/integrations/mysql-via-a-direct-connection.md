---
title: 直接接続による MySQL の接続
description: 直接接続を使用して接続する方法  [!DNL MongoDB]  説明します。
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 直接接続を介して [!DNL MySQL] に接続

## このトピック内

* [&#x200B; [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可](#allowlist)
* [&#x200B; [!DNL MySQL]  のユ  [!DNL Commerce Intelligence] ザーを作成](#steptwo)
* [接続情報の入力先  [!DNL Commerce Intelligence]](#stepthree)

## 移動先

* [[!DNL MySQL] via &#x200B;](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] では、データを保護するために [SSH](../integrations/mysql-via-ssh-tunnel.md) またはその他の形式の暗号化を使用することをお勧めします。 これがオプションでない場合でも、このトピックの手順を使用して、[!DNL Commerce Intelligence] をデータベースに直接接続できます。

このトピックでは、[!DNL MySQL] データベースを [!DNL Commerce Intelligence] に直接接続する手順について説明します。 これらの設定は、[!DNL Adobe Commerce] または MySQL を使用するその他の e コマースデータベースでも使用できます。

## [!DNL Commerce Intelligence] IP アドレスへのアクセスを許可 {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 これらは `54.88.76.97` と `34.250.211.151` ですが、[!DNL MySQL] の資格情報ページにも表示されます。

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## [!DNL MySQL] の [!DNL Commerce Intelligence] ユーザーの作成

`MySQL` の [!DNL Commerce Intelligence] ユーザーを作成する最も簡単な方法は、`MySQL` 権限で `GRANT` にログインしたときに次のクエリを実行することです。 `Commerce Intelligence IP Address` を [!DNL Commerce Intelligence] の IP アドレスに置き換え、`secure password` を選択した安全なパスワードに置き換えます。

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

このユーザーが特定のデータベース、テーブル、または列のデータにアクセスするのを制限するには、許可されたデータへのアクセスのみを許可する `GRANT` クエリを実行します。

**同じユーザーとパスワードを使用して、必要なすべての IP に対して GRANT クエリを再実行します。**

## Commerce Intelligenceに接続情報を入力

まとめるには、接続とユーザー情報を [!DNL Commerce Intelligence] に入力する必要があります。 [!DNL MySQL] 資格情報ページを開いたままにしましたか？ 表示されていない場合は、**[!UICONTROL Data** > **Connections]** に移動して「**[!UICONTROL Add New Data Source]**」をクリックし、[!DNL MySQL] アイコンをクリックします。 `Encrypted` の切り替えを `Yes` に変更することを忘れないでください。

このページに、`Database Connection` のセクションから始まる次の情報を入力します。

* `Connection Nickname`：統合の名前（E コマースストアなど）を入力します
* `Username`:[!DNL Commerce Intelligence] [!DNL MySQL] ユーザーのユーザー名
* `Password`:[!DNL Commerce Intelligence] [!DNL MySQL] ユーザーのパスワード
* `Port`: サーバー上の MySQL のポート （デフォルトでは `3306`）
* `Host`: デフォルトでは、これは localhost です。 一般に、これは [!DNL MySQL] サーバーのバインド アドレス値です。デフォルトでは `127.0.0.1 (localhost)` ですが、ローカル ネットワーク アドレス （`192.168.0.1` など）またはサーバーのパブリック IP アドレスの場合もあります。

  この値は、`my.cnf` を読み取る行の下の `/etc/my.cnf` ファイル（`\[mysqld\]` にあります）にあります。 このファイルで bind-address 行がコメントアウトされている場合、サーバーは外部からの接続の試行から保護されます。

完了したら、「**[!UICONTROL Save & Test]**」をクリックして設定を完了します。

## 関連ドキュメント

* [&#x200B; 統合の再認証 &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=ja)
