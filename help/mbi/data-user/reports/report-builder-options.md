---
title: Report Builder の選択
description: Report Builder の選択方法を説明します。
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# Report Builder の選択

>[!NOTE]
>>[ 管理者権限 ](../../administrator/user-management/user-management.md) が必要です。

分析を作成するオプションが増えたので、ニーズに合った Report Builder のフレーバーを正確に把握することが困難な場合があります。 このトピックでは、分析を構築するための最適な方法を選択する手順を説明します。

## いつその [!DNL SQL Report Builder] を使えばいいですか。 {#whensql}

[!DNL SQL Report Builder] 上で [!DNL traditional Report Builder] を使用する一般的な理由をいくつか見てみましょう。

### [!DNL SQL] 固有の関数を使用する場合

この [!DNL SQL Report Builder] の美しさの一つは、Data Warehouse Manager では現在利用できない機能を使用できることです。 これまでは、アナリストがユーザーのビジョンを完全に実現するために介入する必要があった可能性があります。

[!DNL SQL Report Builder] は、以前は使用できなかった [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) や [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html) などの関数をサポートしています。 [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) にアクセスできますが、その他の SQL 固有の関数には次のものがあります。

* [`Bitwise aggregate` 関数 ](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` 演算子 ](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### 何らかのテストを行う場合

分析に最適な方法を見つけるために、様々な手法や戦略を試す場合は、[!DNL SQL Report Builder] を使用できます。 Data Warehouse Manager で列を構築するには、DWM を使用して作成する時間と列は、更新サイクルに依存します。

せいぜい、列を使用するには 1 回の更新サイクルを待つ必要があります。 列の作成を誤ったことに気付いた場合は、*2* サイクルを経る必要があります。1 つのサイクルで最初に列に入力し、もう 1 つのサイクルで変更が反映されます。

### 新しい列を 1 回だけ使用する場合

前述のように、Data Warehouse Manager で列を作成するには時間がかかります。 Adobe 1 つのレポートで作成した列のみを使用する予定がある場合は、[!DNL SQL Report Builder] の使用をお勧めします。 これにより、更新サイクルが完了するまで待つ必要がなくなり、作業をより迅速に再開できます。

### 1 対多の関係を持つデータを操作する場合

データの構造によっては、分析を構築するための [!DNL SQL Report Builder] ータの方が効率的で論理的な選択になる場合があります。 Data Warehouse Manager では、1 対 1 の関係を表す列を作成するのは簡単ですが、1 対多の関係を扱う場合は、少し混乱する可能性があります。

例えば、1 つの製品が複数の製品カテゴリの一部と見なされ、各製品の各カテゴリに関連付けられた売上高を表示するとします。 DWM を使用してこの関係を作成しようとすることは、面倒で難しい場合がありますが、[!DNL SQL] クエリを作成する方が少し簡単な場合があります。

![1 対多の関係を持つ製品カテゴリ別の売上高を示す SQL クエリ ](../../assets/When_should_I_use_the_RB_2.png)

## 従来のReport Builderは、どのような場合に使用すればよいですか？ {#whentraditionalrb}

[!DNL SQL Report Builder] を使用すると、以前は使用できなかった機能をより詳細に制御してアクセスできますが、常に正しい選択とは限りません。 Adobeでは、使用する report builder のフレーバーを決定する際に、次の点も考慮することをお勧めします。

### 単純なレポートを作成する場合

単純に作成したい場合は、従来のReport Builderを使用すると、完全な [!DNL SQL] クエリを記述するよりもはるかに高速です。 分析の作成が必要な列が既にData Warehouse Manager に存在している場合に役立ちます。

### 作業を他のユーザーと共有している場合…

組織全体のユーザーがこの分析を使用または表示していますか。 誰と作業を共有しているかによって、ビジュアルReport Builderにこだわる方が良い場合もあります。 ユーザーは、[!DNL Visual Report Builder] の定義を素早く確認できるのに対し、長 [!DNL SQL] クエリを読み取る可能性もあります。

レポートを必要としているものの、[!DNL SQL] に詳しくない人がいれば、AdobeはReport Builderのオリジナルの味を使用することをお勧めします。 これにより、作業が容易になります。

## まとめ {#wrapup}

[!DNL SQL Report Builder] と [!DNL Visual Report Builder] はどちらも、様々なユースケースに適しています。 これは、通常、分析のニーズと、誰が分析を使用しているかによって異なります。
