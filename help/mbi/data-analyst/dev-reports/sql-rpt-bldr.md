---
title: SQLReport Builderの使用
description: SQLReport Builderの使用方法を学びます。
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
source-git-commit: 09b6983c3e06a1f18035542dfa3b9de9ac3ceb38
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 0%

---

# 使用 `SQL Report Builder`

>[!NOTE]
>
>必要 [管理者権限](../../administrator/user-management/user-management.md) をクリックし、SQL チャートを作成および編集します。 `Standard` ユーザーは、ダッシュボードでこれらのグラフを並べ替えることができます。 `Read-only` ユーザーは、従来のグラフと同じエクスペリエンスを得ることができます。 さらに、 `Read-only` ユーザーはクエリのテキストにアクセスできません。

詳しくは、 [トレーニングビデオ](https://support.magento.com/hc/en-us/articles/360016730131) を参照してください。

`SQL`(Structured Query Language) は、データベースとの通信に使用されるプログラミング言語です。 In [!DNL MBI]の場合、SQL を使用して、Data Warehouse からデータをクエリしたり、取得したりします。 ダッシュボード上のレポートを見てみましょう。バックグラウンドで、各レポートは SQL クエリによって実行されます。

以下を使用して、 [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) data warehouse に直接問い合わせ、結果を表示し、グラフに変換します。 レポートの作成を開始するには、 `SQL Report Builder` 移動して **[!UICONTROL Report Builder** > **SQL Report Builder]**.

詳しくは、 [トレーニングビデオ](https://support.magento.com/hc/en-us/articles/360016730131-Training-Video-SQL-Report-Builder) を参照してください。

この `SQL Report Builder` では、Data Warehouse に直接問い合わせ、結果を表示し、すばやくグラフに変換できます。 SQL を使用してレポートを作成する最善の方法は、 [列で反復する更新サイクルを待つ必要はありません](https://support.magento.com/hc/en-us/articles/360016506212) 自分で作成します。 結果が正しく表示されない場合は、クエリをすばやく編集し、期待どおりに実行できます。

この記事では、 `SQL Report Builder`. 使い方がわかったら、ビジュアライゼーションに関する SQL のチュートリアルを確認するか、記述したクエリの一部を最適化してみてください。

この記事で取り上げる内容の概要を次に示します。

1. [クエリの作成](#writing)

1. [クエリの実行と結果の表示](#runquery)

1. [ビジュアライゼーションの作成](#createviz)

1. [レポートの保存](#save)

## SQLReport Builderの統合

世界の現在の状態では [[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) は、と共に使用できない唯一の統合です。 [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md). この機能は、今後のリリースで追加する予定です。

新しい SQL レポートの作成を開始するには、 **[!UICONTROL Report Builder]** または **[!UICONTROL Add Report]** をクリックします。 内 `Report Picker` 画面、クリック **[!UICONTROL SQL Report Builder]** をクリックして SQL エディタを開きます。

## はじめに

レポートを編集するには、歯車 (![](../../assets/gear-icon.png)) アイコンをクリックし、 **[!UICONTROL Edit]**.

## クエリの作成 {#writing}

>[!NOTE]
>
>`SQL Report Builder` クエリでは大文字と小文字が区別されます。 クエリを記述する際は、正しいケースを使用していることを確認してください。そうしないと、予期しない結果やエラーが発生する場合があります。

次の [クエリ最適化のガイドライン](../../best-practices/optimizing-your-sql-queries.md)を使用する場合は、SQL エディターでクエリを記述します。

>[!IMPORTANT]
>
>**SQL レポートの指標** - SQL レポートに指標を挿入すると、 `current definition` 」と入力します。

指標が将来更新される場合、SQL レポート *次の条件を満たさない* 変更が反映されます。 変更を反映させるには、レポートを手動で編集する必要があります。

サイドバーの上部にあるボタンを使用して、テーブルのリストと、 `SQL Report Builder`. リストに何を探しているかが表示されない場合は、サイドバーの上部にある検索バーを使用して検索してみてください。

SQL エディターのサイドバーを使用して、指標、テーブルおよび列の上にマウスポインターを置いて「 **[!UICONTROL Insert]**:

![SQL エディタにテーブルを挿入します。](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>任意 [SELECT 関数](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST)、または PostgreSQL でサポートされるデータを変更しない関数は、SQLReport Builderでサポートされます。 これには、AVG、COUNT、COUNT DISTINCT、MIN/MAX、SUM などが該当しますが、これらに限定されません。

また、JOIN タイプもサポートされていますが、JOIN タイプのコストが最も低いので、INNER JOIN のみを使用することをお勧めします。

## クエリの実行と結果の表示 {#runquery}

クエリの記述が完了したら、「 **[!UICONTROL Run Query]**. 結果は、SQL エディターの下の表に表示されます。

![クエリを実行し、結果を表示する。](../../assets/SQL_Run_Query.gif)

結果に何か問題があるように見える場合は、問題が発生するまでクエリを編集し、クエリを再実行できます。

時々、 [エディタの下に EXPLAIN を含むメッセージ](../../best-practices/optimizing-your-sql-queries.md). これらのいずれかが表示される場合は、クエリが実行されておらず、微調整が必要です。

クエリの編集が完了したら、ビジュアライゼーションの作成またはダッシュボードへの作業の保存に進むことができます。

## ビジュアライゼーションの作成 {#createviz}

クエリ結果を使用してビジュアライゼーションを作成するには、 **[!UICONTROL Chart]** 」タブをクリックします。 `Results` ウィンドウ このタブでは、次の項目を選択します。

* この `Series`または、測定する列（例： ） **販売済みアイテム**.
* この `Category`または、データのセグメント化に使用する列 ( 例： **獲得ソース**.
* この `Labels`または X 軸の値。

次に、ビジュアライゼーションプロセスの概要を示します。

![](../../assets/SQL_RB_viz_overview.gif)

ビジュアライゼーションの作成方法について詳しくは、 [SQL クエリからのビジュアライゼーションの作成のチュートリアル](../../tutorials/create-visuals-from-sql.md){:target=&quot;_blank&quot;}。

## レポートの保存 {#save}

作業内容を保存する前に、レポートに名前を付ける必要があります。 忘れずに [命名に関するベストプラクティスのガイドライン](../../best-practices/naming-elements.md){:target=&quot;_blank&quot;} を選択し、レポートの内容を明確に伝えるものを選択します。

クリック **[!UICONTROL Save]** をクリックし、SQL エディターの右上隅にあるレポートを選択します。 `Type` (`Chart` または `Table`) をクリックします。 まとめるには、レポートの保存先となるダッシュボードを選択し、「 **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### データの分析

#### `SQL Report Builder`

[`The SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) では、Data Warehouse に直接問い合わせ、結果を表示し、それらをレポートにすばやく変換できます。 SQL を使用すると、 [使用できない SQL 関数を使用するには](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) 内 `Visual` または `Cohort` Report Builderを使用して、データをより詳細に制御できます。

SQL を使用して作成された計算列は更新サイクルに依存しないので、好きなように繰り返し実行し、すぐに結果を確認できます。

>[!NOTE]
>
>これは列の構造にのみ適用され、データの鮮度には適用されません。 新しいデータは、正常に完了した更新サイクルに依存します。

| **これは…に最適です。** | **これは…** |
|---|---|
| 中級アナリスト/上級アナリスト | 初心者 — SQL を知る必要があります。 |
| SQL に精通している | 単純な分析 — クエリの記述は、単にビジュアルReport Builderを使用するよりも簡単に行えます。 |
| 1 回限りの計算列の作成 | 他のユーザーと共有する — オーディエンスを考慮：SQL を理解しているか そうでない場合は、レポートの作成方法に混乱する可能性があります。 |
| データの格納先 `one-to-many` 関係 |  |
| 新しい列または分析のテスト |  |

#### データベースと SQL エディタの結果

時間の大部分は、結果の違いは、更新サイクルに起因する可能性があります。 If [!DNL MBI] は、データベースからData Warehouseにデータをレプリケートするプロセス中で、同じクエリを使用している場合でも、異なる結果が表示される場合があります。

接続の問題によって不整合が生じる場合もあります。 次に移動： `Connections` ページをクリック **[!DNL Manage Data** > **Connections]**) を使用してチェックアウトします。問題のデータベース統合にエラーはありますか。 その場合は、 [統合の再認証](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations) もう一度動かすために

すべての統合が正常に接続され、更新サイクルの途中にない場合は、他に何か問題が発生する可能性があります。 その場合は、 [データ相違トラブルシューティングガイド](https://support.magento.com/hc/en-us/sections/360003074492) サポートサイトで問題を特定できます。

#### SQL レポートを削除すると、基になる列もData Warehouseから削除されますか。

いいえ。どのように作成したかに関係なく、Data Warehouseから列が失われることはありません。

を使用して作成された列 `Data Warehouse Manager` を使用するレポートまたはクエリを削除しても、影響は受けません。

を使用して作成された列 `SQL Report Builder` はData Warehouseに保存されません。


#### `Report Builder` 対比 `SQL Report Builder`

この `SQL Report Builder` を使用すると、グラフを作成および構造化する際に柔軟性が高まります。例えば、表示する値を選択できます `X` および `Y` 軸 グラフの作成について詳しくは、 `SQL Report Builder`以下をご確認ください。 [SQL クエリからのビジュアライゼーションの作成](../../tutorials/create-visuals-from-sql.md) チュートリアル

#### `Cohort Report Builder` {#cohortrb}

とは異なり、 `Visual Report Builder`、 [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) は、単一の目的を目的としており、類似したユーザーグループの行動トレンドを経時的に分析および識別します。 コホートReport Builderを使用する場合、SQL に関する知識は必要ありません。したがって、使い始めたばかりであれば、ためらうことなくすぐに飛び込むことができます。

| **これは…に最適です。** | **これは…** |
|---|---|
| 中級アナリスト/上級アナリスト | 初心者 — コホートを定義する練習が必要です。 |
| 経時的な行動トレンドの特定 | 定性分析 — 可能 [完了](../dev-reports/create-qual-cohort-analysis.md)ですが、サポートが必要です。 |

## 更新サイクル後の問合せの再構築

クエリを再構築する必要はありません。 を使用して作成されたレポート [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) は、従来の `Report Builder`. SQL グラフの更新プロセスはまったく同じです。データが更新されると、グラフの値が再計算され、再表示されます。

>[!NOTE]
>
>SQL レポート/クエリを削除しても、基になる列はData Warehouseから削除されません。 どのように作成したかに関係なく、列は失われません。

* Data Warehouseマネージャを使用して作成した列は、それらを使用するレポートまたはクエリを削除しても影響を受けません。

* SQLReport Builderを使用して作成した列はData Warehouseに保存されません。

## 折り返し {#wrapup}

もう少し難しいことを試したい場合は、ビジュアライゼーション用に最適化されたクエリを記述してみてはどうですか。 以下をご確認ください。 [SQL クエリからのビジュアライゼーションの作成のチュートリアル](../../tutorials/create-visuals-from-sql.md){:target=&quot;_blank&quot;} をクリックして開始します。
