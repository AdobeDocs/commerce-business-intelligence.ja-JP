---
title: 最も価値の高いマーケティングソースおよびチャネルの特定
description: 最も価値の高いマーケティングチャネルを明らかにするために使用できる、いくつかのレポートについて説明します。
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 0%

---

# 成功するマーケティングソースの特定

オーディエンスを調査し、キャンペーンを作成し、いくつかのマーケティングチャネルに投資しました。 時間が経過した今、これらのチャネルのパフォーマンスはどうですか？ 最も新しいユーザーを取り込んだのは、どのチャネルですか？ 総売上高に最も貢献したソースは何ですか？

（を使用） [!DNL Adobe Commerce Intelligence]を使用すると、が次のいずれに該当するかにかかわらず、リファラルソース別に売上高とユーザーを簡単にセグメント化できます [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) またはカスタムデータフィールドです。 このセグメント化により、最もパフォーマンスの高いチャネルを見つけ、マーケティング予算をより適切に投資できます。

このトピックでは、最も価値の高いマーケティングチャネルを明らかにするために使用できるレポートをいくつか紹介します。

* [ソース別の新規ユーザー](#newusersbysource)
* [ユーザーソース別の平均生涯売上高](#avglifetimerev)
* [ユーザーソース別の平均注文値](#avgorderval)
* [収益（ユーザー登録日およびソース別）](#revbyregdateandsource)
* [繰り返し注文（ユーザーソース別）](#repeatordersbysource)

## 前提条件 {#prereqs}

このトピックで分析を作成するには、マーケティング獲得/リファラルソースデータにアクセスする必要があります。 まだ追跡していない場合は、次のものを持参する必要があります [参照元データの注文元 [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) 対象 [!DNL Adobe Commerce Intelligence] 続行する前に。 また、分析にユーザーデバイス情報を追加すると、参照で使用しているテクノロジーを確認できます。

## ソース別の新規ユーザー {#newusersbysource}

最も価値の高いチャネルを決定するには、リファラルソースのパフォーマンスを評価することが重要です。 このレポートは、新規登録ユーザー数を取得元別に経時的に表示するため、新規登録ユーザーの取得におけるリファラルソースのパフォーマンスを追跡できます。

でレポートを作成するには [Report Builder](../../tutorials/using-visual-report-builder.md)、を追加します **新規ユーザー** レポートに対する指標（または新規ユーザーの数を経時的にカウントする同等の指標）。 次に、以下の手順を実行します。

1. を [!UICONTROL Time Period] を分析する登録期間に変更します。
1. を [!UICONTROL Interval] を毎月に更新します。
1. を設定 [!UICONTROL Group By] 取得元（または参照元）に追加し、追加する取得元を選択します。
1. この例では、を使用します `stacked columns` [!UICONTROL chart type].

次のチュートリアルを視覚的に示します。

![ソース別の新規ユーザー数レポートを作成します。](../../assets/New_Users_by_source.gif)

## ユーザーソース別の平均生涯売上高 {#avglifetimerev}

新しいユーザーを引き込むチャネルを見つけることは重要ですが、それらの紹介は全体としてどの程度価値があるのでしょうか。 このレポートには、特定の獲得ソースからのユーザーの平均生涯売上高が経時的に表示されます。 つまり、これにより、特定のソースから取得したユーザーが、別のソースから取得したユーザーのグループよりも、生涯にわたってあなたと一緒に過ごすかどうかを確認できます。

このレポートをReport Builderで作成するには、 **平均生涯売上高** レポートに対する指標。 次に、以下の手順を実行します。

1. を [!UICONTROL Time Period] 分析する期間。
1. を [!UICONTROL Interval] を毎月に更新します。
   [!UICONTROL Group By] 取得元（または参照元）に追加し、追加する取得元を選択します。
1. この例では、を使用します `line chart` タイプ。

次のチュートリアルを視覚的に示します。

![ユーザーソース別の平均生涯売上高の作成](../../assets/Lifetime_revenue_by_user_source.gif).

この例では生涯売上高のみを見ていますが、この分析をレプリケートしてを確認することもできます [!UICONTROL Number of orders] または [!UICONTROL Distinct buyers] 参照元による。

## ユーザーソース別の平均注文値 {#avgorderval}

特定の獲得ソースからユーザーが費やした金額をより正確に把握するために、平均注文額を調べるレポートを作成できます。 これにより、特定のソースから取得されたユーザーが、別のソースのユーザーよりも注文あたりの支出が多いかどうかを追跡できます。

このレポートをReport Builderで作成するには、 **平均注文値** 次に、指標を使用して以下を行います。

1. を [!UICONTROL Time Period] を分析する登録期間に変更します。
1. を [!UICONTROL Time Interval] を毎月に更新します。
1. を設定 [!UICONTROL Group By] 取得元（または参照元）に追加し、追加する取得元を選択します。
1. この例では、を使用します **積み重ね列** グラフタイプ。

次のチュートリアルを視覚的に示します。

![ユーザー・ソース別平均受注値レポートの作成。](../../assets/Average_order_value_by_source.gif)

## ユーザー登録日およびソース別の合計売上高 {#revbyregdateandsource}

以前に説明した生涯売上高分析では、様々なソースから取得したユーザーの平均生涯売上高を見ることができますが、総生涯売上高についてはどうでしょうか。 このレポートを使用すると、特定の時間に、特定のソースから登録されたユーザーが生成した全体的な売上高を特定できます。

このレポートをReport Builderで作成するには、 `Revenue by user registration date` 指標。 まだインストールしていない場合は、 [がこの指標を作成しました](../../data-user/reports/ess-manage-data-metrics.md) 既に、をレプリケートすることで実行できます `Revenue` 指標と変更 `time stamp` 宛先ユーザー `creation date`. 指標を追加した後、次の操作を行います。

1. を [!UICONTROL Time Period] を分析する登録期間に変更します。
1. を [!UICONTROL Time Interval] を毎月に更新します。
1. を設定 [!UICONTROL Group By] 取得元（または参照元）に追加し、追加する取得元を選択します。
1. この例では、を使用します `stacked columns` グラフタイプ。

次のチュートリアルを視覚的に示します。

![ユーザー登録日およびソース別の合計売上高レポートの作成。](../../assets/Revenue_by_user_registration_date_and_source.gif)

## 繰り返し注文（ユーザーソース別） {#repeatordersbysource}

平均注文額レポートには、注文を行うときに特定のソースから取得したユーザー数が平均して表示されます。 ただし、同じユーザーがリピート顧客の場合、このレポートは表示しません。 しかし、ユーザー別のリピート注文ソースを使用すると、特定のソースのユーザーがリピート購入を多くまたは少なくしているかどうかを確認できます。

でレポートを作成するには [Report Builder](../../tutorials/using-visual-report-builder.md)、を追加します **注文数** 次に、指標を使用して以下を行います。

1. を [!UICONTROL Time Period] を分析する登録期間に変更します。
1. を [!UICONTROL Time Interval] を毎月に更新します。
1. を追加 [!UICONTROL filter] これにより、リピート注文のあるユーザーのみが含まれます。

   ユーザーの注文番号が 1 より大きい

1. を設定 [!UICONTROL Group By] 取得元（または参照元）に追加し、追加する取得元を選択します。
1. この例では、を使用します `stacked columns` グラフタイプ。

次のチュートリアルを視覚的に示します。

![ユーザー・ソース別リピート受注レポートの作成。](../../assets/Repeat_orders_by_user_source.gif)


## まとめ {#wrapup}

このトピックでは、獲得チャネルとマーケティングチャネルの価値を分析するために使用できるいくつかの分析に触れましたが、これは氷山の先端にすぎません。

## 関連 {#related}

* [を介した注文のリファラルソースのトラッキング [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [の接続 [!DNL Google Adwords] アカウント](../importing-data/integrations/google-adwords.md)
* [ビルド [!DNL Google ECommerce] 注文および顧客データを含むディメンション](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [での UTM タグ付けのベストプラクティス [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
