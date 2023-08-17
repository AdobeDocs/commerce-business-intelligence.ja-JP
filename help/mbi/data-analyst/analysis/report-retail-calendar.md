---
title: 小売カレンダーのレポート
description: 内で4-5-4小売業用カレンダーを使用する構造を設定する方法を説明します。 [!DNL Commerce Intelligence] アカウント。
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# 小売カレンダーのレポート

このトピックでは、 [4-5-4小売業用カレンダー](https://nrf.com/resources/4-5-4-calendar) の [!DNL Adobe Commerce Intelligence] アカウント。 Visual Report Builder は、非常に柔軟な時間範囲、間隔、独立した設定を提供します。 ただし、これらの設定はすべて、従来の月次カレンダーを使用して動作します。

多くのお客様がカレンダーを変更して小売または会計日を使用するので、次の手順では、データを使用し、小売日を使用してレポートを作成する方法を示します。 以下の手順は4-5-4小売業用カレンダーを参照していますが、財務用かカスタムの期間かに関わらず、チームが使用する特定のカレンダーに対して変更できます。

使い始める前に、 [ファイルアップローダ](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) そして、長くしてあることを確認します。 `.csv` ファイル。 これにより、日付はすべての履歴データをカバーし、日付を将来の日付にプッシュします。

この分析に含まれる内容 [高度な計算列](../data-warehouse-mgr/adv-calc-columns.md).

## はじめに

以下が可能です。 [ダウンロード](../../assets/454-calendar.csv) a `.csv` 2014 年～2017 年の4-5-4小売年度用カレンダーのバージョン。 内部の小売業用カレンダーに従ってこのファイルを調整し、履歴と現在の期間に対応するように日付範囲を拡張する必要が生じる場合があります。 ファイルをダウンロードした後、ファイルアップローダを使用して、 [!DNL Commerce Intelligence] Data Warehouse。 変更されていないバージョンの4-5-4小売業用カレンダーを使用している場合は、このテーブルのフィールドの構造とデータ型が次のものと一致していることを確認してください。

| 列名 | 列のデータタイプ | プライマリキー |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` （最大 255 文字） | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## 作成する列

* **sales\_order** 表
   * `INPUT` `created\_at` (yyyy-mm-dd 00):00:00)
      * [!UICONTROL Column type]: – `Same table > Calculation`
      * [!UICONTROL Inputs]: – `created\_at`
      * [!UICONTROL Datatype]: – `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **小売カレンダー** ファイルアップロードテーブル
   * **現在の日付**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
        [!UICONTROL データ型]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

        >[!NOTE]
        >
        >The `now()` 上記の関数は、PostgreSQL に固有です。 ただし、 [!DNL Commerce Intelligence] データウェアハウスは PostgreSQL でホストされ、一部は Redshift でホストされる場合があります。 上記の計算でエラーが返された場合は、 Redshift 関数を使用する必要がある場合があります `getdate()` の代わりに `now()`.

   * **現在の小売年** （サポートアナリストが作成する必要があります）
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
        [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **現在の小売年度に含まれますか？ （はい/いいえ）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL データ型]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **前の小売年度に含まれますか？ （はい/いいえ）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL データ型]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`

* **sales\_order** 表
   * **作成日\_at （小売年度）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス —
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * を選択します。 [!UICONTROL table]: `Retail Calendar`
      * を選択します。 [!UICONTROL column]: `Year Retail`
   * **作成日時（小売週）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス —
         * [!UICONTROL Many]: sales\_order\[INPUT\] created\_at (yyyy-mm-dd 00):00:00
         * [!UICONTROL One]：小売業用 Calendar.Date Retail
      * を選択します。 [!UICONTROL table]: `Retail Calendar`
      * を選択します。 [!UICONTROL column]: `Week Retail`
   * **作成日\_at（小売月）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * を選択します。 [!UICONTROL table]: `Retail Calendar`
      * を選択します。 [!UICONTROL column]: `Month Number Retail`
   * **前の小売年度に含めますか？ （はい/いいえ）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス —
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]：小売 `Calendar.Date Retail`
      * を選択します。 [!UICONTROL table]: `Retail Calendar`
      * を選択します。 [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **現在の小売年度に含めますか？ （はい/いいえ）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス —
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]：小売 `Calendar.Date Retail`
      * を選択します。 [!UICONTROL table]: `Retail Calendar`
      * を選択します。 [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## 指標

注意：この分析に新しい指標は必要ありません。 ただし、必ず [sales\_order テーブルで作成した新しい列をディメンションとして追加します。](../data-warehouse-mgr/manage-data-dimensions-metrics.md) を参照してください。

## レポート

* **週別注文件数 — 小売カレンダー (YoY)**
   * 指標 `A`: `2017`
      * [!UICONTROL Metric]：注文数
      * [!UICONTROL Filter]:
         * 作成日（小売年度） = 2017
   * 指標 `B`: `2016`
      * [!UICONTROL Metric]：注文数
      * [!UICONTROL Filter]:
         * 作成日（小売年度） = 2016
   * 指標 `C`: `2015`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail week)
   * 
     [!UICONTROL Chart type]: `Line`
      * オフにする `multiple Y-axes`

* **小売カレンダーの概要（現在の小売年度 — 月別）**
   * 指標 `A`: `Revenue`
      * 
        [!UICONTROL 指標]: `Revenue`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * 指標 `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * 指標 `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * 
     [!UICONTROL Chart type]: `Line`

* **小売カレンダーの概要（前の小売年度 — 月別）**
   * 指標 `A`: `Revenue`
      * 
        [!UICONTROL 指標]: `Revenue`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * 指標 `B`: `Orders`
      * [!UICONTROL Metric]：注文数
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * 指標 `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL Interval]: `None`
   * 
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * 
     [!UICONTROL Chart type]: `Line`

## 次の手順

上記では、 `sales\_order` テーブル ( `Revenue` または `Orders`) をクリックします。 また、任意のテーブルに作成された指標の小売カレンダーをサポートするように拡張することもできます。 唯一の要件は、このテーブルに、小売カレンダーテーブルへの結合に使用できる有効な datetime フィールドがあることです。

例えば、4-5-4小売業用カレンダーに顧客レベルの指標を表示するには、 `Same Table` 計算 `customer\_entity` テーブル、次に類似 `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` 上記の説明。 その後、この列を使用して `One to Many` JOINED\_COLUMN の計算 ( `Created_at (retail year)`) および `Include in previous retail year? (Yes/No)` ～に加わることで `customer\_entity` テーブルから `Retail Calendar` 表。

忘れずに [すべての新しい列を指標のディメンションとして追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に。
