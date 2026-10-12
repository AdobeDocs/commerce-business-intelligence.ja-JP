---
title: Google Analytics Warehoused Dataの想定
description: Google Analyticsウェアハウスデータの使用方法を説明します。
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/-Pulnv7J-TmXxL0msB6nhuMKIWbCpS0163rewp9BOvc'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 1%
---
# [!DNL Google Analytics Warehoused] データが必要です

>[!NOTE]
>
>[管理者権限](../../../administrator/user-management/user-management.md)が必要です。

>[!NOTE]
>
>一部の情報は[[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics)に友達から許可を得て使用されました。

[!DNL Commerce Intelligence]の[!DNL Google Analytics Warehoused]統合では、[!DNL Google Analytics] [Core Reporting API](https://developers.google.com/analytics/devguides/reporting/core/v3/)を使用しています。

>[!NOTE]
>
>予期しない結果や意味のない結果を回避するには、使用するディメンションが[で`Report Builder`で使用する1つ以上の指標](https://ga-dev-tools.google/dimensions-metrics-explorer/)と互換性があることを確認します。

1つのテーブル `report`がData Warehouseに作成されます。

このテーブルのスキーマは、設定プロセス中に選択した指標とディメンションと、その他2つの列（`start-date`と`end-date`）で構成されています。

例えば、設定中に次の指標とディメンションを選択した場合：

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

この表は、次の例のようになります。

| **列名** | **説明** |
|-----|-----|
| `\_id` | この列は`primary key`です。 |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence]の一意のID。 この列は[!DNL Commerce Intelligence]によって作成されました。 |
| `\_updated\_at` | この列には、データ行が最後に更新された時刻が含まれます。 この列は[!DNL Commerce Intelligence]によって作成されました。 |
| `start-date` | 行の日付を識別します。 |
| `end-date` | 行の日付を識別します。 |
| `month` | 選択したディメンション：セッションの月、01から12までの2桁の整数。 |
| `users` | 選択した指標：要求された期間のユーザーの合計数。 |

{style="table-layout:auto"}

## [!DNL Google Analytics Warehoused]と[!DNL Live Integration]の違い

主な差別化要因は、1つの統合が保存され（[!DNL Google Analytics Warehoused]）、もう1つは保存されず（[!DNL Google Analytics Live]）、です。 [!DNL Google Analytics Warehoused]の場合、これにより[!DNL Google Analytics] データの操作が可能になり、[!DNL Google Analytics]とその他のデータソースを組み合わせて、インサイトに満ちたレポートを作成できるようになります。

操作の観点から何ができるかの例については、[!DNL Google Analytics]件の広告キャンペーンを参照してください。 例えば、Q4に複数の広告キャンペーンと異なる名前があったとします。 このキャンペーンは、特定のマーケティング施策を通じて実施されました。 ウェアハウスデータを使用すると、該当するキャンペーン名を検索し、Q4 イニシアチブ名`Operation Dumbo`を返す列を作成できます。

組み合わせアスペクトでは、[!DNL Google Analytics] データを他のデータと結合して分析を行うことができます。 例えば、[!DNL Google Analytics]から`Total Time On Site By Ad Campaign`個のデータを取得し、[!DNL Facebook Ads]から`Total Spent Per Campaign`個のデータに結合して、エンゲージメントにかかるコストを包括的に把握できます。

一方、[!DNL Google Analytics Live]統合では、[!DNL Google Analytics]個のグラフはすべて、[!DNL Commerce Intelligence] Data Warehouseに保存されていない小さなサイロのようなものです。

## 関連：

* [接続中 [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
