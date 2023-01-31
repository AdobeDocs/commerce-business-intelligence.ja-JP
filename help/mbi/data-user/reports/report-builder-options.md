---
title: Report Builder の選択
description: Report Builder の選択方法を説明します。
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Report Builder の選択

>[!NOTE]
>>必要 [管理者権限](../../administrator/user-management/user-management.md).


私たちは皆、選択肢を持つのが好きです。 しかし、選択に直面したとき、決断に従わなければならないという考えに対して、我々の一部は、拒否し、凍結するかもしれません。 オプションは素晴らしいですが、圧倒的で混乱を招く可能性もあります。

現在は、分析を作成するためのオプションが増えているので、Report Builder のどの種類がニーズに合うのかを正確に把握するのが難しい場合があります。 分析を構築する最適な方法を選択する際にガイダンスが必要な場合は、この記事を参照してください。

## 使用するタイミング `SQL Report Builder`? {#whensql}

従来のReport Builderに対して SQLReport Builderを使用する一般的な理由をいくつか見てみましょう。

### SQL 固有の関数を使用する場合…

の美しさの一部 `SQL Report Builder` は、Data Warehouseマネージャで現在使用できない関数を使用できる機能を提供します。 以前は、アナリストが、自分のビジョンを完全に理解するのに役立つように手を差し伸べなければならなかったかもしれません。

SQLReport Builderは、 [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) および [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html)以前は使用できなかったものです。 次にアクセス： [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html)を使用しますが、他の SQL 固有の関数には次のものがあります。

* [`Bitwise aggregate` 関数](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` 演算子](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### テストを実行する場合

様々な手法や戦略を試して、分析に最適なものを見つけたい場合は、 `SQL Report Builder`. Data Warehouseマネージャーでの列の作成には、DWM を使用して作成する時間と列が必要になりますが、更新サイクルによって異なります。

列を使用するには、最善でも 1 つの更新サイクルを経る必要があります。 柱の構築に誤りがあると気付いたら、通り抜けて待つ必要があります *2* サイクル：1 つは最初に列にデータを入力するためのもので、もう 1 つはリビジョンを反映するためのサイクルです。

### 新しい列を 1 回だけ使用する場合

上記の節で説明したように、Data Warehouseマネージャで新しい列を作成するには時間がかかります。 1 つのレポートで作成した列のみを使用する場合は、 `SQL Report Builder`. これにより、更新サイクルが完了するのを待つ必要がなくなり、作業を迅速に戻すことができます。

### 1 対多の関係を持つデータを扱っている場合

場合によっては、データの構造が `SQL Report Builder` 分析を構築するための、より効率的で論理的な選択肢。 1 対 1 の関係用の列を作成する方法は、Data Warehouseマネージャでは非常に簡単ですが、1 対多の関係を扱う場合は、少し混乱を招く可能性があります。

例えば、1 つの製品が複数の製品カテゴリの一部と見なされ、各製品の各カテゴリに関連する売上高を表示したいとします。 DWM を使用してこの関係を作成しようとするのは面倒で困難ですが、SQL クエリを記述する方が少し簡単な場合があります。

![](../../assets/When_should_I_use_the_RB_2.png)

## 従来のReport Builder {#whentraditionalrb}

また、 `SQL Report Builder` は、以前は使用できなかった機能をより詳細に制御し、利用できるようにします。常に適切な選択とは限りません。 また、Report Builder の用途を決定する際には、次の点も考慮することをお勧めします。

### シンプルなレポートを作成する場合

簡単に作成したい場合は、従来のReport Builderを使用する方が、完全な SQL クエリを記述するよりもはるかに高速です。 また、分析を作成する必要がある列が既に [Data Warehouse管理 ] にある場合にも役立ちます。

### 他のユーザーと作業内容を共有する場合

組織全体のユーザーは、この分析を使用/表示しますか？ 誰と作業を共有しているかによっては、場合によっては、ビジュアルReport Builderを使用した方が良い可能性があります。 ユーザーは、長くなる可能性のある SQL クエリを読み取るのに対して、ビジュアルReport Builder内の定義をすばやく確認できます。

レポートを必要とするが SQL に詳しくないユーザーがいる場合は、Report Builderの元の機能を使用することをお勧めします。 それは彼らを楽にする。

## 折り返し {#wrapup}

両方の `SQL Report Builder` および `Visual Report Builder` は、様々な使用例に適しています。 これは、通常、分析ニーズと分析を使用するユーザーによって異なります。
