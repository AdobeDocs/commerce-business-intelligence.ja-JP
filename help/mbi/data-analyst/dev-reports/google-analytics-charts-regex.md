---
title: Google Analytics チャートの作成
description: Google Analytics データからチャートを作成する方法を説明します。
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xfh0BjVasnSNP9mic7ps4jckaGpjF7INFNi2lSaKi-o
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 160
ht-degree: 0%

---

# [!DNL Google Analytics] グラフを作成

（正規表現の構文ヘルプを使用）

[[!DNL Google Analytics]  アカウント ](../../data-analyst/importing-data/integrations/google-analytics.md)を接続したら、[!DNL Google Analytics] データを使用してグラフを作成できます。

## [!DNL Google Analytics] グラフを作成

1. **[!UICONTROL Add Chart** > **Create New Chart]**&#x200B;をクリックします。

1. `Chart Builder`で指標を選択する場合は、リストの一番下までスクロールして、[!DNL Google Analytics] プロファイルを含むセクションを見つけます。 2つ目の指標ドロップダウンが表示されます。 ここで、分析したい指標を選択できます。

1. 指標を選択した後、表示する`time period`、`interval`、およびデータ `perspectives`を選択して、このグラフを他のグラフと同じように進めることができます。

1. ここでの大きな違いは、`√`がフィルターに正規表現を使用することです。 正規表現（短い正規表現）は、検索パターンを記述するための特殊なテキスト文字列です。 Analytics正規表現に関するガイド [[!DNL Google] の正規表記法の例を参照してください](https://support.google.com/analytics/answer/1034324?hl=en)。

>[!NOTE]
>
>\ キャラクタを使用してエスケープする必要がある特殊文字は、次のメタ文字だけです。

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
