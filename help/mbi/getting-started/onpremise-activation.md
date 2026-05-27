---
title: ' [!DNL Adobe Commerce Intelligence]  アカウントを有効にする'
description: お客様の [!DNL Commerce Intelligence]  アカウントをアクティベートするための連絡先情報をご覧ください。
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/V34xz5uwqrCn716FqG5byQ6wnLwkZUccBXgJMqiSdR4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: b6ae8fb1a1a7f30e3d56740986f9366e7d1e7f1a
workflow-type: tm+mt
source-wordcount: 748
ht-degree: 0%

---

# オンプレミスおよびスターターサブスクリプション用に[!DNL Commerce Intelligence] アカウントをアクティブ化する

オンプレミス サブスクリプション用に[!DNL Commerce Intelligence]をアクティブ化するには、まず[!DNL Commerce Intelligence] アカウントを作成し、設定情報を入力してから、[!DNL Commerce Intelligence]を[!DNL Commerce] データベースに接続します。<!-- For information about activation in `Cloud Starter` projects, see [Activating your [!DNL Commerce Intelligence] Account for `Cloud Starter` Subscriptions](../getting-started/cloud-activation.md).-->

## [!DNL Commerce Intelligence] アカウントを作成

アカウントを作成するには、Adobeのアカウントチームまたはカスタマーテクニカルアドバイザーにお問い合わせください。

## パスワードの作成

アカウントが作成されたら、メールで[!DNL The Magento BI Team@rjmetrics.com]からのアカウント通知メールを確認します。 電子メールに記載されているリンクを使用して、[!DNL Commerce Intelligence] アカウントにアクセスし、パスワードを作成してください。 受信トレイに移動し、電子メールアドレスを確認します。

