---
title: Google Analyticsグラフを作成
description: Google Analyticsデータからグラフを作成する方法を説明します。
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# 作成 [!DNL Google Analytics] グラフ

（正規表現構文のヘルプを使用）

接続後、 [[!DNL Google Analytics] アカウント](../../data-analyst/importing-data/integrations/google-analytics.md)を使用すると、 [!DNL Google Analytics] データ。

## 作成 [!DNL Google Analytics] グラフ

1. クリック **[!UICONTROL Add Chart** > **Create New Chart]**.

1. 指標を選択する際に、 `Chart Builder`をクリックし、リストの下部までスクロールして、 [!DNL Google Analytics] プロファイル。 2 つ目の指標ドロップダウンが表示されます。 ここでは、分析する指標を選択できます。

1. 指標を選択した後、このグラフを他のグラフと同じように使用するには、 `time period`, `interval`、およびデータ `perspectives` あなたが見たいと思う

1. ここで大きな違いは `√` は、フィルターに正規表現を使用します。 正規表現 (regex for short) は、検索パターンを説明する特別なテキスト文字列です。 正規表現の構文の例については、 [[!DNL Google] Analytics 正規表現に関するガイド](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>\文字を使用してエスケープする必要がある特殊文字は、次のメタ文字のみです。

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
