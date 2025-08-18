---
title: Google Analyticsが格納する必要があるデータ
description: Google Analyticsに保管されたデータとのやり取りを説明します。
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# 予期される [!DNL Google Analytics Warehoused] データ

>[!NOTE]
>
>[ 管理者権限 ](../../../administrator/user-management/user-management.md) が必要です。

>[!NOTE]
>
>[[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics) 時に友達から許可を得て情報を使用しました。

[!DNL Google Analytics Warehoused] の統合 [!DNL Commerce Intelligence]、[!DNL Google Analytics] [ コアレポート API](https://developers.google.com/analytics/devguides/reporting/core/v3/) を使用します。

>[!NOTE]
>
>予期しない結果や感覚的でない結果を避けるために、使用するディメンションが [ で使用する ](https://ga-dev-tools.google/dimensions-metrics-explorer/)1 つ以上の指標と互換性がある `Report Builder` ことを確認します。

Data Warehouseに `report` という 1 つのテーブルが作成されます。

このテーブルのスキーマは、設定プロセス中に選択した指標およびディメンションと、他の 2 つの列（`start-date` および `end-date`）で構成されています。

例えば、セットアップ時に次の指標とディメンションを選択した場合：

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

テーブルは次の例のようになります。

| **列名** | **説明** |
|-----|-----|
| `\_id` | この列は `primary key` です。 |
| `\_rjm\_record\_hash` | 一意 [!DNL Commerce Intelligence]ID。 この列は [!DNL Commerce Intelligence] が作成しました。 |
| `\_updated\_at` | この列には、データ行が最後に更新された時刻が含まれています。 この列は [!DNL Commerce Intelligence] が作成しました。 |
| `start-date` | 行の日付を示す ID。 |
| `end-date` | 行の日付を示す ID。 |
| `month` | 選択したディメンション : セッションの月。01 ～ 12 の 2 桁の整数。 |
| `users` | 選択した指標：リクエストされた期間のユーザーの合計数。 |

{style="table-layout:auto"}

## [!DNL Google Analytics Warehoused] と [!DNL Live Integration] の違い

主な違いは、1 つの統合が保存され（[!DNL Google Analytics Warehoused]）、もう 1 つは保存されない（[!DNL Google Analytics Live]）ことです。 [!DNL Google Analytics Warehoused] の場合は、[!DNL Google Analytics] データを操作でき、[!DNL Google Analytics] と他のデータソースを組み合わせて、インサイトに満ちたレポートを作成できます。

操作の観点から実行できる操作の例については、[!DNL Google Analytics] の広告キャンペーンを参照してください。 異なる名前の Q4 に複数の広告キャンペーンがあるとします。 キャンペーンは、特定のマーケティング施策の成果でした。 ウェアハウスに格納されたデータを使用すると、問題のキャンペーン名を見つけて、Q4 イニシアチブ名 `Operation Dumbo` を返す列を作成できます。

組み合わせ側面 [!DNL Google Analytics] 使用すると、分析を行うためにデータを他のデータに結合できます。 例えば、`Total Time On Site By Ad Campaign` のデータ [!DNL Google Analytics] 取り、`Total Spent Per Campaign` の [!DNL Facebook Ads] データと結合して、エンゲージメントにかかる費用の全体像を把握できます。

一方、[!DNL Google Analytics Live] の統合では、すべての [!DNL Google Analytics] グラフは [!DNL Commerce Intelligence] Data Warehouseには保存されない小さなサイロのようになります。

## 関連：

* [接続  [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
