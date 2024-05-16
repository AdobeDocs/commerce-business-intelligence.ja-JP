---
title: Report Builder の選択
description: Report Builder の選択方法を説明します。
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Report Builder の選択

>[!NOTE]
>>が必要 [管理者権限](../../administrator/user-management/user-management.md).

分析を作成するオプションが増えたので、ニーズに合った Report Builder のフレーバーを正確に把握することが困難な場合があります。 このトピックでは、分析を構築するための最適な方法を選択する手順を説明します。

## 使用するタイミング [!DNL SQL Report Builder]? {#whensql}

を使用する一般的な理由をいくつか見てみましょう。 [!DNL SQL Report Builder] 次の期間 [!DNL traditional Report Builder].

### を使用する場合 [!DNL SQL]固有の関数…

の美しさの一部 [!DNL SQL Report Builder] これは、Data Warehouseマネージャーで現在使用できない関数を使用する機能を提供するということです。 これまでは、アナリストがユーザーのビジョンを完全に実現するために介入する必要があった可能性があります。

この [!DNL SQL Report Builder] などの関数をサポートしています [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) および [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html)以前は使用できませんでした。 にアクセスできます [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html)ただし、その他の SQL 固有の関数には、次のようなものがあります。

* [`Bitwise aggregate` 関数](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` 演算子](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### 何らかのテストを行う場合

分析に最適な方法を見つけるために、様々な手法や戦略を試したい場合は、 [!DNL SQL Report Builder]. Data Warehouseマネージャで列を構築するには、DWM を使用して作成する時間と列は更新サイクルに依存します。

せいぜい、列を使用するには 1 回の更新サイクルを待つ必要があります。 列の作成を間違えたことに気付いた場合は、しばらくお待ちください *two* サイクル：最初に列に入力するサイクルと、リビジョンが反映されるサイクルです。

### 新しい列を 1 回だけ使用する場合

前述のように、Data Warehouseマネージャーで列を作成するには時間がかかります。 1 つのレポートで作成した列のみを使用する予定がある場合は、Adobeでは、 [!DNL SQL Report Builder]. これにより、更新サイクルが完了するまで待つ必要がなくなり、作業をより迅速に再開できます。

### 1 対多の関係を持つデータを操作する場合

場合によっては、データの構造によって、 [!DNL SQL Report Builder] 分析を構築するための、より効率的で論理的な選択。 1 対 1 のリレーションシップ用の列を作成するのはData Warehouse マネージャでは簡単ですが、1 対多のリレーションシップを処理する場合は、少し混乱する場合があります。

例えば、1 つの製品が複数の製品カテゴリの一部と見なされ、各製品の各カテゴリに関連付けられた売上高を表示するとします。 DWM を使用してこの関係を作成しようとすることは、面倒で困難な場合がありますが、次のように記述します [!DNL SQL] クエリは、もう少し簡単かもしれません。

![](../../assets/When_should_I_use_the_RB_2.png)

## 従来のReport Builderを使用するのは、どのような場合ですか？ {#whentraditionalrb}

一方、は [!DNL SQL Report Builder] 以前は利用できなかった機能をより詳細に制御し、アクセスできるようにします。これは必ずしも正しい選択とは限りません。 Adobeでは、使用する report builder のフレーバーを決定する際に、次の点も考慮することをお勧めします。

### 単純なレポートを作成する場合

単純に作成したい場合は、従来のReport Builderを使用すると、完全なものを書くよりもはるかに高速です [!DNL SQL] クエリ。 分析の作成に必要な列が既にData Warehouseマネージャーに存在している場合に役立ちます。

### 作業を他のユーザーと共有している場合…

組織全体のユーザーがこの分析を使用または表示していますか。 誰と作業を共有しているかによって、ビジュアルReport Builderを使い続けた方が良い場合もあります。 ユーザーは、 [!DNL Visual Report Builder] と、長く読む可能性がある場合の比較 [!DNL SQL] クエリ。

レポートを必要としているが、に詳しくないユーザーがいる場合 [!DNL SQL]Adobeは、Report Builderの元の味を使用することをお勧めします。 これにより、作業が容易になります。

## まとめ {#wrapup}

両方 [!DNL SQL Report Builder] および [!DNL Visual Report Builder] は、様々なユースケースに適しています。 これは、通常、分析のニーズと、誰が分析を使用しているかによって異なります。
