---
title: 計算列の作成
description: 様々なソースのデータを統合する方法を説明します。
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# 計算列の作成

データを分析する場合、様々なソースのデータを統合すると役立ちます。 のデータをリンクし、収益を獲得ソース別にグループ化したい場合 `orders` テーブルと [!DNL Google Analytics] データ？ 売上高を顧客の性別でグループ化する場合や、顧客属性をトランザクションデータに結合してセグメント化する場合があります。 このトピックでは、その方法について説明します。

始める前に、Adobeでは以下を確認することをお勧めします [計算列のタイプに関するガイド](../../data-analyst/data-warehouse-mgr/calc-column-types.md) Data Warehouseマネージャで作成できる列のタイプ、その定義および例については、を参照してください。

1. 開始するには、をクリックします **[!DNL Manage Data > Data Warehouse]**.

1. 列を作成するテーブルをクリックします。 例えば、 `Customer Gender` 収益のセグメント化の列では、次を選択します `sales_flat_order` テーブル。

1. テーブルスキームが表示されます。 クリック **[!UICONTROL Create New Column]**.

1. 列に名前を付けます。 例： `Customer Gender`.

1. 列の定義を選択します。 ここで、 [計算列のタイプに関するガイド](../data-warehouse-mgr/calc-column-types.md) 役に立ちます。

1. 特定のタイプの列については、列を適切に作成するためにもう少し情報が必要です。

   * の場合 `One to Many` （結合）と `Many to One` （集計）列。テーブルと列を選択する必要があります。

   * の場合 `Same Table calculation`ただし、ドロップダウンから目的の日付フィールドを選択する必要があります。

を作成する場合 `One to Many` （結合）または `Many to One` （集計）列は、2 つのテーブルを接続する経路を選択する必要があります。 この手順では、既存のパスを使用するか、新しいパスを作成します。

>[!NOTE]
>
>テーブルは、正しく Many または One と定義してください。

* 必要に応じて、以下を適用できます。 [フィルター](../../data-user/reports/ess-manage-data-filters.md) を新しい列に追加します。

* 終了したら、 **[!UICONTROL Save]**.

新しい列が現在のテーブルに表示され、 `Pending` ステータス。 次回の更新が完了すると、列を指標およびレポートで使用できるようになります。

## 便利な参照マップ {#map}

計算列を作成するときにすべての入力が何であるかを思い出せない場合は、以下を作成するときにこの参照マップを手元に置いておいてください。

![](../../assets/Calculated_Columns_Example.png)

## 関連ドキュメント

* [集計列の種類](../data-warehouse-mgr/calc-column-types.md)
* [高度な計算列のタイプ](../data-warehouse-mgr/adv-calc-columns.md)
* [ビルド [!DNL Google ECommerce] 注文および顧客データを含むディメンション](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
