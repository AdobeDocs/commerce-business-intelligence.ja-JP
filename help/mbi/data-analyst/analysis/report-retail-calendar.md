---
title: 小売カレンダーのレポート
description: 4-5-4 小売カレンダーを内で使用するための構造を設定する方法を説明します [!DNL Commerce Intelligence] アカウント。
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# 小売カレンダーのレポート

このトピックでは、を使用するための構造の設定方法を示します [4-5-4 小売カレンダー](https://nrf.com/resources/4-5-4-calendar) 内で [!DNL Adobe Commerce Intelligence] アカウント。 Visual Report Builder は、非常に柔軟な時間範囲、間隔および独立した設定を提供します。 ただし、これらの設定はすべて、従来の月別カレンダーで機能します。

多くの顧客は小売日付または会計日付を使用するようにカレンダーを変更するので、次の手順では、小売日付を使用してデータを操作し、レポートを作成する方法を説明します。 以下の手順は 4-5-4 小売カレンダーを参照していますが、財務カレンダーやカスタム時間枠かどうかに関係なく、チームが使用する特定のカレンダーに対してそれらを変更できます。

開始する前に、次を確認する必要があります [ファイルアップローダ](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) また、を伸ばしたことを確認します `.csv` ファイル。 これにより、日付が履歴データのすべてをカバーし、日付が将来に向かうようになります。

この分析に含まれる内容 [高度な計算列](../data-warehouse-mgr/adv-calc-columns.md).

## はじめに

次のことができます [download](../../assets/454-calendar.csv) a `.csv` 2014 年から 2017 年の小売年の小売カレンダーのバージョン 4-5-4。 場合によっては、社内の小売カレンダーに従ってこのファイルを調整し、履歴期間と現在の時間枠をサポートするように日付範囲を拡張する必要があります。 ファイルをダウンロードしたら、ファイルアップローダを使用して、に小売カレンダーテーブルを作成します [!DNL Commerce Intelligence] Data Warehouse。 変更されていないバージョンの 4-5-4 小売カレンダーを使用している場合は、このテーブルのフィールドの構造とデータタイプが次と一致していることを確認してください。

| 列名 | 列データタイプ | プライマリキー |
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

* **sales\_order** テーブル
   * `INPUT` `created\_at` （yyyy-mm-dd 00:00:00）
      * [!UICONTROL Column type]: - `Same table > Calculation`
      * [!UICONTROL Inputs]: - `created\_at`
      * [!UICONTROL Datatype]: - `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **小売カレンダー** ファイルのアップロードテーブル
   * **現在の日付**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
        [!UICONTROL データ型]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

        >[!NOTE]
        >
        >この `now()` 上記の関数は PostgreSQL 固有の関数です。 ただし、ほとんどの [!DNL Commerce Intelligence] データウェアハウスは PostgreSQL でホストされ、一部は Redshift でホストされます。 上記の計算でエラーが返された場合は、Redshift 関数を使用する必要がある可能性があります `getdate()` の代わりに `now()`.

   * **現在の小売年** （サポートアナリストが作成する必要があります）
      * [!UICONTROL Column type]:E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
        [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **現在の小売年に含まれていますか？ （はい/いいえ）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL データ型]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **以前の小売年度に含まれていますか？ （はい/いいえ）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
        [!UICONTROL データ型]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`

* **sales\_order** テーブル
   * **Created\_at （retail year）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * を選択 [!UICONTROL table]: `Retail Calendar`
      * を選択 [!UICONTROL column]: `Year Retail`
   * **Created\_at （retail week）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス -
         * [!UICONTROL Many]:sales\_order.\[INPUT\] created\_at （yyyy-mm-dd 00:00:00
         * [!UICONTROL One]：小売カレンダー。日小売
      * を選択 [!UICONTROL table]: `Retail Calendar`
      * を選択 [!UICONTROL column]: `Week Retail`
   * **Created\_at （retail month）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * を選択 [!UICONTROL table]: `Retail Calendar`
      * を選択 [!UICONTROL column]: `Month Number Retail`
   * **以前の小売年度に含めますか？ （はい/いいえ）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]：小売 `Calendar.Date Retail`
      * を選択 [!UICONTROL table]: `Retail Calendar`
      * を選択 [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **現在の小売年に含めますか？ （はい/いいえ）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]：小売 `Calendar.Date Retail`
      * を選択 [!UICONTROL table]: `Retail Calendar`
      * を選択 [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## 指標

メモ：この分析では、新しい指標は必要ありません。 ただし、以下を行うようにしてください [sales\_order テーブルに作成した新しい列をディメンションとして追加します](../data-warehouse-mgr/manage-data-dimensions-metrics.md) レポートを続行する前に、sales\_order テーブルのすべてのメトリックについて説明します。

## レポート

* **週次注文 – 小売カレンダー（YoY）**
   * 指標 `A`: `2017`
      * [!UICONTROL Metric]：注文数
      * [!UICONTROL Filter]:
         * 作成日\_at （小売年） = 2017
   * 指標 `B`: `2016`
      * [!UICONTROL Metric]：注文数
      * [!UICONTROL Filter]:
         * 作成日\_at （小売年） = 2016
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
      * 無効にする `multiple Y-axes`

* **小売カレンダーの概要（現在の小売年/月）**
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

* **小売カレンダーの概要（以前の小売年/月）**
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

上記では、で作成された任意の指標と互換性を持つように小売カレンダーを設定する方法を説明します `sales\_order` テーブル（など） `Revenue` または `Orders`）に設定します。 これを拡張して、任意のテーブルに作成された指標の小売カレンダーをサポートすることもできます。 唯一の要件は、このテーブルには、小売カレンダーテーブルへの結合に使用できる有効な日時フィールドがあることです。

例えば、4-5-4 小売カレンダーで顧客レベルの指標を表示するには、 `Same Table` での計算 `customer\_entity` テーブル、類似 `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` 前述の通りです。 その後、この列を使用してを再現できます `One to Many` JOINED\_COLUMN 計算（など） `Created_at (retail year)`）および `Include in previous retail year? (Yes/No)` に参加する `customer\_entity` テーブルから `Retail Calendar` テーブル。

忘れないでください [すべての新規列をディメンションとして指標に追加](../data-warehouse-mgr/manage-data-dimensions-metrics.md) 新しいレポートを作成する前に、
