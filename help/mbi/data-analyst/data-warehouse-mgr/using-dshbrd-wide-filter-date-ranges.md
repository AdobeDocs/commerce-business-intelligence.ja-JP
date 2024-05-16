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

ダッシュボードの日付範囲またはレポートの間隔を変更するには、右上隅にあるカレンダーアイコン（![カレンダー](../../assets/calendar-button.png)）に設定します。

を使用してデータを表示するように選択できます `Fixed Date Range` またはさまざまな事前計算済み `Moving Date Ranges`:

![日付範囲の移動](../../assets/moving_date_ranges.png)

この `Last Full...` 移動範囲オプションは、最後に完了した範囲を表し、一方で `This...` は、現在の進行中の範囲です。 例えば、6 月の場合 `Last Full Month` 等しい _5 月 1 日～5 月 31 日_、間 `This Month` 等しい _6 月 1 日（PT） – 今_.

または独自に作成 `Custom Moving Range`\:

![カスタム移動範囲](../../assets/custom-moving-range.png)

を選択して、間隔も変更します。 デフォルトボタンの選択（![時間間隔の既定値](../../assets/time_interval_default.png)）は、日付範囲のみが変更されることを意味します。

![時間間隔](../../assets/time_interval.png)

すべてのレポートを初期の日付範囲および間隔に復元するには、をクリックします **[!UICONTROL Restore Defaults]** またはクリック **[!UICONTROL Cancel]**.

ダッシュボードに日付フィルターを指定すると、そのフィルターはそのダッシュボードにのみ適用されます。 他のダッシュボードに移動する場合は適用されません。

>[!NOTE]
>
>現在、 `Cohort Reports` および `SQL Reports` ダッシュボードレベルで変更を適用する場合は、が含まれません。

## フィルターの保存

特定のストアのパフォーマンスを分析するには、右上隅にあるストアアイコン（![フィルターの保存](../../assets/store-filter.png)）に設定します。 デフォルトでは `Store Filter` はに設定されています。 `All Stores`。すべてのデータが表示されます。 [ビューを保存](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) Commerce サイトで使用できます。

>[!NOTE]
>
>ストアフィルターは全体に対して有効または無効になっています [!DNL Commerce Intelligence] アカウント。 ダッシュボードに、フィルターの影響を受けないレポートが含まれている場合（どのレポートにも基づいていないレポートなど） [!DNL Adobe Commerce] data）に設定した場合、これらのレポートは、ストアフィルターが適用される際に更新されません。 次のことができます [サポートに連絡する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) ストアの選択に基づいてレポートを更新する必要があると思われる場合、またはアカウントストアのフィルターが誤って無効になっていると思われる場合。

からストアを選択した場合 `Store Filter`の場合、ダッシュボード間を移動しても、フィルターは選択内容を保持します。 選択を保持すると、を選択するまで、選択したストアのデータをどこにでも表示できます `All Stores`.

## 共有ダッシュボードのフィルター

共有ダッシュボードの場合、1 人のユーザーが日付フィルターを設定すると、ダッシュボードにアクセスできる他のユーザーには、同じフィルターが適用されます。 ただし、この場合、ストアフィルターは適用されません。 ダッシュボードの所有者がストアフィルターを設定してダッシュボードを共有すると、設定されたストアフィルターは別のユーザーには保持されません。 ユーザーの条件 [アクセスを編集](../../data-user/dashboards/share-dashboard-with-users.md) をダッシュボードに移動して、ダッシュボードフィルターを調整します。
