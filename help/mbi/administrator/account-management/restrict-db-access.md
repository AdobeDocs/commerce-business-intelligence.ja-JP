---
title: データベースへのアクセスの制限
description: アクセスを制限し、データベースを格納するサーバーへのアクセスを制限する方法を説明します。
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# アクセスの制限

サーバーへの SSH トンネルを作成する際に、 [!DNL Adobe Commerce Intelligence] データベース以外にアクセスできること。 必要なければ [!DNL Commerce Intelligence] データベースが格納されているサーバーへのフルアクセスを持つには、以下を強制してアクセスを制限できます。 [!DNL Commerce Intelligence Linux] ユーザー入力 a [制限付き bash シェル](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

名前から推測したかもしれませんが、標準のシェルよりも制御が強化された環境を設定するために、制限された bash シェルが使用されています。 このタイプのシェルに関する重要な点は、制限されたシェルのユーザはシステムの関数にアクセスできず、何らかの変更を加えられないことです。

を制限するには [!DNL Commerce Intelligence Linux] ユーザーは、次の 2 つの操作を行う必要があります。

1. PATH 環境変数を空の文字列に変更します。 つまり、ユーザーはシステムの実行可能ファイルにアクセスできません。

1. 実行したシェルが `bash -r`

これらの操作は両方とも `authorized_keys` ユーザーのホームにあるファイル `dir/.ssh` ユーザーがログインしたときに実行するコマンドの一部として使用するディレクトリ。 次のようになります。

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

これが完了すると、用に作成したユーザー [!DNL Commerce Intelligence] システムに変更を加えることはできません。
