---
title: 小売カレンダーのレポート
description: ' [!DNL Commerce Intelligence]  アカウント内で4-5-4小売カレンダーを使用するように構造を設定する方法を説明します。'
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
role: Admin, Developer, User
feature: Data Warehouse Manager, Reports, Dashboards
TQID: https://experienceleague.adobe.com/fXws4NU5bBiAnWU5F9B7mNPts3d-e5D41zSUCpJDomE
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 651
ht-degree: 0%

---

# 小売カレンダーのレポート

このトピックでは、[&#x200B; アカウント内で](https://nrf.com/resources/4-5-4-calendar)4-5-4小売カレンダー[!DNL Adobe Commerce Intelligence]を使用するように構造を設定する方法を示します。 ビジュアルレポートビルダーは、非常に柔軟な時間範囲、間隔、独立した設定を提供します。 ただし、これらの設定はすべて、従来の月次カレンダーを使用して機能します。

多くの顧客がカレンダーを変更して小売または会計日を使用するため、次の手順では、データの使用方法と小売の日付を使用したレポートの作成方法を示します。 以下の手順では、4-5-4小売カレンダーを参照していますが、財務カレンダーであれ、カスタム時間枠であれ、チームが使用する特定のカレンダー用に変更することができます。

開始する前に、[&#x200B; ファイルアップローダー](../../data-analyst/importing-data/connecting-data/using-file-uploader.md)を確認し、`.csv` ファイルが延長されていることを確認する必要があります。 これにより、日付がすべての履歴データをカバーし、日付を将来にプッシュできるようになります。

この分析には、[高度な計算列](../data-warehouse-mgr/adv-calc-columns.md)が含まれています。

## はじめに

2014年から2017年の小売カレンダーの4-5-4の[&#x200B; バージョンを](../../assets/454-calendar.csv) ダウンロード `.csv`できます。 このファイルは、内部の小売カレンダーに従って調整し、日付範囲を拡張して過去と現在の時間枠をサポートする必要がある場合があります。 ファイルをダウンロードした後、ファイルアップローダーを使用して、[!DNL Commerce Intelligence] Data Warehouseに小売カレンダーテーブルを作成します。 4-5-4小売カレンダーの変更されていないバージョンを使用している場合は、このテーブルのフィールドの構造とデータタイプが次のように一致していることを確認します。

| 列名 | 列データタイプ | プライマリキー |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` （最大255文字） | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## 作成する列

* **sales\_order** テーブル
   * `INPUT` `created\_at` （yyyy-mm-dd 00:00:00）
      * [!UICONTROL Column type]: - `Same table > Calculation`
      * [!UICONTROL Inputs]: - `created\_at`
      * [!UICONTROL Datatype]: - `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **小売カレンダー** ファイル アップロード テーブル
   * **現在の日付**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * &#x200B;
        [!UICONTROL データタイプ]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

        >[!NOTE]
        >
        >上記の`now()`関数はPostgreSQLに固有です。 ほとんどの[!DNL Commerce Intelligence] データウェアハウスはPostgreSQLでホストされていますが、一部のデータウェアハウスはRedshiftでホストされている可能性があります。 上記の計算でエラーが返された場合は、`getdate()`ではなくRedshift関数`now()`を使用する必要がある場合があります。

   * **現在の小売年度** （サポートアナリストが作成する必要があります）
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * &#x200B;
        [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **現在の小売年度に含まれますか？ （はい/いいえ）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * &#x200B;
        [!UICONTROL データタイプ]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **前年度の小売に含まれますか？ （はい/いいえ）**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * &#x200B;
        [!UICONTROL データタイプ]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`

* **sales\_order** テーブル
   * **作成日時（小売り年）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * [!UICONTROL table]を選択：`Retail Calendar`
      * [!UICONTROL column]を選択：`Year Retail`
   * **作成日時（小売り週）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス -
         * [!UICONTROL Many]: sales\_order。\[INPUT\]さんが\_at （yyyy-mm-dd 00:00:00を作成しました
         * [!UICONTROL One]：小売カレンダー。日付小売
      * [!UICONTROL table]を選択：`Retail Calendar`
      * [!UICONTROL column]を選択：`Week Retail`
   * **作成日\_at （小売り月）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * [!UICONTROL table]を選択：`Retail Calendar`
      * [!UICONTROL column]を選択：`Month Number Retail`
   * **前年度の小売に含めますか？ （はい/いいえ）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]：小売`Calendar.Date Retail`
      * [!UICONTROL table]を選択：`Retail Calendar`
      * [!UICONTROL column]を選択：`Include in previous retail year? (Yes/No)`
   * **現在の小売年度に含める場合 （はい/いいえ）**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * パス -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]：小売`Calendar.Date Retail`
      * [!UICONTROL table]を選択：`Retail Calendar`
      * [!UICONTROL column]を選択：`Include in current retail year? (Yes/No)`

## 指標

注：この分析に新しい指標は必要ありません。 ただし、レポートに進む前に、sales\_order テーブルのすべての指標に対して、sales\_order テーブルで作成した新しい列をディメンション [として](../data-warehouse-mgr/manage-data-dimensions-metrics.md)追加してください。

## レポート

* **週次オーダー – 小売カレンダー（前年比）**
   * 指標`A`: `2017`
      * [!UICONTROL Metric]：注文数
      * [!UICONTROL Filter]:
         * 作成日\_at （小売り年） = 2017
   * 指標`B`: `2016`
      * [!UICONTROL Metric]：注文数
      * [!UICONTROL Filter]:
         * 作成日\_at （小売り年） = 2016
   * 指標`C`: `2015`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * &#x200B;
     [!UICONTROL Group by]: `Created\_at` (retail week)
   * &#x200B;
     [!UICONTROL Chart type]: `Line`
      * `multiple Y-axes`をオフにする

* **小売カレンダーの概要（現在の小売カレンダーを月ごとに表示）**
   * 指標`A`: `Revenue`
      * &#x200B;
        [!UICONTROL 指標]: `Revenue`
      * [!UICONTROL Filter]:
         * &#x200B;
           [!UICONTROL Include current retail year?]: `Yes`
   * 指標`B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * &#x200B;
           [!UICONTROL Include current retail year?]: `Yes`
   * 指標`C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * &#x200B;
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * &#x200B;
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * &#x200B;
     [!UICONTROL Chart type]: `Line`

* **小売カレンダーの概要（前年から月）**
   * 指標`A`: `Revenue`
      * &#x200B;
        [!UICONTROL 指標]: `Revenue`
      * [!UICONTROL Filter]:
         * &#x200B;
           [!UICONTROL Include current retail year?]: `Yes`
   * 指標`B`: `Orders`
      * [!UICONTROL Metric]：注文数
      * [!UICONTROL Filter]:
         * &#x200B;
           [!UICONTROL Include current retail year?]: `Yes`
   * 指標`C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * &#x200B;
           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL Interval]: `None`
   * &#x200B;
     [!UICONTROL Group by]: `Created\_at` (retail month)
   * &#x200B;
     [!UICONTROL Chart type]: `Line`

## 次のステップ

上記では、小売カレンダーを`sales\_order` テーブル上に構築された任意の指標（`Revenue`や`Orders`など）と互換性を持つように設定する方法について説明します。 また、この機能を拡張して、任意のテーブル上に構築された指標の小売カレンダーをサポートすることもできます。 唯一の要件は、このテーブルに、小売カレンダーテーブルへの結合に使用できる有効な日時フィールドがあることです。

例えば、4 ～ 5 ～ 4個の小売カレンダーで顧客レベルの指標を表示するには、前述の`Same Table`と同様に、`customer\_entity` テーブルに`\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`計算を作成します。 次に、この列を使用して、`One to Many` テーブルを`Created_at (retail year)` テーブルに結合することで、`Include in previous retail year? (Yes/No)`結合\_COLUMN計算（`customer\_entity`など）と`Retail Calendar`を再現できます。

新しいレポートを作成する前に、[すべての新しい列を指標](../data-warehouse-mgr/manage-data-dimensions-metrics.md)にディメンションとして追加することを忘れないでください。
