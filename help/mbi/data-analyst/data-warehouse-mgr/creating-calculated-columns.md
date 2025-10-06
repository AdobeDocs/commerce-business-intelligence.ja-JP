---
title: 計算列の作成
description: 様々なソースのデータを統合する方法を説明します。
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# 計算列の作成

データを分析する場合、様々なソースのデータを統合すると役立ちます。 `orders` テーブルのデータと [!DNL Google Analytics] データをリンクして、収益を獲得ソース別にグループ化したい場合 売上高を顧客の性別でグループ化する場合や、顧客属性をトランザクションデータに結合してセグメント化する場合があります。 このトピックでは、その方法について説明します。

開始する前に、Adobe Data Warehouse Manager で作成できる列の種類とその定義および例について [&#x200B; 計算列の種類のガイド &#x200B;](../../data-analyst/data-warehouse-mgr/calc-column-types.md) を確認することをお勧めします。

1. 開始するには、[**[!DNL Manage Data > Data Warehouse]**] をクリックしてください。

1. 列を作成するテーブルをクリックします。 例えば、売上高のセグメント化に `Customer Gender` しい列を作成する場合、`sales_flat_order` テーブルを選択します。

1. テーブルスキームが表示されます。 「**[!UICONTROL Create New Column]**」をクリックします。

1. 列に名前を付けます。 例：`Customer Gender`。

1. 列の定義を選択します。 [&#x200B; 計算列のタイプ &#x200B;](../data-warehouse-mgr/calc-column-types.md) ガイドが役に立ちます。

1. 特定のタイプの列については、列を適切に作成するためにもう少し情報が必要です。

   * `One to Many` （結合）列と `Many to One` （集計）列の場合は、テーブルと列を選択する必要があります。

   * `Same Table calculation` の場合は、ドロップダウンから目的の日付フィールドを選択する必要があります。

`One to Many` （結合）または `Many to One` （集計）列を作成している場合は、2 つのテーブルを接続する経路を選択する必要があります。 この手順では、既存のパスを使用するか、新しいパスを作成します。

>[!NOTE]
>
>テーブルは、正しく Many または One と定義してください。

* 必要に応じて、新しい列に [&#x200B; フィルター &#x200B;](../../data-user/reports/ess-manage-data-filters.md) を適用できます。

* 終了したら、「**[!UICONTROL Save]**」をクリックします。

現在のテーブルに、新しい列が `Pending` しいステータスで表示されます。 次回の更新が完了すると、列を指標およびレポートで使用できるようになります。

## 便利な参照マップ {#map}

計算列を作成するときにすべての入力が何であるかを思い出せない場合は、以下を作成するときにこの参照マップを手元に置いておいてください。

![Data Warehouse Manager での計算列設定の例 &#x200B;](../../assets/Calculated_Columns_Example.png)

## 関連ドキュメント

* [集計列の種類](../data-warehouse-mgr/calc-column-types.md)
* [高度な計算列のタイプ](../data-warehouse-mgr/adv-calc-columns.md)
* [注文お  [!DNL Google ECommerce]  び顧客データを使用したディメンションの作成](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
