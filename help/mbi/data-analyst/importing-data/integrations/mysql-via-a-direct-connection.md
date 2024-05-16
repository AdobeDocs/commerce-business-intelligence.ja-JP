---
title: 直接接続による MySQL の接続
description: 接続方法を学ぶ [!DNL MongoDB] 直接接続を使用する。
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# 接続 [!DNL MySQL] 直接接続による

## このトピック内

* [へのアクセスを許可 [!DNL Commerce Intelligence] IP アドレス](#allowlist)
* [を作成 [!DNL MySQL] のユーザー [!DNL Commerce Intelligence]](#steptwo)
* [接続情報をに入力 [!DNL Commerce Intelligence]](#stepthree)

## 移動先

* [[!DNL MySQL] 経由 ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] 経由 [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] では、を使用することをお勧めします。 [SSH](../integrations/mysql-via-ssh-tunnel.md) または、データを保護するためのその他の形式の暗号化 このオプションが選択できない場合でも、直接接続できます [!DNL Commerce Intelligence] をデータベースに追加するには、このトピックの手順を使用します。

このトピックでは、を直接接続する方法について説明します [!DNL MySQL] データベース先 [!DNL Commerce Intelligence]. これらの設定は、 [!DNL Adobe Commerce] または、MySQL を使用するその他の e コマースデータベース。

## へのアクセスを許可 [!DNL Commerce Intelligence] IP アドレス {#allowlist}

接続を成功させるには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 次のとおりです `54.88.76.97` および `34.250.211.151`ただし、そのページは [!DNL MySQL] 資格情報ページ：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## を作成 [!DNL MySQL] のユーザー [!DNL Commerce Intelligence]

を作成する最も簡単な方法 `MySQL` のユーザー [!DNL Commerce Intelligence] をにログインすると、次のクエリが実行されます `MySQL` （を使用） `GRANT` 権限。 置換 `Commerce Intelligence IP Address` （を使用） [!DNL Commerce Intelligence] IP アドレスと置換 `secure password` 任意の安全なパスワードを使用：

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

このユーザーが特定のデータベース、テーブルまたは列のデータにアクセスするのを制限するには、代わりにを実行します。 `GRANT` 許可したデータへのアクセスのみを許可するクエリ。

**同じユーザーとパスワードを使用して、必要なすべての IP に対して GRANT クエリを再実行します。**

## Commerce Intelligence で接続情報を入力します

最後に、接続とユーザー情報をに入力する必要があります。 [!DNL Commerce Intelligence]. を残しましたか [!DNL MySQL] 資格情報ページが開かれますか？ そうでない場合は、に移動します **[!UICONTROL Data** > **Connections]** をクリックして、 **[!UICONTROL Add New Data Source]**&#x200B;を選択し、 [!DNL MySQL] アイコン。 を変更することを忘れないでください `Encrypted` 切り替え `Yes`.

このページに以下の情報を入力します。まず、 `Database Connection` セクション：

* `Connection Nickname`：統合の名前（E コマースストアなど）を入力します
* `Username`：のユーザー名 [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー
* `Password`：のパスワード [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー
* `Port`：サーバー上の MySQL のポート（`3306` デフォルト）
* `Host`：デフォルトでは、localhost です。 通常、これはユーザのバインド アドレスの値です [!DNL MySQL] サーバー（デフォルトでは） `127.0.0.1 (localhost)`ただし、ローカルネットワークアドレス（例：）も指定できます `192.168.0.1`）またはサーバーのパブリック IP アドレス。

  値は、 `my.cnf` ファイル （の場所： `/etc/my.cnf`）を表す行の下 `\[mysqld\]`. このファイルで bind-address 行がコメントアウトされている場合、サーバーは外部からの接続の試行から保護されます。

完了したら、 **[!UICONTROL Save & Test]** をクリックして設定を完了します。

## 関連ドキュメント

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
