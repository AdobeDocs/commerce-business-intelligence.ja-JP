---
title: ビジュアルReport Builderでの時間オプションの使用
description: 特定の期間に関するレポートのデータを分析する方法を説明します。
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---

# [!DNL Time] での [!DNL Visual Report Builder] オプションの使用

[!DNL Visual Report Builder] の機能の 1 つは、グローバルな `Time Range` と `Interval` 設定です。 これらの設定を使用すると、特定の期間に関するレポートのデータを分析できます。

ただし、一部の分析では、同じレポート内で異なる時間範囲または時間間隔を考慮する必要が生じる場合があります。 そこで、`Time` Options が役に立ちます。 レポートでのオプションの使用方法をより深く理解でき `Time` ように、このチュートリアルでは次のユースケースを扱います。

* [タイムスタンプのない指標の分析](#notimestamp)
* [1 つの指標に独立した時間間隔を指定する](#independenttimeinterval)
* [異なる時間範囲での同じ指標の比較](#difftimerange)

このトピックで説明するサンプルレポートの一部を使用して作業を行う場合は、先に進む前に [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) を開いてください。

## タイムスタンプのない指標の分析 {#notimestamp}

一部の指標では、データが関連付けられたタイムスタンプで収集または保存されないので、時間の経過と共にトレンドを分析できないだけです。 例えば、多くの場合、在庫テーブルには各 SKU に対して 1 行のみが含まれます。 その場合は、タイムスタンプを指定せずに [ 指標を作成 ](../data-user/reports/ess-manage-data-metrics.md) してください。

レポートでこのような指標を使用すると、この指標をレポートに追加すると、`Time Interval` と `None` の独立した `Time Range` が自動的に `Global` 定されます。

![](../assets/Metrics_without_timestamps.gif)

## 1 つの指標に独立した時間間隔を指定する {#independenttimeinterval}

`Time` のオプションを使用すると、時間ベースの 100% グラフを作成して、特定の時間範囲で最も価値を生み出した日、週、月、年を特定できます。 このセクションでは、年の各暦月で生成された収益の割合を示すグラフを作成します。

このタイプのレポートは、前年比で生じた収益を比較する場合に役立ちます。 例えば、2015 年のグラフで、1 月がその年の売上高の 18% を占めていたことが明らかになり、2016 年のグラフでは 8% しか示されませんでした。 何が起きたのかを調べ始めることができます。

1. レポートに `Revenue` 指標を追加します。
1. 「**[!UICONTROL Duplicate]**」をクリックして、指標のコピーを作成します。
1. 「グローバル **[!UICONTROL Time Range]**」オプションをクリックし、「**[!UICONTROL Moving Time Range]**」をクリックします。 これを `Last Year` に設定します。
1. 「グローバル **[!UICONTROL Time Interval]**」オプションをクリックし、「`Monthly`」に設定します。
1. Report Builderは、2 番目の指標の 2 番目の Y 軸を自動的に追加します。 「`Multiple Y-Axes`」ボックスの選択を解除します。
1. 次に、最初の指標に独立した `Time Interval` を適用します。 **[!UICONTROL Time Options]**`first Revenue metric` 右側にある時計アイコンをクリックします。
1. レポートの上に表示される展開ウィンドウで「**[!UICONTROL Time Options]**」をクリックします。
1. ドロップダウンで、次の設定を行います。

   * `Time Interval`：これを `None` に設定します。

   * `Time Range`：最初に `Last Year` をクリックし、次に **[!UICONTROL Custom]** をクリックして、最後に **[!UICONTROL Moving Range]** オプションを選択することで、これを `Last Year` に設定します。

   * 「**[!UICONTROL Apply]**」をクリックして、間隔と範囲の設定を保存します。 これにより、前年の合計売上高を計算する指標が作成されます。 次に、この指標を式の分母として使用します。

   * 各月の売上高の割合を表示するには、レポートに式を追加する必要があります。 「**[!UICONTROL Add Formula]**」をクリックします。

   * 式フィールドに「`B/A`」と入力し、テキストフィールドの横にあるドロップダウンから「`% Percent`」を選択します。 この数式は、特定の月の昨年の収益の金額を、昨年収益の合計金額で除算します。

   * 「**[!UICONTROL Apply Changes]**」をクリックします。

   * 両方の入力指標を非表示にし、式の名前を変更します。

現在、各月が昨年にどの程度影響を与えたかを確認できます。

![](../assets/Independent_Time_Int.png)

## 異なる時間範囲での同じ指標の比較 {#difftimerange}

この例では、「`Day number of the month`」というカスタムディメンションを使用します。 このレポートを作成したいが、Data Warehouseにこのディメンションがまだない場合は、[ サポートにお問い合わせください ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

このカテゴリの 2 つの最も一般的な例は、（1）成長指標（前年度の売上高または前月比の売上高）の比較、（2）最近の在庫または品目販売のトレンドをより深く理解することです。

この使用例を示すには、前年の同月と比較した前月の日次売上高を確認します。 2016 年 1 月の各日の売上高を見て、それを 2015 年 1 月、2014 年 1 月などと比較すると、このレポートにはそれが表示されます。

1. レポートに `Revenue` 指標を追加します。
1. 「**[!UICONTROL Duplicate]**」をクリックして、指標のコピーを作成します。
1. 最初の指標の名前を `Items sold last 7 days` に、2 番目の指標の名前を `Items sold last 28 days` に変更します。
1. 「**[!UICONTROL Time Range]**」をクリックし、「**[!UICONTROL Moving Time Range]**」をクリックします。 これを `Last Month` に設定します。
1. 「**[!UICONTROL Time Interval]**」をクリックし、`None` に設定します。
1. 2 つ目の **[!UICONTROL Time Options]** 指標の横にある `Revenue` （時計アイコン）をクリックします。
1. レポートの上に表示される展開ウィンドウで「**[!UICONTROL Time Options]**」をクリックします。
1. ドロップダウンで、次の設定を行います。

   * `Time Interval`：これを `None` に設定します。

   * `Time Range`：最初に `From 14 Months Ago To 13 Months Ago` をクリックし、次に **[!UICONTROL Custom]** をクリックして、これを **[!UICONTROL Moving Range]** に設定します。 メニュー上部のフィールドとドロップダウンを使用して、範囲を設定します。 この設定を使用すると、前月の売上高を前年に表示できます。

   指標がレポートから消えても心配しないでください。独立した時間オプションを設定すると、レポートから指標が自動的に非表示になります。 再表示するには、指標の横にある「**[!UICONTROL Show]**」をクリックします。

   ![](../assets/Different_Time_Ranges.gif)

   * 「**[!UICONTROL Apply]**」をクリックして、間隔と範囲の設定を保存します。

   * 次に、`Day number of the month` をクリックしてディメンションを選択することで、カスタム **[!UICONTROL Group By]** ディメンションを追加します。 これにより、注文の月の日数が返されます。例えば、3 月 2 日に注文した場合は `2` が返されます。

   * 「`Group By`」ドロップダウンで「`Show All`」を選択し、「**[!UICONTROL Apply]**」をクリックします。 これにより、レポートの X 軸の値が作成されます。

   ![](../assets/TO4.png)

   * 指標の名前を変更します。 この例では、最初の指標は `Revenue - 2015`、2 番目の指標は `Revenue - 2014` です。

カスタム `Time Options` ールのもう 1 つの一般的な使用方法は、供給週を決定することです。 特に、ホリデーシーズンや特別なプロモーション期間の間に、情報に基づいた購入の決定を行うために、先週、月、前のプロモーション期間に販売されたアイテムを検討する必要がある場合があります。

このレポートを自分で作成する場合は、必要に応じて時間範囲を設定することを忘れないでください。

1. レポートに `Items Sold` 指標を追加します。
1. 「**[!UICONTROL Duplicate]**」をクリックして、指標のコピーを作成します。
1. 指標の名前を変更します。 同じ名前を使用することも、似たものを使用することもできます。
   1. 最初の指標の名前を `Items sold last 7 days` に変更します。
   1. 2 番目の指標の名前を `Items sold last 28 days` に変更します。
1. `Items sold last 7 days` 指標で、「グローバル **[!UICONTROL Time Range]**」オプションをクリックし、**[!UICONTROL Moving Time Range]** をクリックします。 この例では、`Last 7 Days` に設定します。
1. 「**[!UICONTROL Time Interval]**」をクリックし、`None` に設定します。
1. 次に、`Time Options` の指標の `Items sold last 28 days` を定義します。 **[!UICONTROL Time Options]**`second Items sold` 指標の右側にある時計アイコンをクリックします。
1. レポートの上に表示される展開ウィンドウで「**[!UICONTROL Time Options]**」をクリックします。
1. ドロップダウンで、次の設定を行います。

   * `Time Interval`：これを `None` に設定します。
   * `Time Range`：最初に「`From 29 days to 1 day ago`」、次に「**[!UICONTROL Custom]**」をクリックして、これを「**[!UICONTROL Moving Range]**」に設定します。 メニュー上部のフィールドとドロップダウンを使用して、範囲を設定します。
   * 「**[!UICONTROL Apply]**」をクリックして、間隔と範囲の設定を保存します。
   * `Items sold last 28 days` 指標を複製し、新しい指標の `Time Options` を開きます。 オプションを次のように設定します。

      * `Time Interval`：これは `None` のままにします。
      * `Time Range`:**[!UICONTROL Specific Date Range]** をクリックして適切な日付を入力することにより、目的のプロモーションに合わせた日付範囲に変更します。
      * 指標の名前を `Items sold during last promotion` などの名前に変更します。
      * `Units on hand` 指標を追加します。
      * 次に、レポートに含める期間（`last 7 days`、`last 28 days` および `last promo` 期間）について、売上トレンドを考慮して手持週数を示す計算を追加する必要があります。 期間ごとに 1 回ずつ実行する必要があります。

数式を作成するには、[**[!UICONTROL Add Formula]**] をクリックします。 以下の数式を入力し、終了したら「**[!UICONTROL Apply Changes]**」をクリックします。 次の 3 つの期間のそれぞれについて、これを繰り返します。

* `last 7 days time period` の場合は、`D / A` フィールドに「`Formula`」と入力します。
* `last 28 days time period` の場合は、`D / (B/4)` フィールドに「`Formula`」と入力します。

  >[!NOTE]
  >
  >選択した時間範囲をここで正規化することが重要です。 この例では 28 日を 4 週間に分割します。 数式に異なるロジックを適用する必要が生じる場合があります。

* `last promo period` の場合は、`D / C` フィールドに「`Formula`」と入力します。

  ![](../assets/Different_Time_Ranges_2.png)

* 最後に、指標を非表示にし、`SKU` または類似のディメンションを `Group By` としてレポートに追加することで、レポートをカスタマイズします。

この例は、現在の在庫レベルが、製品全体で 14 日間の販売に適切に配置されていることを示しています。 ただし、同等のプロモーション期間を追加すると、より多くの在庫を注文し、十分な数の在庫がある商品をプロモーションするだけで、会社はいくつかの変更を加える必要があります。

顧客の動作は時間の経過と共に変化するので、分析を実行する際にデータに違いが生じることが予想されます。 カスタム時間オプションを設定すると、複雑な分析をすばやく作成し、過去のトレンドを考慮したデータ駆動型の決定が可能になります。

