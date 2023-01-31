---
title: 予想されるGoogle Analyticsウェアストアドデータ
description: 倉庫内のデータを使用してGoogle Analyticsとやり取りする方法を学びます。
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# 予測 [!DNL Google Analytics] 倉庫内データ

>[!NOTE]
>
>必要 [管理者権限](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>友人の許可を得て～で情報を使った [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] 統合 [!DNL MBI] は、 [!DNL Google Analytics] [コアレポート API](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>予期しない結果や無意味な結果を避けるには、使用するディメンションが [指標と互換性がある](https://developers.google.com/analytics/devguides/reporting/core/dimsmets) を `Report Builder`.

という名前の単一のテーブル `report`  — がData Warehouseに作成されます。

このテーブルのスキーマは、設定プロセスで選択した指標とDimension、および他の 2 つの列で構成されます。 `start-date` および `end-date`.

例えば、設定時に次の指標とDimensionを選択した場合：

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

テーブルは次の例のようになります。

| **列名** | **説明** |
|-----|-----|
| `\_id` | この列は `primary key`. |
| `\_rjm\_record\_hash` | [!DNL MBI] 一意の ID。 この列は次のユーザーによって作成されます： [!DNL MBI]. |
| `\_updated\_at` | この列には、データ行が最後に更新された日時が含まれます。 この列は次のユーザーによって作成されます： [!DNL MBI]. |
| `start-date` | 行の対象日を示す ID。 |
| `end-date` | 行の対象日を示す ID。 |
| `month` | 選択したディメンション：セッションの月で、01 ～ 12 の 2 桁の整数。 |
| `users` | 選択した指標：リクエストされた期間のユーザーの合計数。 |

{style=&quot;table-layout:auto&quot;}

## リマインダー：倉庫内Google Analyticsとライブ統合の違い

主な差別化要因は、1 つの統合が保存されることです ([!DNL Google Analytics Warehoused])、それ以外は ([!DNL Google Analytics Live]) をクリックします。 の場合 [!DNL Google Analytics Warehoused]を使用すると、 [!DNL Google Analytics] データを取得し、 [!DNL Google Analytics] と、洞察に富んだレポートを作成するその他のデータソース。

次を見てみましょう。 [!DNL Google Analytics] 広告キャンペーンを参照してください。 Q4 に異なる名前の広告キャンペーンが複数あるとします。 キャンペーンは、特定のマーケティングイニシアチブの結果でした。 倉庫に格納されたデータを使用して、問題のキャンペーン名を検索し、次の Q4 イニシアチブ名を返す新しい列を作成できます。 `Operation Dumbo`.

組み合わせの側面により、 [!DNL Google Analytics] 分析を行うために他のデータに結合するデータ。 例えば、次のようにします。 `Total Time On Site By Ad Campaign` からのデータ [!DNL Google Analytics] そしてそれを仲間に入れ `Total Spent Per Campaign` からのデータ [!DNL Facebook Ads] エンゲージメントに費やされたコストの全体像を把握するために。

を使用 [!DNL Google Analytics Live] 一方で、 [!DNL Google Analytics] グラフは、 [!DNL MBI] data warehouse を使用します。

## 関連：

* [接続中 [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
