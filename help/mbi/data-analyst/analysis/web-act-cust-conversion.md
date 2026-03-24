---
title: web サイトのアクティビティと顧客コンバージョン率の分析
description: ページビュー、セッション、ユーザーなど、web サイトのアクティビティと、顧客のコンバージョン率を長期的に追跡するダッシュボードの設定方法について説明します。
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
TQID: https://experienceleague.adobe.com/HcoHrBbXXjQGsd80DA06Dwq2dDmhUiuRbRLj-QONlw4
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 756
ht-degree: 0%

---

# Web サイトのアクティビティの分析

[!DNL Adobe Commerce Intelligence]を使用すると、広告コスト データを他のデータと簡単に統合できます。 これにより、web サイトのアクティビティを把握できるだけでなく、登録ユーザーや購入したweb サイト訪問者の割合を把握できます。

このトピックでは、ページビュー、セッション、ユーザーなど、web サイトのアクティビティと顧客のコンバージョン率を経時的に追跡するダッシュボードの設定方法を説明します。

## 前提条件

**広告コスト データを読み込む** - [[!DNL [Google AdWords]]](../importing-data/integrations/google-adwords.md)を[!DNL Adobe Commerce Intelligence]に接続すると、Commerce Intelligenceでの[!DNL AdWords]の費用が自動的に同期されます。

**ユーザー獲得チャネルデータの追跡** - [!DNL Google AdWords] データをデータベース内の特定の注文に結び付けるには、[経由で](../analysis/google-track-user-acq.md) ユーザー獲得[!DNL Google Analytics E-commerce]を追跡する必要があります。 これにより、各注文をutm ソースとミディアムに接続できます。

## ユーザー獲得キャンペーン

このレポートコレクションは、次の機能を使用して構築されています。

* [!DNL Google AdWords] データの接続時に自動的に生成される指標
* `Number of orders`や`New users`など、既にお客様のアカウントで利用できる基本的な指標
* 注文のutm ソースと注文のutm メディアなど、[!DNL Google Analytics Ecommerce] データをデータベースに結合する際に作成されたディメンション。 これらのフィールドが現在アカウントで使用できない場合は、サポートチームにお問い合わせください

## レポートの作成

**最初に、ページビュー数、セッション数、ユーザー数を時系列で表示するレポートを作成します。**

1. レポートを作成する。
1. **[!UICONTROL Add Metric]**&#x200B;をクリックし、ドロップダウンの下部にある[!DNL Google Analytics] セクションにマウスを合わせて`Page Views`を選択します。
1. 別の指標を追加し、今度は[!DNL Google Analytics]を選択して`Sessions` セクションにマウスを移動します。
1. 3つ目の指標を追加します。今回は[!DNL Google Analytics]を選択し、`Users` セクションにマウスポインターを合わせます。
1. 次に、期間を31日前から1日前の移動範囲に変更し、時間間隔を`by day`に調整します。
1. レポートに名前を付け（`Page views, sessions and users by day`など）、**[!UICONTROL Save]**&#x200B;をクリックします。

**2つ目のレポートでは、過去1年間のページビュー数を確認しています：**

1. レポートを作成する。
1. **[!UICONTROL Add Metric]**&#x200B;をクリックし、ドロップダウンの下部にある[!DNL Google Analytics] セクションにマウスを合わせて、_ページビュー_&#x200B;を選択します。
1. 期間を13か月前から1か月前の移動範囲に変更し、期間を`by month`に調整します。
1. レポートに「`Page views by month,`」などの名前を付けて「**[!UICONTROL Save]**」をクリックします。

**3つ目のグラフは、過去1年間の直帰率を示しています：**

1. レポートを作成する。
1. **[!UICONTROL Add Metric]**&#x200B;をクリックし、ドロップダウンの下部にある[!DNL Google Analytics] セクションにマウスを合わせ、_直帰率_&#x200B;を選択します。
1. 期間を13か月前から1か月前の移動範囲に変更し、期間を`by month`に調整します。
1. レポートに「`Bounce rate by month`」などの名前を付けて、「**[!UICONTROL Save]**」をクリックします。

**新規訪問者と再訪問者の平均セッション長を見てみましょう：**

1. レポートを作成する。
1. 「**UICONTROL Add Metric**」をクリックし、ドロップダウンの下部にある「[!DNL Google Analytics]」セクションにマウスを合わせて「`Average Session Length`」を選択します。
1. 期間を13か月前から1か月前の移動範囲に変更し、期間を`by month`に調整しますか？
1. `Group by`を追加し、`New or returning visitor`を選択します。  「`Show All`」ボックスをオンにし、「**[!UICONTROL Apply]**」をクリックします。
1. レポートに「`Average session length`」などの名前を付けて、「**[!UICONTROL Save]**」をクリックします。

**次に、過去30日間の上位の参照ドメインを確認します：**

1. レポートを作成する。
1. **[!UICONTROL Add Metric]**&#x200B;をクリックし、ドロップダウンの下部にある[!DNL Google Analytics] セクションにマウスポインターを合わせて`Sessions`を選択します。
1. 期間を31日前から1日前の移動範囲に変更し、時間間隔を`none`に調整します。
1. `Group by`を追加し、`ga:source`を選択します。  「_すべて表示_」ボックスにチェックを入れ、**[!UICONTROL Apply]**&#x200B;をクリックします。
1. 別の`group by`を追加し、`ga:medium`を選択します。 もう一度`Show All` ボックスをオンにし、**[!UICONTROL Apply]**&#x200B;をクリックします。
1. レポートに`Top 20 Referring Domains, 30 Days`などの名前を付けて、**[!UICONTROL Save]**&#x200B;をクリックします。

**最後に、コンバージョンを確認します：**

1. レポートを作成する。
1. 次の指標を追加します。

* `New users`
   * メトリック名の下の&#x200B;**[!UICONTROL Hide]**&#x200B;をクリックします

* `Number of orders`
   * `Customer's order number` = 1のフィルターを追加し、**[!UICONTROL Apply]**&#x200B;をクリックします
   * メトリック名をクリックしてメトリック名を変更し、`Number of first orders`と呼び出してから、**[!UICONTROL Hide]**&#x200B;をクリックします

* `Number of orders`
   * 指標&#x200B;**[!UICONTROL Hide]**

* `Users`
   * 指標&#x200B;**[!UICONTROL Hide]**
   * 期間を`24 months ago to now`に変更し、期間を`by month`に調整します。
   * **[!UICONTROL Formula]**&#x200B;をクリックして、次の数式を追加します。
   * A/Dで、**[!UICONTROL Apply]**&#x200B;をクリックします
   * 数式`Registration conversion`の名前を変更
   * B/Dで「**[!UICONTROL Apply]**」をクリックします
   * 数式`First order conversion`の名前を変更
   * C/Dで「**[!UICONTROL Apply]**」をクリックします
   * 数式`Any order conversion`の名前を変更

* 次に、`Conversion by month`などの名前をレポートに付けて、**[!UICONTROL Save]**&#x200B;をクリックします。

## 次のステップ

web トラフィックとコンバージョン率に関するデータにアクセスできるようになったら、「どのサイトがサイトへのトラフィックの増加に最適か？」といった、ビジネス上の意思決定を促進するために、データを収集し始めることができます。 あるいは、生涯価値の高い顧客を獲得するのに、最も効果的なキャンペーンはどれですか？

広告費とマーケティング戦略を調整しても、[!DNL Commerce Intelligence]で引き続き結果を追跡し、進化する企業の優先事項に対応するために、このダッシュボードを繰り返し実行することができます。
