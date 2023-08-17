---
title: 予想されるGoogle Analyticsウェアストアドデータ
description: 倉庫内のデータを使用してGoogle Analyticsとやり取りする方法を学びます。
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 0%

---

# 期待値 [!DNL Google Analytics Warehoused] データ

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>一部の情報は、次の場所であなたの友人から許可を得て使用されました： [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] の統合 [!DNL Commerce Intelligence] は [!DNL Google Analytics] [コアレポート API](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>予期しない結果や無意味な結果を避けるには、使用するディメンションが [1 つ以上の指標と互換性がある](https://ga-dev-tools.google/dimensions-metrics-explorer/) を `Report Builder`.

という名前の単一のテーブル `report`  — がData Warehouseに作成されました。

このテーブルのスキーマは、設定プロセス中に選択した指標とDimension、および他の 2 つの列で構成されます。 `start-date` および `end-date`.

例えば、セットアップ中に次の指標とDimensionを選択したとします。

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

テーブルは次の例のようになります。

| **列名** | **説明** |
|-----|-----|
| `\_id` | この列は `primary key`. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] 一意の ID。 この列は次のユーザーによって作成されます： [!DNL Commerce Intelligence]. |
| `\_updated\_at` | この列には、データ行が最後に更新された日時が含まれます。 この列は次のユーザーによって作成されます： [!DNL Commerce Intelligence]. |
| `start-date` | 行の目的の日を示す ID。 |
| `end-date` | 行の目的の日を示す ID。 |
| `month` | 選択されたディメンション：セッションの月（01 ～ 12 の 2 桁の整数）。 |
| `users` | 選択された指標：リクエストされた期間のユーザーの合計数。 |

{style="table-layout:auto"}

## ～の違いは何か [!DNL Google Analytics Warehoused] および [!DNL Live Integration]

主な差別化要因は、1 つの統合が保存されることです ([!DNL Google Analytics Warehoused])、それ以外は ([!DNL Google Analytics Live]) をクリックします。 の場合 [!DNL Google Analytics Warehoused]を使用すると、 [!DNL Google Analytics] データを取得し、 [!DNL Google Analytics] と、洞察に富んだレポートを作成するその他のデータソース。

見る [!DNL Google Analytics] 広告キャンペーンを参照してください。 Q4 に異なる名前の広告キャンペーンが複数あるとします。 キャンペーンは、特定のマーケティングイニシアチブの結果でした。 倉庫に格納されたデータを使用して、問題のキャンペーン名を検索し、次の Q4 イニシアチブ名を返す列を作成できます。 `Operation Dumbo`.

組み合わせの側面により、 [!DNL Google Analytics] 分析を行うために他のデータに結合するデータ。 例えば、次のようにします。 `Total Time On Site By Ad Campaign` からのデータ [!DNL Google Analytics] そしてそれを仲間に入れて `Total Spent Per Campaign` からのデータ [!DNL Facebook Ads] エンゲージメントに費やされたコストの全体像を把握するために。

を使用 [!DNL Google Analytics Live] 一方で、 [!DNL Google Analytics] グラフは、 [!DNL Commerce Intelligence] Data Warehouse。

## 関連：

* [接続中 [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
