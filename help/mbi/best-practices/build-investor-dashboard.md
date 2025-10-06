---
title: 投資家向けダッシュボードの構築
description: 投資家向けダッシュボードの作成方法を説明します。
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Data Integration
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '289'
ht-degree: 0%

---

# 投資家ダッシュボードの作成

多くのクライアントは投資家と協力し、プラットフォームから情報を共有する必要がありますが、日々のビジネス上の意思決定のために作成するダッシュボードは、投資家が探しているものではない可能性があります。 以下では、包括的でシンプルで、アクティブな投資家や潜在的な投資家と共有するのに最適なダッシュボードの作成方法に関するベストプラクティスをいくつか説明します。

投資家ダッシュボードのレポートを作成するには、次の操作が必要です。

## スカラーレポート

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## ビジュアルレポート

* **[!UICONTROL Revenue by quarter]**
   * 指標 – 売上高
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * 指標 – 初回の注文売上高
      * フィルター – ユーザーの注文番号は 1 に等しい
   * 指標 2 – リピート注文売上高
      * フィルター – ユーザーの注文番号が 1 より大きい
   * 複数の Y 軸のチェックボックスをオフにします
   * 積み重ね柱状グラフに変更
* **[!UICONTROL AOV by quarter]**
   * 指標 1 – 売上高
      * この指標を非表示
   * 指標 2 – 注文数
      * この指標を非表示
   * 数式 – AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * 指標 – 売上高
   * 顧客の `utm_source` でグループ化
* **[!UICONTROL Revenue from top 10 products]**
   * 指標 – 製品売上高
      * グラフを非表示
      * 製品名でグループ化します。 すべての製品を選択します。
      * 時間範囲を「全時間」に設定します。
      * 時間間隔をなしに設定します
      * 「上位/下位を表示」で、製品の利益順に並べ替えられた上位 10 個のみを表示します
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * 指標 – ユニーク購入者
      * 透視投影 – 累積
* **[!UICONTROL Site visits - New vs. repeat by month]**
* セッション

[!DNL Google Analytics] 統合を使用すると、次の項目に関するレポートを含めることができます。

* サイト訪問数
* コンバージョン率

[Commerce データエンリッチメントサービス &#x200B;](https://business.adobe.com/products/magento/magento-commerce.html) を使用すると、次の項目に関するレポートを含めることができます。

* 州/地域、年齢、性別ごとのユニーク顧客。

## その他のヒント

* 明確で簡潔な [&#x200B; 命名規則 &#x200B;](../best-practices/naming-elements.md) を使用します
* 投資家ユーザーとのダッシュボードの共有
* または、**[!UICONTROL Automated email summary]** （../data-user/export-data/email-summaries.md）経由で送信します
* 1 つのダッシュボードのみを作成します。 これにより、コンテンツのメンテナンスが容易になり、投資家が何を見ているかが正確にわかります。

レポートを思慮深く整理し、詳細に注意を払います。 完了すると、ダッシュボードは次のようになります。

![&#x200B; 投資家ダッシュボードの作成 &#x200B;](../../mbi/assets/investor-dboard-example.png)
