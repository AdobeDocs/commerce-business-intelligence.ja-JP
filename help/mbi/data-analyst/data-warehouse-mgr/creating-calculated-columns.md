---
title: 分かりやすい視覚表現の作成
description: さまざまなソースからデータを統合する方法をご確認ください。
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/dGzhox6Xjuvc3goSxkF2W-5yBlkgKgnOJg7YcuD2Q0s
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 345
ht-degree: 0%

---

# 計算列の作成

データを分析する際には、さまざまなソースから収集したデータを統合することが重要です。 `orders` テーブルと[!DNL Google Analytics] データのデータをリンクして、獲得ソースごとに収益をグループ化しますか？ 顧客の性別ごとに収益をグループ化したり、セグメント化のために顧客の属性をトランザクションデータに結合したりしたいとします。 ここでは、その方法を詳しく解説します。

開始する前に、Adobeでは、Data Warehouse Managerで作成できる列の種類とその定義と例について、[計算列タイプ ガイド &#x200B;](../../data-analyst/data-warehouse-mgr/calc-column-types.md)を確認することをお勧めします。

1. 開始するには、**[!DNL Manage Data > Data Warehouse]**&#x200B;をクリックしてください。

1. 列を作成するテーブルをクリックします。 例えば、収益セグメンテーション用に`Customer Gender`列を作成する場合は、`sales_flat_order` テーブルを選択します。

1. 表書式が表示されます。 **[!UICONTROL Create New Column]**&#x200B;をクリックします。

1. 列に名前を付けます。 例：`Customer Gender`。

1. 列の定義を選択します。 ここでは、[計算列タイプ ガイド &#x200B;](../data-warehouse-mgr/calc-column-types.md)が役立ちます。

1. 特定のタイプの列の場合、列を適切に作成するために、もう少し詳しい情報が必要です。

   * `One to Many` （結合）列と`Many to One` （集計）列の場合は、テーブルと列を選択する必要があります。

   * `Same Table calculation`の場合、ドロップダウンから目的の日付フィールドを選択する必要があります。

`One to Many` （結合）または`Many to One` （集計）列を作成する場合は、2つのテーブルを接続するパスを選択する必要があります。 この手順では、既存のパスを使用するか、パスを作成できます。

>[!NOTE]
>
>テーブルを正しく定義することを忘れないでください。

* 必要に応じて、新しい列に[&#x200B; フィルター](../../data-user/reports/ess-manage-data-filters.md)を適用できます。

* 完了したら、**[!UICONTROL Save]**&#x200B;をクリックします。

新しい列は、現在のテーブルに`Pending` ステータスで表示されます。 次の更新が完了すると、列は指標とレポートで使用できるようになります。

## 便利な参照マップ {#map}

計算列を作成する際にすべての入力が何であるかを思い出すのに問題がある場合は、構築する際にこの参照マップを便利に保つようにしてください。

![Data Warehouse Managerの計算列設定の例](../../assets/Calculated_Columns_Example.png)

## 関連ドキュメント

* [計算された列タイプ](../data-warehouse-mgr/calc-column-types.md)
* [高度な計算列タイプ](../data-warehouse-mgr/adv-calc-columns.md)
* [注文データと顧客データを含む [!DNL Google ECommerce]  ディメンションの作成](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
