---
title: SQL Report Builderの使用
description: SQL Report Builderを使用したの詳細を説明します。
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1384'
ht-degree: 0%

---

# 使用 [!DNL SQL Report Builder]

>[!NOTE]
>
>が必要 [管理者権限](../../administrator/user-management/user-management.md) sql チャートを作成および編集する手順は、次のとおりです。 `Standard` ユーザーは、ダッシュボード上でこれらのグラフを並べ替えることができます。 `Read-only` ユーザーは、従来のグラフと同じエクスペリエンスを得ることができます。 さらに、 `Read-only` ユーザーはクエリのテキストにアクセスできません。

を参照してください。 [トレーニングビデオ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) を参照してください。

[!DNL SQL]構造化クエリ言語は、データベースとの通信に使用されるプログラミング言語です。 対象： [!DNL Commerce Intelligence], [!DNL SQL] は、Data Warehouseに対してデータのクエリや取得を行うために使用します。 ダッシュボード上のレポートを確認します。各レポートは、その背後で、 [!DNL SQL] クエリ。

を使用できます [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) Data Warehouseを直接クエリするには、結果を表示してグラフに変換します。 でレポートの作成を開始できます [!DNL SQL Report Builder] クリックして **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**.

を参照してください。 [トレーニングビデオ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) を参照してください。

この [!DNL SQL Report Builder] を使用すると、Data Warehouseに対して直接クエリを実行し、結果を確認して、グラフにすばやく変換できます。 の使用に関する最も優れた点 [!DNL SQL] レポートを作成する場合、作成した列に対して繰り返し処理を行うために、更新サイクルを待機する必要はありません。 結果が適切でない場合は、期待どおりになるまで、クエリをすばやく編集して再実行できます。

このトピックでは、を使用する手順を説明します [!DNL SQL Report Builder]. あなたの道を知ったら、 [!DNL SQL] ビジュアライゼーションに関するチュートリアルとして利用したり、記述したクエリの一部を最適化してみたりする場合に使用します。

この記事では、次の内容について説明します。

