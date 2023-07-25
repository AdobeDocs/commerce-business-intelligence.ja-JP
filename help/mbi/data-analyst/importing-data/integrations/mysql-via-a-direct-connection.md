---
title: 直接接続を介した MySQL の接続
description: 接続方法の詳細 [!DNL MongoDB] 直接接続を介して。
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# 接続 [!DNL MySQL] 直接接続経由

## このトピックでは、

* [次へのアクセスを許可： [!DNL Commerce Intelligence] IP アドレス](#allowlist)
* [の作成 [!DNL MySQL] のユーザー [!DNL Commerce Intelligence]](#steptwo)
* [次の場所に接続情報を入力 [!DNL Commerce Intelligence]](#stepthree)

## ジャンプ先

* [[!DNL MySQL] 経由 ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] 経由 [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] では、 [SSH](../integrations/mysql-via-ssh-tunnel.md) または、データを保護するための他の暗号化の形式を使用できます。 これがオプションでない場合、直接接続できます [!DNL Commerce Intelligence] をデータベースに追加します。

このトピックでは、 [!DNL MySQL] データベースへ [!DNL Commerce Intelligence]. これらの設定は、 [!DNL Adobe Commerce] または MySQL を使用するその他の e コマースデータベース。

## 次へのアクセスを許可： [!DNL Commerce Intelligence] IP アドレス {#allowlist}

接続が成功するには、IP アドレスからのアクセスを許可するようにファイアウォールを設定する必要があります。 これらは `54.88.76.97` および `34.250.211.151`ですが、それはまた、 [!DNL MySQL] 認証情報ページ：

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## の作成 [!DNL MySQL] のユーザー [!DNL Commerce Intelligence]

最も簡単な方法で `MySQL` のユーザー [!DNL Commerce Intelligence] が次のクエリを実行すると、 `MySQL` と `GRANT` 権限。 置換 `Commerce Intelligence IP Address` と [!DNL Commerce Intelligence] IP アドレスと置換 `secure password` 選択した安全なパスワードで、次の設定を行います。

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

このユーザーが特定のデータベース、テーブルまたは列のデータにアクセスするのを制限するには、代わりにを実行します `GRANT` 許可したデータへのアクセスのみを許可するクエリ。

**同じユーザーとパスワードを使用して、必要な IP すべてに対して GRANT クエリを再実行します。**

## Commerce Intelligence で接続情報を入力

まとめるには、接続とユーザー情報を次のように入力する必要があります。 [!DNL Commerce Intelligence]. あなたは [!DNL MySQL] 認証情報ページを開きますか？ そうでない場合は、に移動します。 **[!UICONTROL Data** > **Connections]** をクリックし、 **[!UICONTROL Add New Data Source]**」、「 [!DNL MySQL] アイコン 忘れずに `Encrypted` 切り替える `Yes`.

このページに、以下の情報を入力します。 `Database Connection` セクション：

* `Connection Nickname`:統合の名前を入力します（例：E コマースストア）。
* `Username`:のユーザー名 [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー
* `Password`:のパスワード [!DNL Commerce Intelligence] [!DNL MySQL] ユーザー
* `Port`:サーバー上の MySQL のポート (`3306` （デフォルト）
* `Host`:デフォルトでは、localhost です。 一般に、バインドアドレスの値は [!DNL MySQL] サーバー（デフォルトは） `127.0.0.1 (localhost)`は、一部のローカルネットワークアドレス ( 例： `192.168.0.1`) またはサーバーのパブリック IP アドレス。

  この値は、 `my.cnf` 次の場所にあるファイル： `/etc/my.cnf`) を `\[mysqld\]`. バインドアドレス行がそのファイルでコメントアウトされている場合、外部接続の試行からサーバーが保護されます。

完了したら、「 **[!UICONTROL Save & Test]** をクリックして設定を完了します。

## 関連ドキュメント

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
