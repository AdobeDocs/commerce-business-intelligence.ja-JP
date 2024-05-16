---
title: Google Analyticsグラフの作成
description: Google Analyticsデータからグラフを作成する方法を説明します。
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# 作成 [!DNL Google Analytics] グラフ

（正規表現構文のヘルプを使用）

接続したら [[!DNL Google Analytics] アカウント](../../data-analyst/importing-data/integrations/google-analytics.md)を使用してグラフを作成できます [!DNL Google Analytics] データ。

## 作成 [!DNL Google Analytics] グラフ

1. クリック **[!UICONTROL Add Chart** > **Create New Chart]**.

1. で指標を選択する場合 `Chart Builder`リストの下部までスクロールし、を含むセクションを見つけます [!DNL Google Analytics] プロファイル。 2 つ目の指標ドロップダウンが表示されます。 ここで、分析する指標を選択できます。

1. 指標を選択したら、次のオプションを選択することで、他のグラフと同様にこのグラフを進めることができます `time period`, `interval`、およびデータ `perspectives` あなたが見たいと思うもの。

1. ここでの 1 つの大きな違いは `√` フィルターに正規表現を使用します。 正規表現（略して正規表現）は、検索パターンを説明するための特別なテキスト文字列です。 で正規表現構文の例を参照してください。 [[!DNL Google] analytics 正規表現に関するガイド](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>\文字を使用してエスケープする必要がある特殊文字は、以下のメタ文字のみです。

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
