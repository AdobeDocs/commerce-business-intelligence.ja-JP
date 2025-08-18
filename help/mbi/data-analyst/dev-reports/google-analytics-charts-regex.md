---
title: Google Analyticsのグラフの作成
description: Google Analytics データからグラフを作成する方法を説明します。
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# [!DNL Google Analytics] グラフの作成

（正規表現構文のヘルプを使用）

[[!DNL Google Analytics]  アカウント ](../../data-analyst/importing-data/integrations/google-analytics.md) に接続したら、[!DNL Google Analytics] データを使用してグラフを作成できます。

## [!DNL Google Analytics] グラフの作成

1. 「**[!UICONTROL Add Chart** > **Create New Chart]**」をクリックします。

1. `Chart Builder` で指標を選択する場合は、リストの下部までスクロールして、[!DNL Google Analytics] プロファイルを含むセクションを探します。 2 つ目の指標ドロップダウンが表示されます。 ここで、分析する指標を選択できます。

1. 指標を選択したら、表示する `time period`、`interval`、データ `perspectives` を選択することで、このグラフを他のグラフと同じように続行できます。

1. ここでの大きな違いは、フィルターに正規表現を使用 `√` ることです。 正規表現（略して正規表現）は、検索パターンを説明するための特別なテキスト文字列です。 [[!DNL Google] Analytics 正規表現に関するガイド ](https://support.google.com/analytics/answer/1034324?hl=en) の正規表現構文の例を参照してください。

>[!NOTE]
>
>\文字を使用してエスケープする必要がある特殊文字は、以下のメタ文字のみです。

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
