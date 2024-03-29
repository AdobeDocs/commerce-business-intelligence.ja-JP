---
title: ダッシュボード全体のフィルタリング
description: 特定のダッシュボードですべてのレポートを一括編集する方法を説明します。
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# ダッシュボード全体のフィルタリング

ダッシュボード全体のフィルタリングを使用すると、特定のダッシュボードですべてのレポートの一括編集をおこなうことができます。 異なる期間や異なる店舗で、同じ分析をすばやく表示できます。 前の年、月、または週の各店舗のパフォーマンスを簡単に比較できます。 新しく起動したキャンペーンに合わせてダッシュボード全体を更新できます。

## 日付フィルター

ダッシュボードのレポートの日付範囲や間隔を変更するには、右上隅にあるカレンダーアイコン (![カレンダー](../../assets/calendar-button.png)) をクリックします。

データの表示は、 `Fixed Date Range` または様々な事前計算済み `Moving Date Ranges`:

![日付範囲の移動](../../assets/moving_date_ranges.png)

The `Last Full...` 移動範囲オプションは、最後に完了した範囲を表します。 `This...` は、現在進行中の範囲です。 例えば、6 月の場合、 `Last Full Month` 次に該当 _5 月 1 日～5 月 31 日_&#x200B;で、 `This Month` 次に該当 _6 月 1 日～今すぐ_.

または、独自の `Custom Moving Range`\:

![カスタム移動範囲](../../assets/custom-moving-range.png)

間隔の変更も選択します。 デフォルトのボタン (![時間間隔のデフォルト](../../assets/time_interval_default.png)) は、日付範囲のみが変更されることを意味します。

![時間間隔](../../assets/time_interval.png)

すべてのレポートを初期の日付範囲と間隔に戻すには、 **[!UICONTROL Restore Defaults]** または、 **[!UICONTROL Cancel]**.

ダッシュボードの日付フィルタを指定すると、そのフィルタはそのダッシュボードにのみ適用されます。 他のダッシュボードに移動しても、適用されません。

>[!NOTE]
>
>現在、 `Cohort Reports` および `SQL Reports` ダッシュボードレベルで変更を適用する際には、が含まれません。

## ストアフィルター

特定のストアのパフォーマンスを分析するには、右上隅にあるストアアイコン (![ストアフィルター](../../assets/store-filter.png)) をクリックします。 デフォルトでは、 `Store Filter` が `All Stores`：すべての [ストア表示](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) コマースサイトで使用できます。

>[!NOTE]
>
>ストアフィルターは、 [!DNL Commerce Intelligence] アカウント。 フィルタの影響を受けないレポート ( [!DNL Adobe Commerce] データなど ) が含まれる場合、これらのレポートは、ストアフィルターが適用されても更新されません。 以下が可能です。 [連絡先サポート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) ストアの選択に基づいてレポートを更新すると思われる場合や、アカウントストアのフィルターが誤って無効になっていると思われる場合。

次の場所からストアを選択すると、 `Store Filter`を使用すると、ダッシュボード間を移動する際にフィルターで選択内容が保持されます。 選択を維持すると、選択したストアのデータを、選択した `All Stores`.

## 共有ダッシュボードのフィルター

共有ダッシュボードの場合、あるユーザーが日付フィルターを設定すると、そのダッシュボードへのアクセス権を持つ他のユーザーに同じフィルターが適用されて表示されます。 ただし、この場合、ストアフィルターは適用されません。 ダッシュボードの所有者がストアフィルターを設定し、ダッシュボードを共有した場合、設定されたストアフィルターは別のユーザーに対して保持されません。 ユーザーが [アクセスを編集](../../data-user/dashboards/share-dashboard-with-users.md) をダッシュボードに追加して、ダッシュボードのフィルターを調整します。
