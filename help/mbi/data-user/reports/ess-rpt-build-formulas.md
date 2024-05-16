---
title: 数式
description: 数式の使用方法を説明します。
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# 数式

数式は、複数の指標と数学的ロジックを組み合わせて、質問に回答します。 例えば、ホリデーシーズンの製品あたりの売上高のうち、新規顧客によって生み出されたものはどれくらいですか。

![ダッシュボードでの休日販売](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 手順 1：基本レポートの作成

1. メニューで、を選択します `Report Builder`.

1. クリック **[!UICONTROL Add Metric]** レポートの最初の指標を選択します。

   この例の場合、 `Revenue by products ordered` 指標が使用されます。

1. クリック **[!UICONTROL Add Metric]** もう一度、レポートの 2 番目の指標を選択します。

   この例の場合、 `New Customers` 指標が使用されます。

1. サイドバーで、をクリックします **[!UICONTROL Details]** 各指標に関する情報を表示します。

   ![注文済製品別の売上高](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. サイドバーで、各指標の名前をクリックして、設定ページを新しいブラウザータブで開きます。 下にスクロールして、指標クエリ、フィルター、ディメンションなど、指標の各コンポーネントを表示します。

   ![指標設定](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. レポートに戻るには、[ 前のブラウザ ] タブをクリックします。

1. グラフで、各線の上にいくつかのデータポイントを置くと、各指標に関連付けられている金額が表示されます。

## 手順 2：数式を追加

1. サイドバーの上部にある「」をクリックします **[!UICONTROL Add Formula]**.

   式ボックスに、使用可能な入力として指標が表示されます `A` および `B`、および数式を入力できる入力ボックスが含まれます。

   次の手順を実行します。

   * が含まれる `Enter your Formula` 入力ボックス、入力 `A/B`.

     これにより、売上高が製品の注文数で、新規顧客数で除算されます。

   * を設定 `Select format` 対象： `123Number`.

   * サイドバーで、 `Untitled` 式の名前を指定します。

   ![数式の設定](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. 完了したら、 **[!UICONTROL Apply]**.

   レポートに、式の新しい行が追加されました。 `New Customer Revenue`サイドバーには、新規顧客が生み出した売上高の合計金額が表示されます。

   ![式を含むレポート](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## 手順 3：日付範囲の追加

1. クリック **[!UICONTROL Date Range]** 右上隅

1. 日 `Fixed Date Range` タブで、次の操作を実行します。

   * カレンダーで、日付範囲を選択します。

     この例では、ホリデーシーズンは次のとおりです `November 1` から `December 31`.

   * 次の下 `Select Time Interval`、を選択 `Day`.

     ![固定日付範囲](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * 完了したら、 **[!UICONTROL Apply]**.

   レポートは現在、ホリデーシーズンに限定され、各日のデータポイントが含まれます。

   ![固定日付範囲](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## 手順 4：レポートを保存する

この手順では、レポートをグラフおよびテーブルとして保存します。

1. クリック `Untitled Report` ページの上部に、わかりやすいタイトルを入力します。 この例では、レポートタイトルはです `2017 Holiday Sales`.

   次に、以下の手順を実行します。

   * 右上隅のをクリックします。 **[!UICONTROL Save]**.

   * の場合 `Type`、デフォルトを使用します `Chart` の設定値。

   * を選択します。 `Dashboard` レポートを使用できる場所。

   * クリック **[!UICONTROL Save to Dashboard]**.

1. レポートのタイトルをクリックし、名前を変更します。 この例では、レポートタイトルがに変更されます。 `2017 Holiday Sales Data`.

   次に、以下の手順を実行します。

   * 右上隅のをクリックします。 **[!UICONTROL Save a Copy]**.

   * を設定 `Type` 対象： `Table`.

   * を選択します。 `Dashboard` レポートを使用できる場所。

   * クリック **[!UICONTROL Save a Copy to Dashboard]**.

1. ダッシュボードでレポートを表示するには、次のいずれかの操作を行います。

   * クリック **[!UICONTROL Go to Dashboard]** ページ上部のメッセージ。

   * メニューで、を選択します **[!UICONTROL Dashboards]**. 現在のダッシュボードの名前をクリックしてリストを表示します。 次に、レポートが保存されたダッシュボードの名前をクリックします。
