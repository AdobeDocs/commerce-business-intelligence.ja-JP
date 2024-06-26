---
title: レプリケーションメソッドの設定
description: テーブルを整理する方法と、テーブルデータの動作によってテーブルに最適なレプリケーション方法を選択する方法について説明します。
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---

# レプリケーションメソッドの設定

`Replication` メソッドと [再チェック](../data-warehouse-mgr/cfg-data-rechecks.md) を使用して、データベーステーブル内の新しいデータや更新されたデータを識別します。 これらを正しく設定することは、データの精度と最適な更新時間の両方を確保するために重要です。 このトピックでは、レプリケーション方法に焦点を当てます。

で新しいテーブルが同期されたとき [Data Warehouse管理者](../data-warehouse-mgr/tour-dwm.md)の場合、レプリケーション方法がテーブルに対して自動的に選択されます。 様々なレプリケーション方法、テーブルの編成方法、テーブルデータの動作について理解しておくと、テーブルに最適なレプリケーション方法を選択できます。

## レプリケーション方法を教えてください。

`Replication` メソッドは 3 つのグループに分類されます。 `Incremental`, `Full Table`、および `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) という意味です [!DNL Commerce Intelligence] レプリケーションを実行するたびに、新しいデータまたは更新されたデータのみをレプリケートします。 これらの方法で待ち時間が大幅に短縮されるので、Adobeでは可能な限りこれを使用することをお勧めします。

[**[!UICONTROL Full Table Replication]**](#fulltable) という意味です [!DNL Commerce Intelligence] レプリケーションが試行されるたびに、テーブルのコンテンツ全体がレプリケートされます。 レプリケートされるデータは大量になる可能性があるので、これらの方法によって待ち時間と更新時間が長くなる場合があります。 テーブルにタイムスタンプ付きまたは日時の列が含まれる場合、Adobeでは、代わりに増分処理メソッドを使用することをお勧めします。

**[!UICONTROL Paused]** テーブルのレプリケーションが停止または一時停止されていることを示します。 [!DNL Commerce Intelligence] は、更新サイクル中に新しいデータまたは更新されたデータをチェックしません。つまり、これがレプリケーション方法として設定されているテーブルからデータがレプリケートされることはありません。

## 増分レプリケーション方法 {#incremental}

### 変更日時（最も理想的）

この `Modified At` レプリケーション・メソッドでは、datetime 列を使用して、レプリケートするデータを検索します。この列は、行が作成されると入力され、データが変更されると更新されます。 この方法は、次の条件を満たすテーブルを操作するように設計されています。

* 次を含む `datetime` 行の作成時に最初に入力され、行が変更されるたびに更新される列。
* この `datetime` 列が null になることはありません。
* 行はテーブルから削除されません

これらの条件に加えて、Adobeでは次のことをお勧めします **索引付け** この `datetime` 使用する列 `Modified At` レプリケーションは、レプリケーション速度の最適化に役立ちます。

更新を実行すると、に値を持つ行を検索することで、新しいデータまたは変更されたデータが識別されます。 `datetime` 最新の更新後に発生した列。 新しい行が検出されると、それらがData Warehouseにレプリケートされます。 に行が存在する場合、 [Data Warehouse管理者](../data-warehouse-mgr/tour-dwm.md)現在のデータベース値で上書きされます。

例えば、テーブルにはという列がある場合があります。 `modified\_at` これは、データが最後に変更された時刻を示します。 最新の更新が正午に火曜日に実行された場合、更新では、を持つすべての行が検索されます `modified\_at` 正午の火曜日より大きい値。 火曜日の正午から作成または変更された検出された行はすべて、Data Warehouseにレプリケートされます。

**ご存じでしたか？**
データベースが現在をサポートしていない場合でも、 `Incremental` レプリケーション方法。次のことが可能です。 [データベースに変更を加える](../../best-practices/mod-db-inc-replication.md) それは～の利用を可能にするだろう `Modified At` または `Single Auto Incrementing PK`.

`Modified At` 最も理想的なレプリケーション方法であるだけでなく、最速のレプリケーション方法でもあります。 この方法は、大きなデータセットで顕著な速度の増加を引き起こすだけでなく、再チェックオプションを設定する必要もありません。 他のメソッドは、データの小さなサブセットが変更された場合でも、変更を特定するためにテーブル全体を反復処理する必要があります。 `Modified At` その小さなサブセットのみを反復処理します。

### 1 つの自動増分プライマリキー

`Auto Incrementing` は、ローにプライマリ・キーを順番に割り当てる動作です。 テーブルが `Auto Incrementing` テーブルの最上位の主キーが 1,000 で、次の主キーの値が 1,001 以上である。 を使用しないテーブル `Auto Incrementing` ビヘイビアーは、1,000 未満のプライマリキー値を割り当てたり、はるかに大きな数値にジャンプしたりできますが、これは一般的には使用されません。

この方法は、次の条件を満たすテーブルから新しいデータをレプリケートするように設計されています。

* `single-column primary key`、および
* `primary key` データタイプは `integer`、および
* `auto incrementing` プライマリキーの値。

テーブルが以下を使用している場合 `Single Auto Incrementing Primary Key` レプリケーションでは、Data Warehouse内の現在の最大値より大きいプライマリ・キー値を検索することで、新しいデータが検出されます。 例えば、Data Warehouseの最上位のプライマリキー値が 500 の場合、次の更新の実行時に、プライマリキー値が 501 以上の行が検索されます。

### 日付を追加

この `Add Date` メソッドの機能はと同様です。 `Single Auto Incrementing Primary Key` メソッド。 このメソッドでは、テーブルのプライマリキーに整数を使用する代わりに、 `timestamped` 新しい行をチェックする列。

テーブルで以下を使用するとき `Add Date` レプリケーションの場合、新しいデータは、Data Warehouseに同期された最新の日付より大きいタイムスタンプ付きの値を検索することで検出されます。 例えば、更新が最後に実行されたのは 2015 年 12 月 20 日 09 です:00:00 の場合、タイムスタンプがこの値より大きい行は、新しいデータとしてマークされ、レプリケートされます。

>[!NOTE]
>
>と異なります。 `Modified At` メソッド、 `Add Date` は、既存の行の更新された情報をチェックしません。新しい行のみを期待します。

## フルテーブルのレプリケーションメソッド {#fulltable}

### フル テーブル

`Full table` 新しい行が検出されるたびに、レプリケーションによってテーブル全体が更新されます。 これは、新しい行があると仮定して、すべてのデータを更新時に再処理する必要があるため、最も効率的なレプリケーション方法ではありません。

同期処理の開始時にデータベースに対してクエリを実行し、行数をカウントすることで、新しい行が検出されます。 ローカルデータベースによりも多くの行が含まれている場合 [!DNL Commerce Intelligence]を選択すると、テーブルが更新されます。 行数が同じ場合、または [!DNL Commerce Intelligence] 次を含む *詳細* ローがローカル・データベースより多い場合、テーブルはスキップされます。

これは重要な点を提起する **`Full Table`次の場合、レプリケーションに互換性がありません。**

* 後続の更新サイクルの間に、ローカルデータベーステーブルで作成された行よりも多くの行が削除される。
* 列の値は変更されますが、行は追加されません

上記のシナリオのいずれかで、 `Full Table` レプリケーションで変更が検出されず、データが古くなります。 このレプリケーション方法は非効率であり、前述の要件により、 `Full Table` レプリケーションは、最後の手段としてのみ推奨されます。

### プライマリキーバッチ

テーブルで以下を使用するとき `Primary Key Batch` （PK バッチ）、プライマリキー値の範囲（バッチ）内の行をカウントすることで、新しいデータが検出されます。 通常、これは整数で使用されると考えられますが、テキスト値でも、システムが定数範囲を定義できる方法で並べ替えることができます。

例えば、更新が実行され、1 から 100 のキーの範囲に対して行数が計算されるとします。 この更新では、システムは 37 行を検索してログに記録します。 次の更新では、1 ～ 100 の範囲で行数が再び実行され、41 行が検索されます。 最後の更新と比較すると行数に違いがあるので、システムはその範囲（またはバッチ）をより詳細に調べます。

この方法は、次の条件を満たすテーブルからデータをレプリケートすることを目的としています。

* 単一カラムの整数以外、または
* 複合キー（プライマリキーを構成する複数の列） – 複合プライマリキーで使用される列に null 値を指定することはできません。
* 単一カラム、整数、プライマリ・キー値を自動増分しない。

バッチを調査して変更を見つけるために発生する必要がある処理の量が原因で非常に遅いので、この方法は理想的ではありません。 Adobeでは、他のレプリケーション方式をサポートするために必要な変更を加えることが不可能な場合を除き、この方式を使用しないことをお勧めします。 このメソッドを使用する必要がある場合は、更新時間が長くなることが予想されます。

## レプリケーションメソッドの設定

レプリケーション方法はテーブル単位で設定されます。 テーブルのレプリケーション方法を設定するには、次が必要です [`Admin`](../../administrator/user-management/user-management.md) Data Warehouseマネージャーにアクセスできる権限。

1. Data Warehouseマネージャーで、 `Synced Tables` リストを使用して、テーブルのスキーマを表示します。
1. 現在のレプリケーション方法がテーブル名の下に表示されます。 変更するには、リンクをクリックします。
1. 表示されるポップアップで、次のいずれかの横にあるラジオボタンをクリックします `Incremental` または `Full Table` replication：レプリケーションタイプを選択します。
1. 次に、 **[!UICONTROL Replication Method]** ドロップダウンでメソッドを選択します。 例： `Paused` または `Modified At`.

   >[!NOTE]
   >
   >**一部の増分処理メソッドでは、`Replication Key`**. [!DNL Commerce Intelligence] は、このキーを使用して、次回の更新サイクルを開始する場所を決定します。
   >
   >例えば、 `modified at` のメソッド `orders` テーブル、を設定する必要があります `date column` レプリケーションキーとして。 レプリケーションキーには複数のオプションが存在する場合がありますが、選択するのは次の場合です `created at`、または注文が作成された時刻。 最後の更新サイクルが 2015 年 12 月 1 日に停止した場合 00:10:00：次のサイクルでは、データのレプリケーションが `created at` この日付より後の日付。

1. 終了したら、 **[!UICONTROL Save]**.

プロセス全体を見てみましょう。

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## まとめ

最後に、さまざまなレプリケーション方法を比較するこのテーブルを作成しました。 Data Warehouse内のテーブルのメソッドを選ぶ際に非常に便利です。

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | 速い | 遅い | 不可 | 不可 | 不可 | はい |
| `Primary Key Batch Monitoring` | 遅い | 遅い | はい | はい | はい | はい |
| `Modified At` | 速い | 速い | はい | はい | はい | 不可 |

{style="table-layout:auto"}

## 関連ドキュメント

* [データの再チェックについて](../data-warehouse-mgr/cfg-data-rechecks.md)
* [サポートするようにデータベースを変更する ](../../best-practices/mod-db-inc-replication.md)
* [分析のためのデータベースの最適化](../../best-practices/opt-db-analysis.md)
* [更新時間の短縮](../../best-practices/reduce-update-cycle-time.md)
