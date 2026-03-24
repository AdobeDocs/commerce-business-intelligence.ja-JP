---
title: フィルター
description: フィルターの使用方法を説明します。
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/XnfqSloTGv-hfUbUwPpFbWVsvs8DPrYdzMmTdERSr4Q
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 364
ht-degree: 0%

---

# フィルター

1つ以上のフィルターを追加して、レポートの作成に使用するデータを制限できます。 各フィルターは、関連付けられたテーブルの列、演算子、値を含む式です。 例えば、リピート顧客のみを含めるには、複数の注文を行った顧客のみを含むフィルターを作成します。 論理`AND/OR`演算子で複数のフィルターを使用して、レポートにロジックを追加できます。

>[!TIP]
>
>レポートには最大3,500個のデータポイントを含めることができます。 データポイントの数を減らすには、フィルターを使用して、レポートの生成に使用するデータの量を減らします。

[!DNL Adobe Commerce Intelligence]には、「すぐに使える（OOTB）」を使用するか、ニーズに合わせて変更できるフィルターの選択が含まれています。 作成できるフィルターの数に制限はありません。

## フィルターを追加するには：

1. グラフの各データ ポイントにカーソルを合わせます。

   このレポートでは、各データポイントは1か月の合計顧客数を示します。

1. 左側のパネルで、「フィルター（![ フィルターアイコン ](../../assets/magento-bi-btn-filter.png)）」アイコンをクリックします。

   ![ フィルターを追加](../../assets/magento-bi-report-builder-filter-add.png)

1. **[!UICONTROL Add Filter]**&#x200B;をクリックします。

   フィルターにはアルファベット順に番号が付けられ、最初は`[A]`です。 フィルターの最初の2つの部分はドロップダウンオプションで、3番目の部分は値です。

   ![ フィルターの追加オプションを表示するフィルターインターフェイス ](../../assets/magento-bi-report-builder-filter-add-a.png)

   * フィルターの最初の部分をクリックし、式の被写体として使用する列を選択します。

     ![ フィルターの最初の部分を選択](../../assets/magento-bi-report-builder-filter-part1.png)

   * フィルターの2番目の部分をクリックして、演算子を選択します。

     ![演算子を選択](../../assets/magento-bi-report-builder-filter-part2.png)

   * フィルターの3番目の部分で、式を完了するために必要な値を入力します。

     ![値を入力](../../assets/magento-bi-report-builder-filter-part3.png)

   * フィルターが完了したら、**[!UICONTROL Apply]**&#x200B;をクリックします。

     現在、レポートにはリピート顧客のみが含まれており、レポート用に取得された顧客記録の数は33,000件から12,600件に減少しました。

     ![ フィルター済みレポート ](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. サイドバーで、遠近法（![遠近法アイコン ](../../assets/magento-bi-btn-perspective.png)）アイコンをクリックします。

   ![遠近法](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. 設定のリストで、`Cumulative`を選択します。 次に、**[!UICONTROL Apply]**&#x200B;をクリックします。

   ![累積的な視点](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   `Cumulative`の遠近法は、各月のギザギザの上下を示すのではなく、時間の経過に伴う変化を分布させます。

1. レポートの`Title`を入力し、**[!UICONTROL Save]**&#x200B;を`Chart`としてダッシュボードにクリックします。

   ![ ダッシュボードに保存](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
