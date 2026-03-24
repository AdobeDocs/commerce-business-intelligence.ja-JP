---
title: 数式
description: 数式の使用方法を説明します。
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/FYpOkbam6YFAKQtrLQZsZefke8baiqpK9pwsRI1z2n0
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 472
ht-degree: 0%

---

# 数式

数式は、複数の指標と数学的論理を組み合わせて質問に回答します。 例えば、ホリデーシーズン中に、新顧客によって生み出された商品1個当たりの売上は、どの程度でしょうか？

ダッシュボードでの![ ホリデーセールス ](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## 手順1：基本レポートの作成

1. メニューで、`Report Builder`を選択します。

1. **[!UICONTROL Add Metric]**&#x200B;をクリックし、レポートの最初の指標を選択します。

   この例では、`Revenue by products ordered`指標が使用されています。

1. もう一度&#x200B;**[!UICONTROL Add Metric]**&#x200B;をクリックし、レポートの2番目の指標を選択します。

   この例では、`New Customers`指標が使用されています。

1. サイドバーで、**[!UICONTROL Details]**&#x200B;をクリックして、各指標に関する情報を表示します。

   ![注文済み製品による収益](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. サイドバーで各指標の名前をクリックし、新しいブラウザータブで設定ページを開きます。 下にスクロールして、指標クエリ、フィルター、ディメンションなど、指標の各コンポーネントを表示します。

   ![指標の設定](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. レポートに戻るには、以前のブラウザータブをクリックします。

1. グラフで、各行のいくつかのデータポイントにカーソルを合わせると、各指標に関連付けられている金額が表示されます。

## 手順2：数式の追加

1. サイドバーの上部にある「**[!UICONTROL Add Formula]**」をクリックします。

   数式ボックスには、指標が使用可能な入力`A`および`B`として表示され、数式を入力できる入力ボックスが含まれています。

   次の操作を行います。

   * `Enter your Formula`入力ボックスに、`A/B`と入力します。

     これにより、売上を新規顧客数の多い商品で割ります。

   * `Select format`を`123Number`に設定します。

   * サイドバーで、`Untitled`を数式の名前に置き換えます。

   ![数式設定](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. 完了したら、**[!UICONTROL Apply]**&#x200B;をクリックします。

   レポートに数式`New Customer Revenue`の新しい行が追加され、サイドバーに新規顧客によって生成された収益の合計金額が表示されます。

   ![数式](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)を使用したレポート

## 手順3：日付範囲の追加

1. 右上隅の&#x200B;**[!UICONTROL Date Range]**&#x200B;をクリックします。

1. 「`Fixed Date Range`」タブで、次の操作を行います。

   * カレンダーで、日付範囲を選択します。

     この例では、ホリデーシーズンは`November 1`から`December 31`までです。

   * `Select Time Interval`で、`Day`を選択します。

     ![固定日付範囲](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * 完了したら、**[!UICONTROL Apply]**&#x200B;をクリックします。

   レポートは現在、ホリデーシーズンに限定され、毎日のデータポイントが表示されます。

   ![固定日付範囲](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## 手順4：レポートの保存

この手順では、レポートをグラフとしてもテーブルとしても保存します。

1. ページの上部にある「`Untitled Report`」をクリックし、わかりやすいタイトルを入力します。 この例では、レポートタイトルは`2017 Holiday Sales`です。

   次に、次の操作を行います。

   * 右上隅の「**[!UICONTROL Save]**」をクリックします。

   * `Type`の場合は、デフォルトの`Chart`設定を受け入れます。

   * レポートを利用できる`Dashboard`を選択します。

   * **[!UICONTROL Save to Dashboard]**&#x200B;をクリックします。

1. レポートタイトルをクリックし、名前を変更します。 この例では、レポートタイトルが`2017 Holiday Sales Data`に変更されています。

   次に、次の操作を行います。

   * 右上隅の「**[!UICONTROL Save a Copy]**」をクリックします。

   * `Type`を`Table`に設定します。

   * レポートを利用できる`Dashboard`を選択します。

   * **[!UICONTROL Save a Copy to Dashboard]**&#x200B;をクリックします。

1. ダッシュボードにレポートを表示するには、次のいずれかの操作を行います。

   * ページ上部のメッセージで「**[!UICONTROL Go to Dashboard]**」をクリックします。

   * メニューで、**[!UICONTROL Dashboards]**&#x200B;を選択します。 現在のダッシュボードの名前をクリックして、リストを表示します。 次に、レポートが保存されたダッシュボードの名前をクリックします。
