---
title: 最も価値のあるマーケティングソースとチャネルの特定
description: 最も価値の高いマーケティングチャネルを明らかにするために使用できるレポートの一部について説明します。
exl-id: 8d25bc80-ea60-47db-b01b-04a23a24c14d
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '978'
ht-degree: 0%

---

# 成功したマーケティングソースの特定

オーディエンスを調べ、キャンペーンを作り、いくつかのマーケティングチャネルに投資しました。 しばらく経った今、これらのチャネルはどのように動いているのでしょうか？ 最も新しいユーザーを導いたチャネルは何ですか？ 合計売上高に最も貢献したのは、どのソースですか？

を使用 [!DNL Adobe Commerce Intelligence]を使用すると、リファラルソース ( [!DNL [Google Analytics' UTM fields]](https://support.google.com/analytics/answer/1191184?hl=en) またはカスタムデータフィールド。 このセグメント化により、最もパフォーマンスの高いチャネルを見つけ、マーケティング予算に投資することができます。

このトピックでは、最も価値のあるマーケティングチャネルを明らかにするために使用できるレポートをいくつか紹介します。

* [ソース別の新規ユーザー](#newusersbysource)
* [ユーザーソース別の平均ライフタイム売上高](#avglifetimerev)
* [ユーザーソース別の平均注文額](#avgorderval)
* [ユーザー登録日およびソース別の売上高](#revbyregdateandsource)
* [ユーザーソース別に注文を繰り返す](#repeatordersbysource)

## 前提条件 {#prereqs}

このトピックの分析を作成するには、マーケティング獲得/参照元データにアクセスする必要があります。 まだ追跡していない場合は、 [紹介元のデータを注文する [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md) into [!DNL Adobe Commerce Intelligence] をクリックしてください。 また、分析にユーザーデバイス情報を追加すると、紹介で使用しているテクノロジーを確認できます。

## ソース別の新規ユーザー数 {#newusersbysource}

リファラルソースのパフォーマンスの評価は、最も価値の高いチャネルを決定する上で重要です。 このレポートは、新たに登録されたユーザーの数を、獲得ソースごとに経時的に表示します。これにより、新しく登録されたユーザーを取得する際の参照元のパフォーマンスを追跡できます。

このレポートを [Report Builder](../../tutorials/using-visual-report-builder.md)、 **新規ユーザー** 指標（または時間の経過に伴う新規ユーザー数をカウントする同等の指標）を示します。 次に、以下の手順を実行します。

1. を設定します。 [!UICONTROL Time Period] を、分析する登録期間に追加します。
1. を設定します。 [!UICONTROL Interval] から毎月
1. 設定 [!UICONTROL Group By] 獲得（または紹介）ソースを選択し、含めるソースを選択します。
1. この例では、 `stacked columns` [!UICONTROL chart type].

以下に、視覚的なガイドを示します。

![ソース別に新しいユーザーを作成します。](../../assets/New_Users_by_source.gif)

## ユーザーソース別の平均ライフタイム売上高 {#avglifetimerev}

新しいユーザーを呼び込むチャネルを見つけることは重要ですが、それらの紹介は全体的にどの程度価値があるのでしょうか。 このレポートは、特定の獲得ソースからのユーザーの平均ライフタイム売上高を経時的に表示します。 つまり、特定のソースから獲得したユーザーが、別のソースから獲得したユーザーのグループよりも、生涯にわたって多くのユーザーを費やしているかどうかを確認できます。

このレポートをReport Builderで作成するには、 **平均ライフタイム売上高** 指標をレポートに追加します。 次に、以下の手順を実行します。

1. を設定します。 [!UICONTROL Time Period] を分析する期間に追加します。
1. を設定します。 [!UICONTROL Interval] から毎月
   [!UICONTROL Group By] 獲得（または紹介）ソースを選択し、含めるソースを選択します。
1. この例では、 `line chart` タイプ。

以下に、視覚的なガイドを示します。

![ユーザーソース別の平均ライフタイム売上高の作成](../../assets/Lifetime_revenue_by_user_source.gif).

この例では、全期間の売上高のみを調べますが、この分析を複製して [!UICONTROL Number of orders] または [!UICONTROL Distinct buyers] リファラルソースによる。

## ユーザーソース別の平均注文額 {#avgorderval}

特定の獲得ソースからのユーザーの支出額をより深く把握するには、平均注文額を調べるレポートを作成します。 これにより、特定のソースから獲得したユーザーが、別のソースからのユーザーよりも注文あたりの支出を増やしているかを追跡できます。

このレポートをReport Builderで作成するには、 **平均注文額** 指標を選択し、次の操作を実行します。

1. を設定します。 [!UICONTROL Time Period] を、分析する登録期間に追加します。
1. を設定します。 [!UICONTROL Time Interval] から毎月
1. 設定 [!UICONTROL Group By] 獲得（または紹介）ソースを選択し、含めるソースを選択します。
1. この例では、 **積み重ね列** グラフのタイプ。

以下に、視覚的なガイドを示します。

![ユーザーソース別の平均注文額レポートの作成](../../assets/Average_order_value_by_source.gif)

## ユーザー登録日およびソース別の合計売上高 {#revbyregdateandsource}

先ほど説明した全期間売上高分析では、様々なソースから取得したユーザーの平均全期間売上高を調べることができますが、全期間売上高はどうなりますか？ このレポートでは、特定の期間および特定のソースから登録した全体的な売上高ユーザーが生み出す売上高を特定できます。

このレポートをReport Builderで作成するには、 `Revenue by user registration date` 指標。 次の条件を満たしていない場合、 [この指標を作成しました](../../data-user/reports/ess-manage-data-metrics.md) 既に、 `Revenue` 指標を追加して、 `time stamp` ユーザーの `creation date`. 指標を追加した後、次の操作を行います。

1. を設定します。 [!UICONTROL Time Period] を、分析する登録期間に追加します。
1. を設定します。 [!UICONTROL Time Interval] から毎月
1. 設定 [!UICONTROL Group By] 獲得（または紹介）ソースを選択し、含めるソースを選択します。
1. この例では、 `stacked columns` グラフのタイプ。

以下に、視覚的なガイドを示します。

![ユーザー登録日別合計売上高およびソースレポートの作成。](../../assets/Revenue_by_user_registration_date_and_source.gif)

## ユーザーソース別に注文を繰り返す {#repeatordersbysource}

平均注文額レポートは、注文時に特定のソースから獲得したユーザーの平均数を示します。 ただし、同じユーザーがリピーターの場合、このレポートは表示されません。 ただし、ユーザー別の注文を繰り返すソースを使用すると、特定のソースのユーザーが繰り返し購入を行うかどうかを確認できます。

このレポートを [Report Builder](../../tutorials/using-visual-report-builder.md)、 **注文数** 指標を選択し、次の操作を実行します。

1. を設定します。 [!UICONTROL Time Period] を、分析する登録期間に追加します。
1. を設定します。 [!UICONTROL Time Interval] から毎月
1. を追加します。 [!UICONTROL filter] 繰り返し注文を持つユーザーのみが含まれるように、次の手順に従います。

   1 より大きいユーザーの注文番号

1. 設定 [!UICONTROL Group By] 獲得（または紹介）ソースを選択し、含めるソースを選択します。
1. この例では、 `stacked columns` グラフのタイプ。

以下に、視覚的なガイドを示します。

![ユーザーソース別の繰り返し注文レポートの作成。](../../assets/Repeat_orders_by_user_source.gif)


## 折り返し {#wrapup}

このトピックでは、獲得やマーケティングチャネルの価値を分析するために使用できる分析をいくつか紹介しましたが、これは氷山の一角にすぎません。

## 関連 {#related}

* [経由での注文のリファラルソースのトラッキング [!DNL Google ECommerce]](../importing-data/integrations/google-ecommerce.md)
* [接続 [!DNL Google Adwords] アカウント](../importing-data/integrations/google-adwords.md)
* [建物 [!DNL Google ECommerce] 注文と顧客データを含むディメンション](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [での UTM タグ付けのベストプラクティス [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
