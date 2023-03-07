---
title: フィルター
description: フィルターの使用方法を説明します。
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# フィルター

1 つ以上のフィルターを追加して、レポートの作成に使用するデータを制限できます。 各フィルターは、関連付けられたテーブルの列、演算子、値を含む式です。 例えば、リピート顧客のみを含めるには、複数の注文をした顧客のみを含むフィルターを作成します。 論理 `AND/OR` 演算子を使用して、レポートにロジックを追加できます。

>[!TIP]
>
>1 つのレポートに設定できるデータポイントは最大 3,500 個です。 データポイントの数を減らすには、フィルターを使用して、レポートの生成に使用するデータの量を減らします。

MBI には、「標準 (OOTB)」を使用したり、必要に応じて変更したりできる、様々なフィルターが含まれています。 作成できるフィルターの数に制限はありません。

## フィルターを追加するには、次の手順に従います。

1. グラフで、各データポイントにカーソルを合わせます。

   このレポートでは、各データポイントにはその月の顧客の合計数が表示されます。

1. 左のパネルで、「フィルター」(![](../../assets/magento-bi-btn-filter.png)) アイコンをクリックします。

   ![フィルターを追加](../../assets/magento-bi-report-builder-filter-add.png)

1. クリック **[!UICONTROL Add Filter]**.

   フィルターはアルファベット順に番号付けされ、最初は `[A]`. フィルターの最初の 2 つの部分はドロップダウンオプションで、3 番目の部分は値です。

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * フィルターの最初の部分をクリックし、式の件名として使用する列を選択します。

      ![フィルタの最初の部分を選択](../../assets/magento-bi-report-builder-filter-part1.png)

   * フィルターの 2 番目の部分をクリックし、演算子を選択します。

      ![演算子を選択](../../assets/magento-bi-report-builder-filter-part2.png)

   * フィルターの 3 番目の部分に、式を完了するために必要な値を入力します。

      ![値を入力](../../assets/magento-bi-report-builder-filter-part3.png)

   * フィルターが完了したら、 **[!UICONTROL Apply]**.

      レポートにリピート客のみが含まれるようになり、レポートに対して取得した顧客レコードの数が 33,000 から 12,600 に減りました。

      ![フィルター済みレポート](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. サイドバーで、パースペクティブ ( ![](../../assets/magento-bi-btn-perspective.png)) アイコンをクリックします。

   ![遠近法](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. 設定のリストで、「 」を選択します。 `Cumulative`. 次に、「 **[!UICONTROL Apply]**.

   ![累積パースペクティブ](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   この `Cumulative` パースペクティブは、月ごとのぼかしやぼかしを表示するのではなく、時間の経過と共に変化を分布します。

1. を入力します。 `Title` をクリックします。 **[!UICONTROL Save]** それは `Chart` をダッシュボードに追加します。

   ![ダッシュボードに保存](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
