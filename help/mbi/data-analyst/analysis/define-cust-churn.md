---
title: 顧客チャーンの定義
description: トランザクション顧客のチャーンを定義するのに役立つダッシュボードの設定方法を説明します。
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---

# トランザクション顧客チャーン

このトピックでは、トランザクション顧客のチャーンを定義するのに役立つダッシュボードの設定方法を示します。

![&#x200B; チャーンレートとリテンション指標を表示する顧客チャーンダッシュボード &#x200B;](../../assets/churn-deashboard.png)

この分析には [&#x200B; 高度な計算列 &#x200B;](../data-warehouse-mgr/adv-calc-columns.md) が含まれています。

## 計算される列

作成する列

* `customer_entity` テーブル
* `Customer's lifetime number of orders`
* 定義を選択：`Count`
* [!UICONTROL table] を選択：`sales_flat_order`
* [!UICONTROL column] を選択：**`entity_id`**
* [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* カウントされる注文

* `sales_flat_order` テーブル
* `Customer's lifetime number of orders`
* 定義を選択：[ 結合 ] 列
* [!UICONTROL table] を選択：`customer_entity`
* [!UICONTROL column] を選択：`Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* 定義を選択：`Age`
* [!UICONTROL column] を選択：`created_at`

* **`Customer's order number`** は、アナリストが **[チャーンの定義]** チケットの一部として作成します
* **`Is customer's last order`** は、アナリストが **[チャーンの定義]** チケットの一部として作成します
* **`Seconds since previous order`** は、アナリストが **[チャーンの定義]** チケットの一部として作成します
* **`Months since order`** は、アナリストが **[チャーンの定義]** チケットの一部として作成します
* **`Months since previous order`** は、アナリストが **[チャーンの定義]** チケットの一部として作成します

## 指標

新しい指標はありません。

>[!NOTE]
>
>新しいレポートを作成する前に、必ず [&#x200B; すべての新しい列をディメンションとして指標に追加する &#x200B;](../data-warehouse-mgr/manage-data-dimensions-metrics.md) ようにしてください。

## レポート

* **最初の繰り返し順序確率**
* 指標 A：全期間リピート注文
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 指標 B：全期間オーダー
* [!UICONTROL Metric]：注文数

* [!UICONTROL Formula]：最初の繰り返し順序確率
* &#x200B;
  [!UICONTROL 数式]: `A/B`
* &#x200B;
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart type]: `Scalar`

* **注文以降に指定された月の繰り返し注文確率**
* 指標 A：以前の注文以降の月別の繰り返し注文（非表示）
* [!UICONTROL Metric]: `Number of orders`
* &#x200B;
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 指標 B：注文以降の過去の注文件数（月別）（非表示）
* [!UICONTROL Metric]: `Number of orders`
* &#x200B;
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 指標 C：全期間のリピート注文（非表示）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* &#x200B;
  [!UICONTROL Group by]: `Independent`

* 指標 D：すべての時間の最後の注文（非表示）
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* &#x200B;
  [!UICONTROL Group by]: `Independent`

* [!UICONTROL Formula]：最初の繰り返し順序確率
* &#x200B;
  [!UICONTROL 数式]: `(C-A)/(C+D-A-B)`
* &#x200B;
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* top.bottom を表示：上位 24 個のカテゴリをカテゴリ名順に表示

* &#x200B;
  [!UICONTROL Chart type]: `Line`

最初のリピート注文確率レポートは、リピート注文の合計/注文の合計を表します。 すべての注文は、リピート注文を行う機会です。リピート注文の数は、実際に行う注文のサブセットです。

使用する式は、（X か月後に発生したリピート注文の合計）/（少なくとも X か月前の注文の合計）を簡略化します。 これは、注文後 X か月が経過している場合、ユーザーが別の注文を行う可能性が Y% あることを歴史的に示しています。

ダッシュボードを作成したら、最も一般的な質問は次のとおりです。チャーンしきい値を決定するにはどうすればよいですか？

**これに対する「唯一の正解」はありません。** ただし、Adobeでは、線が最初の繰り返し確率率の半分の値と交差する点を見つけることをお勧めします。 これは、「リピート注文をするつもりなら、今ごろはもう間に合っただろう」と言えるポイントです。 最終的な目標は、「リテンション」から「再アクティブ化」に切り替えると効果的な、しきい値を選択することです。

すべてのレポートをコンパイルした後、必要に応じてダッシュボード上で整理できます。 結果は、ページ上部の画像のようになります

分析中に質問が発生した場合や、プロフェッショナルサービスチームに依頼したい場合は、[&#x200B; サポートにお問い合わせください &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)。
