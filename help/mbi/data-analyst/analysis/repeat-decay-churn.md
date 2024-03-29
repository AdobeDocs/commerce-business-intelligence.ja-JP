---
title: 繰り返し確率減衰とチャーンの分析
description: 注文と顧客がチャーンすると予想されるタイミングとの間の時間の経過を学び、理解します。
exl-id: ea26052d-ac74-43b7-a4a6-977800d4c719
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# 確率減衰とチャーンを繰り返す

売上高の一部がリピート購入に起因する場合、常連客ベースの莫大な価値を知っていると思われます。 このためには、注文間の時間の経過と、顧客がチャーンすると予想される時間の経過を理解することが重要です。

このトピックでは、次の質問に答えるのに役立つ分析について説明します。

* 顧客が別の購入を行う確率はどれくらいですか？
* 繰り返し注文の確率は、顧客の最新の購入以降、時間と共にどのように変化しますか。
* 顧客をいつチャーンと見なす必要がありますか？ したがって、再アクティベーションキャンペーンはいつ開始する必要がありますか？

## 推奨指標

繰り返しの確率減衰とチャーンを分析する場合は、 ([または建物](../../data-user/reports/ess-manage-data-metrics.md)) を参照してください。

### 最初の繰り返し順序の確率

この測定は、繰り返し注文の合計数を、合計注文件数に対するパーセントとして定義します。 別の言い方で、順序が後に続く可能性を表現しました。 この確率が 50%を超える場合、すべての注文の半分以上に続いて後続の注文が続くことを意味します。

### 注文から指定された月の繰り返し注文の確率

このメジャーは、最後の注文から経過した月数を指定して、ユーザーが再度注文する確率を示します。 この指標の生成に使用する数式は、次の操作を簡単におこなえます。

![確率式を繰り返す](../../assets/Repeat_probability_formula.png)

ビジネスモデルによっては、顧客が注文した直後に繰り返し注文の確率が下がり、その後数か月で減少が続く場合や、季節による変動やスパイクが示される場合があります。

リピート購入を期待される顧客の割合（およびこのトレンドの経時的な変化）を把握することで、顧客を一定の間隔でターゲティングし、リピート購入の確率を最大化できます。 したがって、リピート購入の確率が下がっている場合は、顧客をチャーンとして識別する時間を選択し、取り組みを定着から再アクティブ化に切り替えることができます。

## 今日の例

典型的な e コマースビジネスの繰り返しの確率減衰を見てみましょう。

![注文から数か月後に指定された最初の繰り返し注文確率繰り返し注文確率。](../../assets/Order_probability_reports.png)

### 最初の繰り返し順序の確率

この例では、最初の繰り返し注文の確率（顧客が繰り返し購入する可能性）は 60%です。 つまり、このビジネスで発行されたすべての注文の 60%に続いて、後続の注文が発生します。

### 注文から指定された月の繰り返し注文の確率

このレポートは、最後の注文から数ヶ月が経過した場合に、顧客が再度注文する確率を表示します。 このレポートでは、チャーンしきい値に特異な定義はありませんが、Adobeでは、確率減衰が初期繰り返し確率レートの半分の値を超えるポイントとしてチャーンを定義することをお勧めします。

この例の初期繰り返し確率率は 60%なので、チャーン日は、繰り返し注文の確率が 60%/2 = 30%を下回った時刻、または約 6 ヶ月の時刻になります。 60%の注文のうち、もう 1 回の注文を受けると予想されるものの、半数が最初の 6 ヶ月以内に発注された。

別の言い方で顧客がフォローアップ注文をする場合は 6 ヶ月後よりも最後の注文から 6 ヶ月以内に同じ処理を行った可能性が高いと言います 顧客が 6 ヶ月後に再購入しなかった場合は、この顧客を再度呼び込むために、再アクティブ化キャンペーンを開始する必要があります。

ビジネスモデルに応じて、繰り返し注文の確率が 50%または 10%を下回るポイントなど、異なるしきい値を選択することもできます。 内部の知識が異なる数を示す場合は、必ずそれを使用してください。

最終的な目標は、保存から再アクティブ化への切り替えが意味を持つしきい値を選択することです。 リテンションの取り組みには、フォローアップ購入を提案した既存の顧客と再び関わるための E メールが含まれる場合があります。一方、再アクティブ化の取り組みには、クーポンや契約を持つラップ済みの顧客に E メールが含まれます。

## どのような質問を考慮すべきですか？

繰り返し注文の確率をビジネスに当てはめるのに役立つように、独自のデータを調べる際に、Adobeは次の質問を検討するよう提案します。

* 最初の繰り返し注文の確率は期待されますか？ そうでないのに、なぜ高い、低いと思うのか。
* 最後の注文から特定の月の繰り返し注文の確率に大きな減少はありますか？ その場合、これらの変更は期待されるものですか？
* 現在のチャーンしきい値は何ですか？
* 現在のチャーンしきい値は、前回の注文レポートから数ヶ月経過した場合、繰り返し注文の確率の値の 1 つに揃っていますか？
* 現在のしきい値は、リテンションから再アクティブ化に切り替わる広告活動を反映していますか？
* しきい値を、確率減衰が最初の繰り返し確率の半分の値を超える月に変更するのは、お客様のビジネスにとって合理的ですか？

## 私は他に何を分析すべきですか？

上記の分析を作成し、チャーンしきい値を決定した後は、より多くの分析を作成して、チャーンユーザーの一般的なトレンドを特定できます。 例えば、同じ期間にチャーンを購入した顧客や、類似した製品を最後の注文で購入した顧客はいますか。 チャーンしきい値を設定したら、これらのチャーン対象の顧客の特定の特性をさらに掘り下げて調べることができます。

複数の製品を提供する場合、特定の製品を購入した顧客の行動が、他の顧客と比べて時間の経過と共にどのように異なるのか疑問に思うかもしれません。 詳細を知りたい場合は、 このチュートリアルを調べて、購入した特定の製品に基づく、顧客コホートのライフタイム購入行動を調べます。

このベストプラクティスは、次の URL で提供されます。 [!DNL Adobe Commerce Intelligence] データ分析サービス (DAS)。 [サポートへの問い合わせ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 詳しくは、を参照してください。

### 関連

* [顧客の獲得および維持に対するクーポンの影響の分析](../analysis/coupon-impact.md)
* [顧客の再購入行動の分析](../analysis/repurchase-behavior.md)
