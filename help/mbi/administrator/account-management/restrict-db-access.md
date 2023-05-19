---
title: データベースへのアクセスの制限
description: アクセスを制限し、データベースを格納するサーバーへのアクセスを制限する方法を説明します。
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# アクセスを制限

サーバーに SSH トンネルを作成する場合、 [!DNL Adobe Commerce Intelligence] データベース以外の何かにアクセスできるようにする。 もしあなたが望まないなら [!DNL Commerce Intelligence] データベースを格納しているサーバーに対するフルアクセス権を持つには、 [!DNL Commerce Intelligence Linux] ユーザーを [制限付き bash シェル](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

名前から推測したかもしれませんが、制限付きの bash シェルは、標準のシェルよりも制御された環境を設定するために使用されます。 この種のシェルに関する重要な点は、制限付きシェルユーザーがシステム関数にアクセスしたり、何らかの変更を加えたりできないことです。

次の手順で [!DNL Commerce Intelligence Linux] ユーザーは、次の 2 つの操作を実行する必要があります。

1. PATH 環境変数を空の文字列に変更します。 つまり、ユーザーはシステム実行可能ファイルにアクセスできません。

1. 実行するシェルがであることを確認します。 `bash -r`

どちらも `authorized_keys` ユーザーの家にあるファイル `dir/.ssh` ディレクトリが、ユーザーがログインしたときに実行されるコマンドの一部として含まれている。 次のようになります。

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

これが完了すると、 [!DNL Commerce Intelligence] はシステムに変更を加えることができません。
