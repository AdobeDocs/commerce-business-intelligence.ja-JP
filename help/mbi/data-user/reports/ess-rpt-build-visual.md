---
title: ビジュアルReport Builder
description: Visual Report Builderの使用方法を説明します。
exl-id: 1101f43d-e014-4df2-be21-12d90a9d8a56
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 0%

---

# [!DNL Visual Report Builder]

[!DNL Visual Report Builder] を使用すると、事前定義済みの指標に基づいてクイックレポートを簡単に作成できます。 各指標には、レポートのデータセットを定義するクエリが含まれます。

次の例では、単純なレポートを作成し、追加のディメンションでデータをグループ化し、日時の間隔を設定し、グラフの種類を変更して、レポートをダッシュボードに保存する方法を示します。

## シンプルなレポートを作成するには：

1. [!DNL Commerce Intelligence] メニューで、「**[!UICONTROL Report Builder]**」をクリックします。

1. [[!UICONTROL Visual Report Builder]] で [**[!UICONTROL Create Report]**] をクリックし、次の操作を行います。

   * 「**[!UICONTROL Add Metric]**」をクリックします。

     使用可能な指標は、アルファベット順またはテーブル順に表示されます。

     ![&#x200B; ビジュアルReport Builder](../../assets/magento-bi-visual-report-builder-add-metric.png)

   * レポートに使用するデータセットを表す [&#x200B; 指標 &#x200B;](../../data-user/reports/ess-manage-data-metrics.md) を選択します。

     この例で使用される `New Customers` 指標は、すべての顧客をカウントし、顧客がアカウントに登録した日付でリストを並べ替えます。 最初のレポートには、単純な折れ線グラフと、データのテーブルが続きます。

     左側の概要には、現在の指標の名前が表示され、その後、指標で指定された列データに対する計算の結果が表示されます。 この例では、概要に合計顧客数が表示されます。

     ![&#x200B; ビジュアルReport Builder](../../assets/magento-bi-report-builder-untitled.png)

1. グラフでは、線上の各データ ポイントにポインタを合わせます。 各データポイントには、その月に新規登録した顧客の合計数が表示されます。

1. データのグループ化、日付範囲の変更、グラフのタイプの変更を行うには、次の手順に従います。

   **`Group By`**

   `Group By` コントロールを使用すると、グループまたはセグメントごとに複数の寸法を追加できます。 ディメンションは、データのグループ化に使用できるテーブルの列です。

   * オプションのリストから、使用可能なディメンションの 1 つ `Group By` 選択します。

     この例では、システムは顧客が最初の注文時に使用した 5 つのクーポンコードを見つけました。

     ![&#x200B; グループ化 &#x200B;](../../assets/magento-bi-report-builder-group-by-dimensions.png)

     `Group By` の詳細には、顧客が使用する各クーポンが一覧表示されます。 最初の注文に使用したクーポンには、チェックボックスが付きます。 グラフには、最初の注文で使用された各クーポンを表す複数の色付きの線が追加されました。 凡例は、データの各行に対応するように色分けされます。

   * **[!UICONTROL Apply]** をクリックして、Group By の詳細を閉じます。

     ![&#x200B; 複数ディメンション &#x200B;](../../assets/magento-bi-report-builder-group-by-dimension-detail.png)

   * 各行にいくつかのデータポイントを合わせると、最初の注文時にそのクーポンを使用した 1 か月の顧客数が表示されます。

   * データのテーブルに追加ディメンションが追加され、各月の列とクーポンコードごとの行が含まれるようになりました。

     ![&#x200B; テーブルデータでグループ化 &#x200B;](../../assets/magento-bi-report-builder-group-by-table-data.png)

   * テーブルの右上隅にある転置（![&#x200B; 転置アイコン &#x200B;](../../assets/magento-bi-btn-transpose.png)）コントロールをクリックして、データの方向を変更します。

     データの軸が反転され、テーブルにはクーポンコードごとに列があり、月ごとに行があります。 この向きは、読みやすいかもしれません。

     ![&#x200B; 転置データ &#x200B;](../../assets/magento-bi-report-builder-group-by-table-data-transposed.png)

   **`Date Range`**

   `Date Range` コントロールは、現在の日付範囲と時間間隔の設定を表示し、グラフのすぐ上の右側にあります。

   * `Date Range` コントロールをクリックします。この例では、`All-Time by Month` に設定されています。

     ![&#x200B; 日付範囲 &#x200B;](../../assets/magento-bi-report-builder-date-range.png)

   * 次の変更を行います。

      * 拡大表示するには、日付範囲を `Last Full Quarter` に変更します。
      * 「`Select Time Interval`」で、「`Week`」を選択します。
      * 完了したら、「**[!UICONTROL Save]**」をクリックします。

     レポートには、前四半期のデータのみが週別に含まれるようになりました。

     ![&#x200B; 前四半期の週別レポート &#x200B;](../../assets/magento-bi-report-builder-date-range-quarter-by-week-chart.png)

   **グラフのタイプ**

   * 右上隅のコントロールをクリックして、データに最適なグラフを見つけます。

     一部のグラフの種類は、多次元データと互換性がありません。

     | | |
     |-----|-----|
     | ![&#x200B; 折れ線グラフアイコン &#x200B;](../../assets/magento-bi-btn-chart-line.png) | 折れ線グラフ |
     | ![&#x200B; 横棒グラフのアイコン &#x200B;](../../assets/magento-bi-btn-chart-horz-bar.png) | 横棒グラフ |
     | ![&#x200B; 積み重ね横棒グラフのアイコン &#x200B;](../../assets/magento-bi-btn-chart-horz-stacked-bar.png) | 横積み重ね棒グラフ |
     | ![&#x200B; 縦棒アイコン &#x200B;](../../assets/magento-bi-btn-chart-vert-bar.png) | 縦棒グラフ |
     | ![&#x200B; 垂直積み重ね棒アイコン &#x200B;](../../assets/magento-bi-btn-chart-vert-stacked-bar.png) | 縦積み横棒グラフ |
     | ![&#x200B; 円グラフアイコン &#x200B;](../../assets/magento-bi-btn-chart-pie.png) | 円グラフ |
     | ![&#x200B; 面グラフ アイコン &#x200B;](../../assets/magento-bi-btn-chart-area.png) | 面グラフ |
     | ![Funnel グラフ アイコン &#x200B;](../../assets/magento-bi-btn-chart-funnel.png) | ファネル |

     {style="table-layout:auto"}

1. レポートに `title` を付けるには、ページ上部の `Untitled Report` のテキストを説明的なタイトルに置き換えます。

1. 右上隅の「**[!UICONTROL Save]**」をクリックして、次の操作を行います。

   * `Type` の場合は、デフォルト設定 `Chart` を使用します。

   * レポートを使用できる `Dashboard` を選択します。

   * 「**[!UICONTROL Save to Dashboard]**」をクリックします。

     ![&#x200B; ダッシュボードに保存 &#x200B;](../../assets/magento-bi-report-builder-save-to-dashboard.png)

1. ダッシュボードにグラフを表示するには、次のいずれかの操作を行います。

   * ページ上部のメッセージで「**[!UICONTROL Go to Dashboard]**」をクリックします。

   * メニューで「`Dashboards`」を選択し、現在のダッシュボードの名前をクリックしてリストを表示します。 次に、レポートが保存されたダッシュボードの名前をクリックします。

     ![&#x200B; ダッシュボードのレポート &#x200B;](../../assets/magento-bi-report-builder-my-dashboard.png)
