---
title: 直接接続を介した MySQL の接続
description: 接続方法の詳細 [!DNL MongoDB] 直接接続を介して。
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# 接続 [!DNL MongoDB] 直接接続経由

## この記事では、

* [次へのアクセスを許可： [!DNL MBI] IP アドレス](#allowlist)
* [の作成 ](#steptwo)
* [次の場所に接続情報を入力 [!DNL MBI]](#stepthree)

## ジャンプ先

* [&#39;SSH トンネル経由の MySQL&#39;](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [&#39;MySQL via cPanel&#39;](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>Adobeでは、 [SSH](../integrations/mysql-via-ssh-tunnel.md) または、データを保護するための他の暗号化の形式を使用できます。 これがオプションでない場合、直接接続できます [!DNL MBI] をデータベースに追加する場合は、この記事の手順を使用します。

この記事では、MySQL データベースを [!DNL MBI]. これらの設定は、MySQL を使用する Commerce またはその他の e コマースデータベースでも使用できます。

## 次へのアクセスを許可： [!DNL MBI] IP アドレス {#allowlist}

接続が成功するには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 これらは `54.88.76.97` および `34.250.211.151`ですが、MySQL 資格情報ページにも表示されます。

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## MySQL ユーザーの作成 [!DNL MBI]

最も簡単な方法で `MySQL` のユーザー [!DNL MBI] が次のクエリを実行すると、 `MySQL` と `GRANT` 権限。 置換 `MBI IP Address` と [!DNL MBI] IP アドレスと置換 `secure password` 選択した安全なパスワードで、次の設定を行います。

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

このユーザーが特定のデータベース、テーブルまたは列のデータにアクセスするのを制限するには、代わりにを実行します `GRANT` 許可したデータへのアクセスのみを許可するクエリ。

**同じユーザーとパスワードを使用して、必要な IP すべてに対して GRANT クエリを再実行します。**

## MBI に接続情報を入力

まとめるには、接続とユーザー情報を次のように入力する必要があります。 [!DNL MBI]. MySQL 資格情報ページを開いたままにしましたか？ そうでない場合は、に移動します。 **[!UICONTROL Data** > **Connections]** をクリックし、 **[!UICONTROL Add New Data Source]**、 MySQL アイコンの順にクリックします。 忘れずに `Encrypted` 切り替える `Yes`.

このページに、以下の情報を入力します。 `Database Connection` セクション：

* `Connection Nickname`:統合の名前を入力します（例：E コマースストア）。
* `Username`:のユーザー名 [!DNL MBI] MySQL ユーザー
* `Password`:のパスワード [!DNL MBI] MySQL ユーザー
* `Port`:サーバー上の MySQL のポート (`3306` （デフォルト）
* `Host`:デフォルトでは、localhost です。 一般的に、MySQL サーバーのバインドアドレスの値です。デフォルトではですが、 `127.0.0.1 (localhost)`は、一部のローカルネットワークアドレス ( 例： `192.168.0.1`) またはサーバーのパブリック IP アドレス。

   この値は、 `my.cnf` 次の場所にあるファイル： `/etc/my.cnf`) を `\[mysqld\]`. バインドアドレス行がそのファイルでコメントアウトされている場合、外部接続の試行からサーバーが保護されます。

それだ！ 完了したら、「 **[!UICONTROL Save & Test]** をクリックして設定を完了します。

## 関連ドキュメント

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