電子メールが届かない場合は、[&#x200B; サポートにお問い合わせください](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

![新しいCommerce Intelligence アカウントのパスワード画面を作成](../assets/create-account-4.png)

## ストアの環境設定

データベース接続を設定する前に、ストア情報フォームに入力します。 この情報は、**[!UICONTROL Connect your Database]**&#x200B;の設定を完了するために必要です。

![&#x200B; ビジネス名、通貨、タイムゾーンのフィールドを含む情報フォームを保存する](../assets/create-account-6.png)

## [!DNL Commerce Intelligence] ユーザーを追加

パスワードを設定して[!DNL Commerce Intelligence]にログインしたら、他のユーザーを[!DNL Commerce Intelligence] アカウントに追加できます。 ユーザーを追加する場合は、適切な権限を持つ管理者ユーザーを追加して、アクティベーションプロセスを完了します。

![電子メールアドレスと権限レベルのフィールドを含むユーザーフォームを追加](../assets/create-account-5.png)

## [!DNL Commerce]管理者に専用の[!DNL Commerce Intelligence] ユーザーを作成します

[!DNL Commerce Intelligence]を使用するには、[!DNL Commerce] プロジェクトに永続的かつ専用のユーザーを追加する必要があります。 この専用ユーザーは、アカウントの[!DNL Commerce Intelligence] Data Warehouseへの新しいデータの取得と転送を可能にする[!DNL Commerce]への永続的な接続として機能します。

専用の[!DNL Commerce Intelligence] ユーザーを設定すると、アカウントが非アクティブ化または削除されないことが保証されるので、[!DNL Commerce Intelligence]接続が停止されます。


>[!NOTE]
>
>Adobeでは、永続ステータス（ACI-dedicated、ACI-database-connectorなど）を示すアカウント名を使用することをお勧めします。

管理者で[!DNL Commerce Intelligence]の専用ユーザーを作成した後、**[!UICONTROL Master]**&#x200B;設定が`Contributor`の[!DNL Commerce] プロジェクトのプライマリ環境に同じユーザーを追加します。

![Commerceは、役割がコントリビューター](../assets/commerce-add-user-settings.png)に設定されたユーザーインターフェイスを追加します

## Commerce IntelligenceのSSH キーを取得する

1. [!DNL Commerce Intelligence]設定の[!UICONTROL Connect your database] ページで、下にスクロールして「**[!UICONTROL Encryption settings]**」を選択します。

1. **暗号化タイプ**&#x200B;で、`SSH Tunnel`を選択します。

1. ドロップダウンから、指定された公開鍵をコピーします。

   ![SSH トンネルの種類と公開鍵フィールドを表示する暗号化設定ページ &#x200B;](../assets/encryption-setting-new-account.png)

## 公開鍵を[!DNL Commerce Intelligence]に追加

1. [!DNL Commerce Admin]から、作成したばかりの[!DNL Commerce Intelligence] ユーザーのログイン情報を使用してログインします。

1. 「**アカウント設定**」タブを選択します。

1. 下にスクロールして、**[!UICONTROL SSH Keys]** ドロップダウンを展開します。 次に、**[!UICONTROL Add a public key]**&#x200B;を選択します。

   ![SSH キーを使用したアカウント設定ページの節と「公開鍵を追加」ボタン &#x200B;](../assets/add-public-key.png)

1. 上記の[!DNL Encryption Type] ステップでコピーした公開鍵を貼り付けます。

   ![&#x200B; キーテキストフィールドと送信ボタンを含む公開鍵フォームを追加](../assets/paste-public-key.png)

## [!DNL Commerce Intelligence] Essentials `MySQL`資格情報を指定してください

1. `.magento/services.yaml`を更新します。

   ![services.yaml ファイル内のMySQL サービス設定を示すコード &#x200B;](../assets/update-magento-services-yaml.png)

1. `.magento.app.yaml`を更新します。

   ![app.yaml ファイル内のデータベース関係の設定を示すコード &#x200B;](../assets/magento-app-yaml-relationships.png)

## データベース接続情報の取得

[!DNL Commerce] データベースから[!DNL Commerce Intelligence]へのデータベース接続情報を取得します

1. 次のコマンドを実行して、情報を取得します。

   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

1. データベース情報を確認します。これは、次の例のようになります。

   ホスト、ポート、ユーザー名を含むデータベース接続資格情報を示す![JSON出力](../assets/example-database-information.png)

## 暗号化された接続を使用して[!DNL Commerce Intelligence]を[!DNL Commerce] データベースに接続します

>[!NOTE]
>
>Adobeでは、[`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) トンネルを使用してデータベース接続を行うことを強くお勧めします。 ただし、このメソッドがオプションでない場合でも、[`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md)を使用して[!DNL Commerce Intelligence]をデータベースにリンクできます。

[!UICONTROL Connect your Magento Database]画面に[!DNL Commerce Intelligence]情報を入力します。

![統合名、ホスト、ポート、ユーザー名、パスワード、データベース名のフィールドを使用してデータベース フォームを接続します](../assets/connect-magento-db.png)

**入力：**

[!UICONTROL Integration Name]: [自分の[!DNL Commerce Intelligence] インスタンスの名前を選択]

[!UICONTROL Host]: `mbi.internal`

[!UICONTROL Port]: `3306`

[!UICONTROL ユーザー名]: `mbi`

[!UICONTROL Password]: [前のセクションに表示された入力パスワード ]

[!UICONTROL Database Name]: `main`

[!UICONTROL Table Prefixes]: [ テーブルの接頭辞がない場合は空白のままにします]

## [!UICONTROL **タイムゾーン**]&#x200B;の設定

![&#x200B; データベースのタイムゾーンと目的のタイムゾーンドロップダウンフィールドを含むタイムゾーン設定フォーム &#x200B;](../assets/time-zone-settings.png)

**入力：**

[!UICONTROL Database Timezone]: `UTC`

[!UICONTROL Desired Timezone]: [ データを表示するタイムゾーンを選択]

## 暗号化設定情報を取得する

プロジェクト UIには、SSH アクセス文字列が表示されます。 この文字列は、[!UICONTROL **リモートアドレス**]&#x200B;および&#x200B;[!UICONTROL **ユーザー名**]&#x200B;に必要な情報を収集するために使用できます。 プロジェクト UIのマスターブランチにある「サイトにアクセス」ボタンを選択して、SSH アクセス文字列を使用します。 次に、次に示すように、[!UICONTROL User Name]と[!UICONTROL Remote Address]を見つけます。

ユーザー名とリモート アドレスを含むSSH アクセス情報を表示する![&#x200B; プロジェクト UI](../assets/master-branch-settings.png)

## [!DNL Encryption]の設定を入力

![暗号化タイプ、リモート アドレス、ユーザー名、およびポートのフィールドを含む暗号化設定フォーム &#x200B;](../assets/encryption-settings-2.png)

**入力：**

[!UICONTROL Encryption Type]: `SSH Tunnel`

[!UICONTROL Remote Address]: `ssh.us-3.magento.cloud` [前の手順]から

[!UICONTROL Username]: `vfbfui4vmfez6-master-7rqtwti—mymagento` [前の手順]から

[!UICONTROL Port]: `22`

## 統合を保存します。

設定手順を完了したら、[!UICONTROL **統合を保存**]&#x200B;を選択して変更を適用します。

これで、[!DNL Commerce] データベースを[!DNL Commerce Intelligence] アカウントに正常に接続しました。

>[!NOTE]
>
>[!DNL Adobe Commerce Intelligence Pro]のお客様の場合は、カスタマーサクセスマネージャーまたはカスタマーテクニカルアドバイザーに連絡して、次の手順を調整してください。

設定が完了したら、[あなたの[!DNL Commerce Intelligence] アカウントに](../getting-started/sign-in.md) ログインしてください。

<!--
# Activate your [!DNL Commerce Intelligence] Account

To activate [!DNL Commerce Intelligence] for on-premise or `Cloud Pro` subscriptions, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

>[!NOTE]
>
>Adobe no longer supports new `Cloud Starter` subscriptions.
-->
