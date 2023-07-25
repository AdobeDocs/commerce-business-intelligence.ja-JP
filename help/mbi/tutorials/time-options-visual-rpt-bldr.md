---
title: ビジュアルReport Builderの [ 時間オプションを使用 ]
description: 特定の期間のレポート内のデータを分析する方法を学びます。
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 0%

---

# 用途 [!DNL Time] のオプション [!DNL Visual Report Builder]

の機能の 1 つ [!DNL Visual Report Builder] グローバル `Time Range` および `Interval` 設定。 これらの設定を使用すると、特定の期間のレポート内のデータを分析できます。

ただし、分析によっては、同じレポート内で異なる時間範囲や時間間隔を考慮する必要が生じる場合があります。 そこにある `Time` オプションが用意されています。 より良い使用方法をお知らせします `Time` レポートのオプションについては、このチュートリアルで次の使用例を扱います。

* [タイムスタンプを使用しない指標の分析](#notimestamp)
* [1 つの指標に独立した時間間隔を設定する](#independenttimeinterval)
* [異なる時間範囲での同じ指標の比較](#difftimerange)

このトピックで取り上げたサンプルレポートの一部に従う場合は、 [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) 続行する前に

## タイムスタンプを使用しない指標の分析 {#notimestamp}

一部の指標では、データが収集されず、関連するタイムスタンプと共に保存されないので、経時的なトレンドを示すことはできません。 例えば、在庫テーブルには、多くの場合、各 SKU に対して 1 つの行のみが含まれます。 その場合、 [指標の作成](../data-user/reports/ess-manage-data-metrics.md) タイムスタンプを指定しないでください。

レポートでこのような指標を使用する場合、この指標をレポートに追加すると、独立した `Time Interval` / `None` および `Time Range` / `Global`:

![](../assets/Metrics_without_timestamps.gif)

## 1 つの指標に独立した時間間隔を設定する {#independenttimeinterval}

`Time` オプションを使用すると、特定の期間に最も貢献した日、週、月、年を示す時間ベースの 100%グラフを作成できます。 このセクションでは、1 年の各月に発生した売上高の割合を示すグラフを作成します。

このタイプのレポートは、前年比で生み出された売上高を比較する場合に役立ちます。 例えば、2015 年のグラフで、1 月の売上高が 18%に達し、2016 年のグラフは 8%しか達していないことが明らかになりました。 何が起こったのか調べ始める事が出来ます

1. を `Revenue` 指標をレポートに追加します。
1. クリック **[!UICONTROL Duplicate]** 指標のコピーを作成します。
1. グローバル **[!UICONTROL Time Range]** オプション、 **[!UICONTROL Moving Time Range]**. これを `Last Year`.
1. グローバル **[!UICONTROL Time Interval]** オプションを選択し、 `Monthly`.
1. Report Builderは、2 番目の指標の 2 番目の Y 軸を自動的に追加します。 選択を解除する `Multiple Y-Axes` ボックス
1. 次に、独立した `Time Interval` を最初の指標に追加します。 クリック **[!UICONTROL Time Options]** （時計のアイコン） `first Revenue metric`.
1. クリック **[!UICONTROL Time Options]** をクリックします。
1. ドロップダウンで、以下を設定します。

   * `Time Interval`:をに設定します。 `None`.

   * `Time Range`:をに設定します。 `Last Year` 最初にクリックして **[!UICONTROL Custom]**&#x200B;を、 **[!UICONTROL Moving Range]**&#x200B;をクリックし、最後に `Last Year` オプション。

   * クリック **[!UICONTROL Apply]** をクリックして、間隔と範囲の設定を保存します。 これにより、前年の合計売上高を計算する指標が作成されます。 次に、この指標を数式の分母として使用します。

   * 各月の売上高の割合を表示するには、レポートに数式を追加する必要があります。 クリック **[!UICONTROL Add Formula]**.

   * 入力 `B/A` 数式フィールドで、「 」を選択します。 `% Percent` を選択します。 この数式では、特定の月からの前年の売上高を、昨年の売上高の合計金額で割ります。

   * クリック **[!UICONTROL Apply Changes]**.

   * 入力指標の両方を非表示にし、数式の名前を変更します。

これで、昨年の各月の影響を調べることができます。

![](../assets/Independent_Time_Int.png)

## 異なる時間範囲での同じ指標の比較 {#difftimerange}

この例では、という名前のカスタムディメンションを使用します。 `Day number of the month`. このレポートを作成し、Data Warehouseにこのディメンションがない場合は、 [連絡先サポート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 助けを求めて

このカテゴリの最も一般的な例は、(1) 成長指標（前年比または前月比）と (2) 最近の在庫または品目の販売傾向をより深く把握できる、という 2 つです。

この使用例を示すために、前年と同じ月と比較した、前月の日別売上高を見てみましょう。 2016 年 1 月の各日の売上高を調べて、2015 年 1 月、2014 年 1 月などと比較すると、このレポートに示されているとします。

1. を `Revenue` 指標をレポートに追加します。
1. クリック **[!UICONTROL Duplicate]** 指標のコピーを作成します。
1. 最初の指標の名前をに変更します。 `Items sold last 7 days` 2 番目の指標は `Items sold last 28 days`.
1. クリック **[!UICONTROL Time Range]**&#x200B;を、 **[!UICONTROL Moving Time Range]**. これを `Last Month`.
1. クリック **[!UICONTROL Time Interval]** を設定し、 `None`.
1. クリック **[!UICONTROL Time Options]** （時計のアイコン）次の `Revenue` 指標。
1. クリック **[!UICONTROL Time Options]** をクリックします。
1. ドロップダウンで、以下を設定します。

   * `Time Interval`:をに設定します。 `None`.

   * `Time Range`:をに設定します。 `From 14 Months Ago To 13 Months Ago` 最初にクリックして **[!UICONTROL Custom]** その後 **[!UICONTROL Moving Range]**. メニュー上部のフィールドとドロップダウンを使用して、範囲を設定します。 この設定を使用すると、前月の売上高を、前年に表示できます。

   レポートに指標が表示されなくなっても、心配する必要はありません。独立時間オプションを設定すると、レポートから指標が自動的に非表示になります。 再表示するには、 **[!UICONTROL Show]** をクリックします。

   ![](../assets/Different_Time_Ranges.gif)

   * クリック **[!UICONTROL Apply]** をクリックして、間隔と範囲の設定を保存します。

   * 次に、カスタム `Day number of the month` クリックによるディメンション **[!UICONTROL Group By]** をクリックし、ディメンションを選択します。 注文月の日数が返されます。例えば、3 月 2 日に発注された注文は、 `2`.

   * 内 `Group By` ドロップダウン、選択 `Show All` をクリックし、 **[!UICONTROL Apply]**. これにより、レポートの X 軸値が作成されます。

   ![](../assets/TO4.png)

   * 指標の名前を変更します。 この例では、最初の指標は `Revenue - 2015` 二つ目は `Revenue - 2014`.

カスタムのもう 1 つの一般的な使用方法 `Time Options` は、何週間もの供給を決定するためのものです。 特に、ホリデーシーズンや特別なプロモーション期間の間に、前週、前月、前のプロモーション期間に販売された品目を考慮して、十分な情報に基づいた購入上の意思決定を行うことができます。

このレポートを自分で作成する際には、必要な時間範囲をに必ず設定してください。

1. を `Items Sold` 指標をレポートに追加します。
1. クリック **[!UICONTROL Duplicate]** 指標のコピーを作成します。
1. 指標の名前を変更します。 同じ名前を使用することも、似たような名前を使用することもできます。
   1. 最初の指標の名前をに変更します。 `Items sold last 7 days`.
   1. 2 番目の指標の名前をに変更します。 `Items sold last 28 days`.
1. の `Items sold last 7 days` 指標を選択し、グローバル **[!UICONTROL Time Range]** オプション **[!UICONTROL Moving Time Range]**. この例では、をに設定します。 `Last 7 Days`.
1. クリック **[!UICONTROL Time Interval]** を設定し、 `None`.
1. 次に、 `Time Options` の `Items sold last 28 days` 指標。 クリック **[!UICONTROL Time Options]** （時計のアイコン） `second Items sold` 指標。
1. クリック **[!UICONTROL Time Options]** をクリックします。
1. ドロップダウンで、以下を設定します。

   * `Time Interval`:をに設定します。 `None`.
   * `Time Range`:をに設定します。 `From 29 days to 1 day ago` 最初にクリックして **[!UICONTROL Custom]**&#x200B;を、 **[!UICONTROL Moving Range]**. メニュー上部のフィールドとドロップダウンを使用して、範囲を設定します。
   * クリック **[!UICONTROL Apply]** をクリックして、間隔と範囲の設定を保存します。
   * を複製します。 `Items sold last 28 days` 指標を選択し、新しい指標の `Time Options`. 次のオプションを設定します。

      * `Time Interval`:これを次のように残す `None`.
      * `Time Range`:これを、 **[!UICONTROL Specific Date Range]** そして適切な日付を入力する
      * 指標の名前を変更 `Items sold during last promotion` 似たようなものです。
      * を `Units on hand` 指標。
      * 次に、販売トレンドを考慮して、期間 (`last 7 days`, `last 28 days`、および `last promo` 期間を含む ) を含める必要があります。 期間ごとに 1 回ずつ実行する必要があります。

数式を作成するには、 **[!UICONTROL Add Formula]**. 以下の式を入力し、 **[!UICONTROL Apply Changes]** 終了したとき。 次の 3 つの期間のそれぞれについて、この手順を繰り返します。

* の `last 7 days time period`を入力して、 `D / A` 内 `Formula` フィールドに入力します。
* の `last 28 days time period`を入力して、 `D / (B/4)` 内 `Formula` フィールドに入力します。

  >[!NOTE]
  >
  >ここで選択した期間を正規化することが重要です。 この例では、28 日を 4 週間に分割します。 場合によっては、数式に別のロジックを適用する必要があります。

* の `last promo period`を入力して、 `D / C` 内 `Formula` フィールドに入力します。

  ![](../assets/Different_Time_Ranges_2.png)

* 最後に、指標を非表示にし、 `SKU` または、 `Group By`.

この例は、現在の在庫レベルが、製品全体の 14 日間の販売に適した場所にあったことを示しています。 ただし、同等のプロモーション期間を追加すると、在庫を増やし、在庫数が十分な品目だけをプロモーションすることで、会社はいくつかの変更を行う必要があることを示しています。

顧客の行動は時間の経過と共に異なるので、分析の実行時にデータの相違を確認できます。 カスタム時間オプションを設定すると、複雑な分析をすばやく作成でき、履歴トレンドを考慮したデータ主導型の決定を可能にします。