1. [クエリの作成](#writing)

1. [クエリの実行と結果の表示](#runquery)

1. [ビジュアライゼーションの作成](#createviz)

1. [レポートの保存](#save)

## [!DNL SQL Report Builder] 統合

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) は、 [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md). この機能は開発中です。

の作成を開始するには [!DNL SQL] レポート、クリック **[!UICONTROL Report Builder]** または **[!UICONTROL Add Report]** ダッシュボードの上部 が含まれる [!DNL Report Picker] 画面、クリック **[!UICONTROL SQL Report Builder]** を開きます [!DNL SQL] 編集者。

## はじめに

レポートを編集するには、歯車（![](../../assets/gear-icon.png)の右上隅にある） アイコン [!DNL SQL]ベースのグラフを選択し、 **[!UICONTROL Edit]**.

## クエリの作成 {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] クエリでは大文字と小文字が区別されます。 クエリを記述する際は、正しいケースを使用していることを確認してください。そうでない場合、予期しない結果やエラーが発生する可能性があります。

次に [クエリの最適化のガイドライン](../../best-practices/optimizing-your-sql-queries.md)でクエリを記述します [!DNL SQL] 編集者。

>[!IMPORTANT]
>
>**の指標 [!DNL SQL] 報告書** - SQL レポートに指標を挿入すると、 `current definition` 指標のが使用されます。

指標が将来更新された場合、SQL レポート *次を含まない* 変更を反映します。 変更を有効にするには、レポートを手動で編集する必要があります。

サイドバーの上部にあるボタンを使用すると、で使用できるテーブルと指標のリストを切り替えることができます [!DNL SQL Report Builder]. リストに探しているものが表示されない場合は、サイドバーの上部にある検索バーを使用して検索してみてください。

でサイドバーを使用することもできます [!DNL SQL] 指標、テーブル、列にカーソルを合わせてクリックすることで、クエリに直接指標、テーブル、列を挿入するエディター **[!UICONTROL Insert]**:

![にテーブルを挿入する [!DNL SQL] 編集者。](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>任意 [関数を選択](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST)、または PostgreSQL でサポートされているデータを変更しない関数は、SQL Report Builderでサポートされています。 これには、AVG、COUNT、COUNT DISTINCT、MIN/MAX、SUM などが含まれますが、これらに限定されません。

次のいずれか `JOIN` 型はサポートされていますが、Adobeでは、INNER JOIN を使用することをお勧めします。これは、 `JOIN` タイプ。

## クエリの実行と結果の表示 {#runquery}

クエリの作成が完了したら、 **[!UICONTROL Run Query]**. 結果は、SQL エディターの下のテーブルに表示されます。

![クエリを実行し、結果を表示する。](../../assets/SQL_Run_Query.gif)

結果に誤りがあると思われる場合は、クエリを編集し、問題がなくなるまで再実行できます。

時々は見るかもしれない [エディターの下のメッセージに説明が含まれる](../../best-practices/optimizing-your-sql-queries.md). これらのいずれかが表示された場合は、クエリが実行されておらず、少し微調整が必要であることを意味します。

クエリの編集が完了したら、ビジュアライゼーションの作成または作業内容のダッシュボードへの保存に進むことができます。

## ビジュアライゼーションの作成 {#createviz}

クエリ結果でビジュアライゼーションを作成するには、 **[!UICONTROL Chart]** タブ `Results` ペイン。 このタブでは、次の項目を選択します。

* この `Series`や、測定する列（など） **販売された品目**.
* この `Category`または、データのセグメント化に使用する列（など） **獲得ソース**.
* この `Labels`、または X 軸の値。

ビジュアライゼーションプロセスがどのように表示されるかを次に示します。

![](../../assets/SQL_RB_viz_overview.gif)

ビジュアライゼーションの作成方法に関する詳細な手順については、 [「SQL クエリからのビジュアライゼーションの作成」チュートリアル](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}。

## レポートの保存 {#save}

作業内容を保存する前に、レポートに名前を付ける必要があります。 を忘れずにフォローしてください [の命名に関するベストプラクティスガイドライン](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} して、レポートの内容を明確に伝えるものを選択します。

クリック **[!UICONTROL Save]** の右上隅に [!DNL SQL] エディターでレポートを選択する `Type` （`Chart` または `Table`）に設定します。 まとめるには、レポートの保存先のダッシュボードを選択し、 **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### データの分析

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) を使用すると、Data Warehouseに対して直接クエリを実行し、結果を表示して、レポートにすばやく変換できます。 使用 [!DNL SQL] では、次の操作も実行できます [使用する [!DNL SQL] 使用できない関数](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) が含まれる `Visual` または `Cohort` Report Builderを使用すると、データをより詳細に制御できます。

を使用して作成された計算列 [!DNL SQL] 更新サイクルに依存しないので、自由に繰り返し処理して、すぐに結果を確認できます。

>[!NOTE]
>
>これは列の構造にのみ適用され、データの鮮度には適用されません。 新しいデータは、引き続き、正常に完了した更新サイクルに依存します。

| **これは…に最適です** | **これは…にはあまり良くありません。** |
|---|---|
| 中級/上級アナリスト | 初心者 – あなたは知る必要があります [!DNL SQL]. |
| この [!DNL SQL] 精通した | 単純な分析 – クエリの記述は、単にクエリを使用するよりも作業が複雑になる場合があります。 [!UICONTROL Visual Report Builder]. |
| 1 回限りの計算列の作成 | 他のユーザーとの共有 – 対象オーディエンスを検討します。理解しているか [!DNL SQL]? そうしないと、レポートの作成方法で混乱する可能性があります。 |
| を含むデータ `one-to-many` の関係 |  |
| 新しい列または分析のテスト |  |

#### データベースと SQL エディターの結果

ほとんどの場合、結果の違いは更新サイクルに起因する可能性があります。 次の場合 [!DNL Commerce Intelligence] は、データベースからData Warehouseにデータをレプリケーション中です。同じクエリを使用しても、異なる結果が表示される場合があります。

接続の問題によって、不一致が発生する場合もあります。 に移動します。 `Connections` をクリックしたページ **[!DNL Manage Data** > **Connections]** チェックアウトするには、データベース統合に関するエラーがありますか？ その場合、次が必要になる可能性があります。 [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html) 再び動作させる。

すべての統合が正常に接続され、更新サイクルの途中ではない場合は、他の何かが問題である可能性があります。

#### 削除の実行 [!DNL SQL] レポートでData Warehouseから基になる列も削除しますか？

いいえ、どのように構築したかに関係なく、Data Warehouseから列が失われることはありません。

を使用して作成された列 `Data Warehouse Manager` これらを使用するレポートまたはクエリを削除しても、影響を受けません。

を使用して作成された列 [!DNL SQL Report Builder] はData Warehouseに保存されていません。


#### `Report Builder` 対 `SQL Report Builder`

この [!DNL SQL Report Builder] を使用すると、グラフを作成および構造化する際の柔軟性が向上します。例えば、で表示する値を選択できます `X` および `Y` 軸： でのグラフの作成について詳しくは、 [!DNL SQL Report Builder]を確認してください。 [からのビジュアライゼーションの作成 [!DNL SQL] クエリ](../../tutorials/create-visuals-from-sql.md) チュートリアル。

#### `Cohort Report Builder` {#cohortrb}

と異なります。 [!DNL Visual Report Builder], [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) は、類似したユーザーグループの行動のトレンドを時間の経過と共に分析および特定する、単一の目的を対象としています。 使用， [!DNL Cohort Report Builder] は次を必要としません [!DNL SQL] 知識が豊富なので、始めたばかりの場合でも、ためらうことなくダイビングできます。

| **これは…に最適です** | **これは…にはあまり良くありません。** |
|---|---|
| 中級/上級アナリスト | 初心者 – あなたは練習を定義するコホートが必要です。 |
| 行動の経時的なトレンドの特定 | 定性分析 – 次のことが可能です [完了](../dev-reports/create-qual-cohort-analysis.md)ただし、Adobeの支援が必要です。 |

## 更新サイクル後のクエリの再構築

クエリを再構築する必要はありません。 を使用して作成されたレポート [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) は、従来ので作成したように保存されます `Report Builder`. の更新プロセス [!DNL SQL] グラフは同じです。データを更新すると、グラフの値が再計算され、再表示されます。

>[!NOTE]
>
>を削除する場合 [!DNL SQL] レポート/クエリの場合、基になる列はData Warehouseから削除されません。 列の作成方法にかかわらず、列は失われません。

* Data Warehouse・マネージャを使用して作成された列は、それらを使用するレポートまたは問合せを削除しても影響を受けません。

* SQL Report Builderを使用して作成された列は、Data Warehouseに保存されません。

## まとめ {#wrapup}

もう少し難しいことに挑戦する場合は、ビジュアライゼーションに最適化されたクエリを記述してみませんか？ を確認してください。 [からのビジュアライゼーションの作成 [!DNL SQL] クエリチュートリアル](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} をクリックして開始してください。
