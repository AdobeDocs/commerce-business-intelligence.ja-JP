---
title: データベースへのアクセスの制限
description: アクセスを制限し、データベースを格納するサーバーへのアクセスを制限する方法について説明します。
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
TQID: https://experienceleague.adobe.com/O2cS-hbhjqktc4LpJD6agxgIwabrypgCY9fnJTCR2XM
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: efc8727dd67a9ffcd7a8a1059ea93df8c6344599
workflow-type: tm+mt
source-wordcount: 225
ht-degree: 0%

---

# アクセスを制限

サーバーへのSSH トンネルを作成する場合、[!DNL Adobe Commerce Intelligence]がデータベース以外にアクセスする必要はありません。 SSH ホストキーの登録、エラー、およびトラブルシューティングについては、[SSH ホストキーの検証](../../data-analyst/importing-data/integrations/ssh-host-key-verification.md)を参照してください。 データベースを格納するサーバーに[!DNL Commerce Intelligence]が完全にアクセスすることを望まない場合は、[!DNL Commerce Intelligence Linux] ユーザーを[制限付きbash shell](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html)に強制的に割り当てることで、アクセスを制限できます。

名前から推測したかもしれませんが、制限されたbash シェルは、標準シェルよりも制御された環境を設定するために使用されます。 このタイプのシェルについて重要なことは、制限付きシェルユーザーはシステム機能にアクセスしたり、何らかの変更を加えたりすることができないということです。

[!DNL Commerce Intelligence Linux] ユーザーを制限するには、次の2つの操作を行う必要があります。

1. PATH環境変数を空の文字列に変更します。 つまり、ユーザーはシステム実行可能ファイルにアクセスできません。

1. 実行されたシェルが`bash -r`であることを確認してください

これらはすべて、ユーザーがログインしたときに実行されるコマンドの一部として、ユーザーのホーム `dir/.ssh` ディレクトリの`authorized_keys` ファイル内で実行できます。 次のようになります。

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

この操作が完了すると、[!DNL Commerce Intelligence]用に作成したユーザーはシステムに変更を加えることができません。

