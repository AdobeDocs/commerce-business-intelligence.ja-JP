---
title: フィルター
description: フィルターの使用方法を説明します。
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 0854d644cb72b3fc8b8b31a0bf7e8dca4cc99724
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# フィルター

1 つ以上のフィルターを追加して、レポートの作成に使用するデータを制限できます。 各フィルターは、関連付けられたテーブルの列、演算子、値を含む式です。 例えば、リピート顧客のみを含めるには、複数の注文を行った顧客のみを含めるフィルターを作成します。 複数のフィルターを論理 `AND/OR` 演算子と共に使用して、レポートにロジックを追加できます。

>[!TIP]
>
>レポートには、最大 3,500 個のデータポイントを含めることができます。 データポイントの数を減らすには、フィルターを使用して、レポートの生成に使用するデータの量を減らします。

[!DNL Adobe Commerce Intelligence] には、「標準搭載（OOTB）」を使用したり、必要に応じて変更したりできる、一連のフィルターが含まれています。 作成できるフィルターの数に制限はありません。

## フィルターを追加するには：

1. グラフで、各データポイントにポインタを合わせます。

   このレポートでは、各データポイントはその月の顧客の合計数を示します。

1. 左側のパネルで、フィルター（![](../../assets/magento-bi-btn-filter.png)） アイコンをクリックします。

   ![ フィルターを追加 ](../../assets/magento-bi-report-builder-filter-add.png)

1. 「**[!UICONTROL Add Filter]**」をクリックします。

   フィルターにはアルファベット順に番号が付けられ、最初のフィルターは `[A]` です。 フィルターの最初の 2 つの部分はドロップダウンオプションで、3 番目の部分は値です。

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * フィルターの最初の部分をクリックし、式の件名として使用する列を選択します。

     ![ フィルターの最初の部分を選択 ](../../assets/magento-bi-report-builder-filter-part1.png)

   * フィルターの 2 番目の部分をクリックし、演算子を選択します。

     ![ 演算子の選択 ](../../assets/magento-bi-report-builder-filter-part2.png)

   * フィルターの 3 番目の部分で、式を完成させるために必要な値を入力します。

     ![ 値を入力 ](../../assets/magento-bi-report-builder-filter-part3.png)

   * フィルターが完了したら、「**[!UICONTROL Apply]**」をクリックします。

     レポートにはリピート顧客のみが含まれるようになり、レポート用に取得された顧客レコードの数が 33,000 から 12,600 に減りました。

     ![ フィルター済み報告書 ](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. サイドバーで、遠近法（![ 遠近法アイコン ](../../assets/magento-bi-btn-perspective.png)）アイコンをクリックします。

   ![ 分析観点 ](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. 設定のリストで、「`Cumulative`」を選択します。 次に、「**[!UICONTROL Apply]**」をクリックします。

   ![ 累積的な視点 ](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   `Cumulative` パースペクティブでは、各月のギザギザした上下を表示するのではなく、時間の経過に伴う変化が分配されます。

1. レポートの `Title` を入力し、ダッシュボードの **[!UICONTROL Save]** として `Chart` をクリックします。

   ![ ダッシュボードに保存 ](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
