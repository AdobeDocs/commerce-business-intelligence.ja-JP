---
title: ホリデーシーズンのパフォーマンスの分析
description: 今年の成長パターンが前年と比較してどのように変化しているかを学び、理解します。
exl-id: 328f30b8-0db6-48fd-8d97-95f0bc7e4803
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# ホリデーショッピング分析

あなたのビジネスにとって、休日は年の中で最も忙しい時の 1 つになるかもしれません。 大規模なアメリカの顧客ベースを持つ小売業者の場合、ホリデーシーズンは、通常、感謝祭と新年の間の月をまたいでいます。

例えば、ビジネスがショートカットやプール用品を販売する場合は、夏の間にラッシュが発生する可能性があります。 このトピックでは、様々な年の高い季節を比較するのに役立つ分析を紹介します。

## 推奨指標

ホリデーシーズンのパフォーマンスを分析する際は、[または建物](../../data-user/reports/ess-manage-data-metrics.md)) を参照してください。

### 新規顧客数、注文数、売上高

今年の成長パターンを前年と比較した結果を把握するために、これらの対策の分析を検討してください。 新規顧客数、新規注文数および売上高は、指定した期間（ホリデーシーズン）に対する日別のビジネスパフォーマンスを示します。 また、累積的な視点を使用して、これらの測定を分析し、経時的な指標の変化を確認できます。

### 平均注文額

この測定は、ホリデーシーズンの全体的な平均注文額を表示します。

## 例：日別のホリデーシーズンの売上高

分析する指標を知ったので、2014 年と 2015 年の両方の 11 月と 12 月の祝日期間中の売上高データの例を見てみましょう。

![2014 年と 2015 年のホリデーシーズンの売上高](../../assets/Analyzing_holiday_season.png)

この例では、2014 年と 2015 年の売上高の急増が 2 つあります。これらの増加は、ブラックフライデーおよびサイバーマンデーと同時に発生します。 2014 年と 2015 年の同じ日にスパイクが発生していないことに注意してください。 これは、ブラック・フライデーが 2014 年 11 月 27 日に、2015 年 11 月 28 日に落ちたからです。 同様に、サイバーマンデーは 2014 年 11 月 30 日、2015 年 12 月 1 日でした。

さらに、2014 年には表示されない、2015 年 12 月 19 日の売上高の急増があります。 前年に入手できなかったこの土曜日に販売が行われた可能性があります。

上記の数日以外にも、この 2 年間の売上高は一緒に追跡されます。

## どのような質問を考慮すべきですか？

ビジネスの季節的なトレンドを把握するのに役立つように、独自のデータを調べる際に留意すべき質問を次に示します。

* 年々の傾向は予想されていますか？
* トレンドは、季節ごとの変化に対する期待を反映しているか。
* 年によって違いはありますか。 これらの違いは説明できますか。
* 特定の 1 年間にプロモーションは提供されましたか？
* 特定の年の間に値上がりはありましたか？
* 特定の年間、広告費用は増加したのでしょうか？

## 私は他に何を分析すべきですか？

選択肢の 1 つは、ホリデーシーズン中の顧客の購入行動を分析することです。 ホリデーシーズンの間に獲得した顧客は、ホリデーシーズン以外で獲得した顧客より多くの費用を費やしているか、または、購入頻度が高いか。

もう 1 つの選択肢は、ホリデーシーズンの間にキャンペーン別に ROI を分析することです。 ホリデーシーズンの間に実行される特定のキャンペーンの ROI は高くなりますか。 この季節に高い ROI を持つキャンペーンの費用を増やす必要がありますか？

さらに、割引注文の数と定価注文の数を分析できます。 [ほとんどの顧客が注文の購入を待っています](../analysis/coupon-usage.md) 休暇シーズンの間に、または定価の商品を購入していますか。

### 関連

* [顧客の獲得および維持に対するクーポンの影響の分析](../analysis/coupon-impact.md)
* [顧客の再購入行動の分析](../analysis/repurchase-behavior.md)
