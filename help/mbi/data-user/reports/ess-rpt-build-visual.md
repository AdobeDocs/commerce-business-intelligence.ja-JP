---
title: ビジュアルReport Builder
description: ビジュアルReport Builderの使用方法
exl-id: 1101f43d-e014-4df2-be21-12d90a9d8a56
source-git-commit: df81d2b036d00cd53274ec1ae22031dbf06cc948
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# [!DNL Visual Report Builder]

[!DNL Visual Report Builder] では、事前定義された指標に基づくクイックレポートを簡単に作成できます。 各指標には、レポートのデータのセットを定義するクエリが含まれます。

次の例では、シンプルなレポートの作成、追加のディメンションでのデータのグループ化、日付と時間間隔の設定、グラフタイプの変更、レポートのダッシュボードへの保存を行う方法を示します。

## シンプルなレポートを作成するには：

1. 内 [!DNL Commerce Intelligence] メニュー、クリック **[!UICONTROL Report Builder]**.

1. の下 [!UICONTROL Visual Report Builder]をクリックし、 **[!UICONTROL Create Report]** 次の操作を実行します。

   * クリック **[!UICONTROL Add Metric]**.

      使用可能な指標は、アルファベット順またはテーブル別に一覧表示できます。

      ![ビジュアルReport Builder](../../assets/magento-bi-visual-report-builder-add-metric.png)

   * を選択します。 [指標](../../data-user/reports/ess-manage-data-metrics.md) レポートに使用する一連のデータを表します。

      この `New Customers` この例で使用される指標では、すべての顧客がカウントされ、顧客がアカウントに新規登録した日付でリストが並べ替えられます。 最初のレポートには、シンプルな折れ線グラフに続くデータのテーブルが含まれます。

      左側の概要には、現在の指標の名前が表示され、その後に、指標で指定された列データに対する計算の結果が表示されます。 この例では、概要に顧客の総数が表示されます。

      ![ビジュアルReport Builder](../../assets/magento-bi-report-builder-untitled.png)

1. グラフで、線の各データポイントにカーソルを合わせます。 各データポイントは、その月に新規登録した顧客の合計数を示します。

1. データのグループ化、日付範囲の変更およびグラフタイプを行うには、次の手順に従います。

   **`Group By`**

   この `Group By` 「 」コントロールを使用すると、複数のディメンションをグループまたはセグメント別に追加できます。 Dimensionは、データのグループ化に使用できるテーブル内の列です。

   * 次のリストから、使用可能なディメンションの 1 つを選択します。 `Group By` オプション。

      この例では、顧客が最初の注文時に使用したクーポンコードが 5 つ見つかりました。

      ![グループ化の基準](../../assets/magento-bi-report-builder-group-by-dimensions.png)

      この `Group By` 顧客が使用する各クーポンの詳細リストが表示されます。 最初の注文をおこなうために使用されたクーポンは、チェックボックスでマークされます。 グラフに、1 回目の注文で使用された各クーポンを表す、複数の色付きの線が表示されるようになりました。 凡例は、データの各行に対応するように色分けされます。

   * クリック **[!UICONTROL Apply]** をクリックして、Group By の詳細を閉じます。

      ![複数のDimension](../../assets/magento-bi-report-builder-group-by-dimension-detail.png)

   * 各行のデータポイントにマウスポインターを置くと、その月にそのクーポンを使用し、最初の注文時にそのクーポンを使用した顧客の数が表示されます。

   * データのテーブルに、追加のディメンションが追加され、各月に列が、各クーポンコードに行が追加されるようになりました。

      ![テーブルデータでグループ化](../../assets/magento-bi-report-builder-group-by-table-data.png)

   * 移動 (![](../../assets/magento-bi-btn-transpose.png)) コントロールを使用して、データの向きを変更できます。

      データ軸が反転し、テーブルに各クーポンコードの列と、各月の行が表示されるようになりました。 この向きは読みやすいかもしれません。

      ![転送されたデータ](../../assets/magento-bi-report-builder-group-by-table-data-transposed.png)
   **`Date Range`**

   この `Date Range` コントロールは、現在の日付範囲と時間間隔の設定を表示し、右側のグラフのすぐ上に配置されます。

   * 次をクリック： `Date Range` コントロール ( この例では `All-Time by Month`.

      ![日付範囲](../../assets/magento-bi-report-builder-date-range.png)

   * 次の変更を行います。

      * 拡大して表示を拡大するには、日付範囲を `Last Full Quarter`.
      * の下 `Select Time Interval`選択 `Week`.
      * 完了したら、「 **[!UICONTROL Save]**.

      レポートには、前四半期のデータのみが週別に含まれるようになりました。

      ![前四半期のレポートを週別に表示](../../assets/magento-bi-report-builder-date-range-quarter-by-week-chart.png)
   **グラフのタイプ**

   * 右上隅のコントロールをクリックして、データに最適なグラフを見つけます。

      一部のグラフの種類は、多次元データと互換性がありません。

      |  |  |
      |-----|-----|
      | ![](../../assets/magento-bi-btn-chart-line.png) | 折れ線グラフ |
      | ![](../../assets/magento-bi-btn-chart-horz-bar.png) | 横棒グラフ |
      | ![](../../assets/magento-bi-btn-chart-horz-stacked-bar.png) | 積み重ね横棒グラフ |
      | ![](../../assets/magento-bi-btn-chart-vert-bar.png) | 縦棒グラフ |
      | ![](../../assets/magento-bi-btn-chart-vert-stacked-bar.png) | 積み重ね縦棒グラフ |
      | ![](../../assets/magento-bi-btn-chart-pie.png) | 円グラフ |
      | ![](../../assets/magento-bi-btn-chart-area.png) | 領域 |
      | ![](../../assets/magento-bi-btn-chart-funnel.png) | ファネル |

      {style="table-layout:auto"}




1. レポートに `title`、 `Untitled Report` ページ上部のテキストに説明的なタイトルが付きます。

1. 右上隅で、 **[!UICONTROL Save]** 次の操作を実行します。

   * の場合 `Type`、デフォルト設定を受け入れます。 `Chart`.

   * を選択します。 `Dashboard` ここで、レポートを使用できます。

   * クリック **[!UICONTROL Save to Dashboard]**.

      ![ダッシュボードに保存](../../assets/magento-bi-report-builder-save-to-dashboard.png)

1. グラフをダッシュボードに表示するには、次のいずれかの操作を行います。

   * クリック **[!UICONTROL Go to Dashboard]** 」と入力します。

   * メニューで、「 」を選択します。 `Dashboards` をクリックし、現在のダッシュボードの名前をクリックしてリストを表示します。 次に、レポートが保存されたダッシュボードの名前をクリックします。

      ![ダッシュボードでのレポート](../../assets/magento-bi-report-builder-my-dashboard.png)
