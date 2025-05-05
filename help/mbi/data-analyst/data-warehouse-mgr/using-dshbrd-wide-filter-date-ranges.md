---
title: ダッシュボード全体のフィルタリング
description: 特定のダッシュボードですべてのレポートを一括編集する方法を説明します。
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# ダッシュボード全体のフィルタリング

ダッシュボード全体のフィルタリングを使用すると、特定のダッシュボード上のすべてのレポートを一括編集できます。 同じ分析を異なる期間や店舗ですばやく確認できます。 ストアごとに前年、月、週のパフォーマンスを簡単に比較できます。 ダッシュボード全体を更新して、新しく開始されたキャンペーンに対応できます。

## 日付フィルター

ダッシュボードの日付範囲またはレポートの間隔を変更するには、右上隅にあるカレンダーアイコン（![calendar](../../assets/calendar-button.png)）をクリックします。

`Fixed Date Range` ールまたは様々な事前計算された `Moving Date Ranges` を使用して、データを表示するよう選択できます。

![ 日付範囲の移動 ](../../assets/moving_date_ranges.png)

`Last Full...` の移動範囲オプションは、最後に完了した範囲を表し、`This...` は現在の進行中の範囲です。 例えば、6 月の場合、`Last Full Month` は _5 月 1 日から 5 月 31 日_、`This Month` は _6 月 1 日から現在_ になります。

または独自の `Custom Moving Range` を作成\:

![ カスタム移動範囲 ](../../assets/custom-moving-range.png)

を選択して、間隔も変更します。 デフォルトのボタン（![ 時間間隔のデフォルト ](../../assets/time_interval_default.png)）を選択すると、日付範囲のみが変更されます。

![ 時間間隔 ](../../assets/time_interval.png)

すべてのレポートを初期の日付範囲および間隔に復元するには、「**[!UICONTROL Restore Defaults]**」または「**[!UICONTROL Cancel]**」をクリックします。

ダッシュボードに日付フィルターを指定すると、そのフィルターはそのダッシュボードにのみ適用されます。 他のダッシュボードに移動する場合は適用されません。

>[!NOTE]
>
>現在、ダッシュボードレベルで変更を適用する場合、`Cohort Reports` と `SQL Reports` は含まれません。

## フィルターの保存

特定のストアのパフォーマンスを分析するには、右上隅にあるストアアイコン（![ ストアフィルター ](../../assets/store-filter.png)）をクリックします。 デフォルトでは、`Store Filter` は `All Stores` に設定されており、Commerce サイトで使用可能なすべての [ ストア表示 ](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html?lang=ja) からのデータが表示されます。

>[!NOTE]
>
>ストアフィルターは、[!DNL Commerce Intelligence] アカウント全体で有効または無効になります。 ダッシュボードにフィルターの影響を受けないレポート（[!DNL Adobe Commerce] のデータに基づいていないレポートなど）が含まれている場合、ストアフィルターを適用してもそれらのレポートは更新されません。 ストアの選択に基づいてレポートを更新する必要があると思われる場合、またはアカウントストアのフィルターが誤って無効になっていると思われる場合は、[ サポートにお問い合わせください ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)。

ダッシュボードからストアを選択しても、ダッ `Store Filter` ボード間を移動する際は、選択内容がフィルターに保持されます。 選択を保持すると、`All Stores` を選択するまで、選択したストアのデータをどこにでも表示できます。

## 共有ダッシュボードのフィルター

共有ダッシュボードの場合、1 人のユーザーが日付フィルターを設定すると、ダッシュボードにアクセスできる他のユーザーには、同じフィルターが適用されます。 ただし、この場合、ストアフィルターは適用されません。 ダッシュボードの所有者がストアフィルターを設定してダッシュボードを共有すると、設定されたストアフィルターは別のユーザーには保持されません。 ダッシュボードフィルターを調整するには、ユーザーがダッシュボードに [ 編集アクセス ](../../data-user/dashboards/share-dashboard-with-users.md) できる必要があります。
