---
title: 予期されるGoogle Analyticsのウェアハウスされたデータ
description: Google Analyticsが保管したデータとやり取りする方法を説明します。
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# 予測 [!DNL Google Analytics Warehoused] データ

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>で友人の許可を得て情報を使用しました [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] との統合 [!DNL Commerce Intelligence] はを使用します [!DNL Google Analytics] [コアレポート API](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>予期しない結果や感覚的でない結果を避けるために、使用するディメンションが次のものであることを確認します [1 つ以上の指標と互換性がある](https://ga-dev-tools.google/dimensions-metrics-explorer/) では、を使用します `Report Builder`.

単一のテーブル – と呼ばれます `report`  – がData Warehouse内に作成されます。

このテーブルのスキーマは、設定プロセスで選択した指標およびDimensionと、他の 2 つの列で構成されています。 `start-date` および `end-date`.

例えば、セットアップ時に次の指標とDimensionを選択した場合：

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

テーブルは次の例のようになります。

| **列名** | **説明** |
|-----|-----|
| `\_id` | この列はです `primary key`. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] 一意の ID。 この列の作成者 [!DNL Commerce Intelligence]. |
| `\_updated\_at` | この列には、データ行が最後に更新された時刻が含まれています。 この列の作成者 [!DNL Commerce Intelligence]. |
| `start-date` | 行の日付を示す ID。 |
| `end-date` | 行の日付を示す ID。 |
| `month` | 選択したディメンション : セッションの月。01 ～ 12 の 2 桁の整数。 |
| `users` | 選択した指標：リクエストされた期間のユーザーの合計数。 |

{style="table-layout:auto"}

## の違いは何ですか。 [!DNL Google Analytics Warehoused] および [!DNL Live Integration]

主な差別化要因は、1 つの統合が格納されるということです（[!DNL Google Analytics Warehoused]）、もう 1 つは（[!DNL Google Analytics Live]）に設定します。 の場合 [!DNL Google Analytics Warehoused]を使用すると、の操作が可能です [!DNL Google Analytics] を使用すると、との結合が可能です。 [!DNL Google Analytics] インサイトに満ちたレポートを作成するためのその他のデータソース。

を見る [!DNL Google Analytics] 操作の観点からできることの例として、広告キャンペーンを使用します。 異なる名前の Q4 に複数の広告キャンペーンがあるとします。 キャンペーンは、特定のマーケティング施策の成果でした。 ウェアハウスに格納されたデータを使用すると、問題のキャンペーン名を見つけて、第 4 四半期のイニシアチブ名を返す列を作成できます。 `Operation Dumbo`.

組み合わせ側面では、 [!DNL Google Analytics] 分析を行うために他のデータに結合されるデータ。 例： `Total Time On Site By Ad Campaign` からのデータ [!DNL Google Analytics] そして、それに加わる `Total Spent Per Campaign` からのデータ [!DNL Facebook Ads] エンゲージメントにかかる費用の全体像を把握する

（を使用） [!DNL Google Analytics Live] 一方、の統合では、 [!DNL Google Analytics] グラフは、に保存されていない小さなサイロのようなものです [!DNL Commerce Intelligence] Data Warehouse。

## 関連：

* [接続中 [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
