---
title: 投資家向けダッシュボードの構築
description: 投資家向けのダッシュボードを作成する方法を説明します。
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# 投資者ダッシュボードの作成

多くの顧客は投資家と連携し、プラットフォームから情報を共有する必要がありますが、日々のビジネス上の意思決定を行うために作成するダッシュボードは、投資家が探しているものではない場合があります。 包括的でシンプルで、アクティブで潜在的な投資家との共有に最適なダッシュボードの作成方法に関するベストプラクティスを以下に示します。

投資家ダッシュボード用にレポートを作成する必要がある情報を次に示します。

## スカラーレポート

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## ビジュアルレポート

* **[!UICONTROL Revenue by quarter]**
   * 指標 — 売上高
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * 指標 — 初回注文売上高
   * フィルター — ユーザーの注文番号が 1 に等しい
   * 指標 2 — リピート注文売上高
      * フィルター — ユーザーの注文番号が 1 より大きいです
   * 「複数の Y 軸」のチェックボックスをオフにします。
   * 積み重ね縦棒グラフに変更する
* **[!UICONTROL AOV by quarter]**
   * 指標 1 — 売上高
      * この指標を非表示にする
   * 指標 2 — 注文数
      * この指標を非表示にする
   * 数式 — AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * 指標 — 売上高
   * 顧客別のグループ `utm_source`
* **[!UICONTROL Revenue from top 10 products]**
   * 指標 — 製品の売上高
      * グラフを非表示にする
      * 製品名でグループ化します。 すべての製品を選択します。
      * 時間範囲を全時間に設定
      * 間隔を「なし」に設定します。
      * 「上位/下位を表示」で、上位 10 を製品の利益で並べ替えて表示します
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * 指標 — ユニーク購入者
      * パースペクティブ — 累積
* **[!UICONTROL Site visits - New vs. repeat by month]**
* セッション

を使用 [!DNL Google Analytics] 統合には、次のレポートを含めることができます。

* サイト訪問数
* コンバージョン率

を使用 [コマースデータエンリッチメントサービス](https://business.adobe.com/products/magento/magento-commerce.html)を使用すると、次のレポートを含めることができます。

* 州/地域、年齢、性別別のユニーク顧客。

## その他のヒント

* 明確で簡潔な [命名規則](../best-practices/naming-elements.md)
* 投資家ユーザーとダッシュボードを共有
* または、 **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* 1 つのダッシュボードのみを作成します。 これにより、コンテンツの保守が容易になり、投資家が何を見ているかを正確に把握できます。

レポートを慎重に整理し、詳細に注意します。 完了すると、ダッシュボードは次のようになります。

![](../../mbi/assets/investor-dboard-example.png)
