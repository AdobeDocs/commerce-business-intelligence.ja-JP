---
title: 数式
description: 数式の使用方法を説明します。
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# 数式

数式は、複数の指標と数学ロジックを組み合わせて、質問に答えます。 例えば、新規顧客が生み出したホリデーシーズンの製品あたりの売上高はどれくらいか。

![ダッシュボードでのホリデーセールス](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 手順 1：基本レポートの作成

1. メニューで、「 」を選択します。 `Report Builder`.

1. クリック **[!UICONTROL Add Metric]** レポートの最初の指標を選択します。

   この例では、 `Revenue by products ordered` という指標が使用されます。

1. クリック **[!UICONTROL Add Metric]** 再度選択し、レポートの 2 番目の指標を選択します。

   この例では、 `New Customers` という指標が使用されます。

1. サイドバーで、 **[!UICONTROL Details]** をクリックして、各指標に関する情報を表示します。

   ![注文製品別の売上高](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. サイドバーで、各指標の名前をクリックし、設定ページを新しいブラウザータブで開きます。 下にスクロールして、指標クエリ、フィルター、ディメンションを含む、指標の各コンポーネントを確認します。

   ![指標設定](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. レポートに戻るには、前のブラウザータブをクリックします。

1. グラフで、各行のいくつかのデータポイントにマウスポインターを置くと、各指標に関連付けられている金額が表示されます。

## 手順 2：数式を追加する

1. サイドバーの上部で、 **[!UICONTROL Add Formula]**.

   数式ボックスには、指標が使用可能な入力として表示されます `A` および `B`には、数式を入力できる入力ボックスが含まれます。

   次の操作を実行します。

   * Adobe Analytics の `Enter your Formula` 入力ボックスに、 `A/B`.

     これにより、売上高が新規顧客数で並べ替えられた製品数で割られます。

   * 設定 `Select format` から `123Number`.

   * サイドバーで、 `Untitled` 数式の名前を持つ。

   ![数式設定](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. 完了したら、「 **[!UICONTROL Apply]**.

   これで、レポートに数式の新しい行が追加されました。 `New Customer Revenue`サイドバーには、新規顧客が生み出した売上高の合計が表示されます。

   ![数式でレポート](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## 手順 3：日付範囲の追加

1. クリック **[!UICONTROL Date Range]** をクリックします。

1. 次の日： `Fixed Date Range` 「 」タブで、以下の操作を実行します。

   * カレンダーで、日付範囲を選択します。

     この例では、ホリデーシーズンは `November 1` 経由 `December 31`.

   * の下 `Select Time Interval`を選択します。 `Day`.

     ![固定日付範囲](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * 完了したら、「 **[!UICONTROL Apply]**.

   レポートがホリデーシーズンに限定され、1 日のデータポイントが表示されるようになりました。

   ![固定日付範囲](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## 手順 4：レポートの保存

この手順では、レポートをグラフとして、またテーブルとして保存します。

1. クリック `Untitled Report` をクリックし、説明的なタイトルを入力します。 この例では、レポートタイトルは `2017 Holiday Sales`.

   次に、以下の手順を実行します。

   * 右上隅で、 **[!UICONTROL Save]**.

   * の場合 `Type`、デフォルトを受け入れる `Chart` 設定。

   * を選択します。 `Dashboard` ここで、レポートを使用できます。

   * クリック **[!UICONTROL Save to Dashboard]**.

1. レポートのタイトルをクリックし、名前を変更します。 この例では、レポートのタイトルは `2017 Holiday Sales Data`.

   次に、以下の手順を実行します。

   * 右上隅で、 **[!UICONTROL Save a Copy]**.

   * 設定 `Type` から `Table`.

   * を選択します。 `Dashboard` ここで、レポートを使用できます。

   * クリック **[!UICONTROL Save a Copy to Dashboard]**.

1. ダッシュボードにレポートを表示するには、次のいずれかの操作を行います。

   * クリック **[!UICONTROL Go to Dashboard]** 」と入力します。

   * メニューで、「 」を選択します。 **[!UICONTROL Dashboards]**. 現在のダッシュボードの名前をクリックして、リストを表示します。 次に、レポートが保存されたダッシュボードの名前をクリックします。
