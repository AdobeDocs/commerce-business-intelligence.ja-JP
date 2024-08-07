---
title: 「上/下を表示」機能を使用したデータの順序付け
description: 上と下を表示機能を使用してデータを並べ替える方法を説明します。
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---

# `Show Top/Bottom` 機能を使用したデータの順序付け

時間の経過に伴うトレンドを分析して作成するより、より多くの作業を `Visual Report Builder` で行うことができます。 例えば、獲得チャネルとマーケティングチャネルの価値を示すレポートを作成できますが、上位 5 人の実行者のみを示すレポートを作成することもできます。 同様に、最も売上高が多い州を示すレポートを作成して、マーケティング活動を再フォーカスできます。

このようなデータの並べ替えと並べ替えは、`Group By` と `Time Interval of None` の両方を使用するレポートで実行できます。 これらの要素の両方がレポート内にある場合、`Show Top/Bottom` 機能はグラフのプレビューの上に表示されます。 この機能を使用すると、設定したパラメーターに基づいて、上（最大から最小）および下（最小から最大）のデータポイントを表示できます。

![ ビジュアルReport Builderで上/下機能を表示します。](../../assets/Show_Top_Bottom.png)

## これはどうやって使うのですか。 {#how}

**[!UICONTROL Show Top/Bottom link]** をクリックして、表示および並べ替えパラメーターを設定します。 テキストボックスに入力できる数値は、整数（`5` など）または `ALL` です。 次に、指標またはグループ化でレポートを並べ替えるように選択できます。

例えば、最も多くの売上高をもたらした 5 つのリファラルソースを表示する場合は、次の方法で行います。

1. レポートに `Revenue` 指標を追加します。

1. リファラルソース別に指標をセグメント化する `Group By` を追加します。

1. `Time Interval` を `None` に設定します。

1. `Show Top/Bottom` の設定で、表示を `5` に設定して、上位 5 つの合計収益金額を持つリファラルソースのみがレポートに含まれるようにします。

>[!NOTE]
>
>レポートには `Time Interval` がないため、値（この場合は上位 5 つのリファラルソース）は時間の経過と共に変化する可能性があります。 ある参照元が売上高の点で別の参照元を上回る場合、参照元の表示順序が変更されます。

## 複数の指標を使用する場合はどうですか？ {#multiplemetrics}

各指標は単独またはグループの 1 つによってのみ並べ替えできるので、tHere がレポート内の複数の指標となる場合、この機能の使用は複雑になります。

例えば、`Revenue` 指標と `Number of orders` 指標の両方をリファラルソースでグループ化したレポートを作成したとします。 `Revenue` は `Revenue` または参照元でのみ並べ替えることができ、`Number of orders` は `Number of orders` または参照元でのみ並べ替えることができます。

つまり、上位 `5` の収益発生のリファラルソースのみの `Revenue` ールを表示することはできますが、上位 `5` の収益発生のリファラルソースの注文数も表示することはできません。 簡単に言えば、複数の指標がある場合、グループで各指標を並べ替えることをお勧めします。

以下は、グループ化ではなく `Revenue` 指標そのものを並べ替えたグラフの例です。 ご覧のように、指標をグループ化で並べ替えると、奇妙な（そして最終的には役に立たない）レポートが作成されます。

![ 不審で役に立たないレポートの結果 ](../../assets/strange-report-results.png)

両方の指標をグループ化で並べ替えた場合、グラフは次のようになります。

![ グループ化による両方の指標の並べ替え ](../../assets/sort-metrics-by-grouping.png)

## デフォルトでは、値はどのように並べ替えられていますか？ {#defaultsorting}

`Group by` と `Time Interval` が `None` のレポートに含まれる指標が 1 つだけの場合、`Visual Report Builder` のデフォルトの順序は、指標に基づいて上位の値を表示することです。 この場合、ニーズに合う場合は、`Show Top/Bottom` 機能は必要ない可能性があります。

この例では、営業担当者がクローズしたオポチュニティの数を確認します。 このテーブルは、指標（この場合は `Won Opportunities`）に基づいて高い順に自動的に並べ替えられます。

![ 指標による並べ替え ](../../assets/Ordered_by_metric.png)

ただし、2 番目の指標を追加した場合、デフォルトでは、グループ化に基づいて上位のが並べ替えられます。 指標とグループ化を追加すると、デフォルトの並べ替えは最初のグループ化に基づいて、次に 2 番目のグループ化に基づいて、というように行われます。

![ グループ化による順序付け ](../../assets/Ordered_by_grouping.png)

## まとめ {#wrapup}

ここでは、いくつかの基本機能について説明しますが、この機能には多くの興味深い用途があります。

前の担当営業とオポチュニティの例について考えます。 `Time Interval` を削除し、`Group By` を適用し、グループ化に基づいてデータを並べ替えると、各担当者の獲得商談数の詳細が得られます。 また、`Show Top/Bottom` 機能を使って、トップパフォーマーが誰であるかを見つけましょう。
