---
title: ダッシュボード全体のフィルタリング
description: 特定のダッシュボードですべてのレポートを一括編集する方法について説明します。
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/6wixrQXkvGMF9c36wrGJ4Qj23HqJ--Mr0XMYMBhujjo
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 0%

---

# ダッシュボード全体のフィルタリング

ダッシュボード全体のフィルタリングを使用すると、特定のダッシュボード上のすべてのレポートを一括編集できます。 異なる期間にわたって、または異なるストアに対して、同じ分析をすばやく表示できます。 店舗ごとの前年、月、週のパフォーマンスを簡単に比較できます。 新しく開始されたキャンペーンに対応するために、ダッシュボード全体を更新できます。

## 日付フィルター

ダッシュボード上のレポートの日付範囲または間隔を変更するには、右上隅（![&#x200B; カレンダー](../../assets/calendar-button.png)）のカレンダーアイコンをクリックします。

`Fixed Date Range`または事前計算されたさまざまな`Moving Date Ranges`を使用してデータを表示できます。

![日付範囲を移動](../../assets/moving_date_ranges.png)

`Last Full...`移動範囲オプションは、最近完了した範囲を表し、`This...`は現在の進行中の範囲です。 例えば、6月の場合、`Last Full Month`は&#x200B;_5月1日～5月31_&#x200B;で、`This Month`は&#x200B;_6月1日～現在_&#x200B;です。

または、独自の`Custom Moving Range`\:

![&#x200B; カスタム移動範囲](../../assets/custom-moving-range.png)

間隔も変更できます。 デフォルトのボタン（![時間間隔のデフォルト &#x200B;](../../assets/time_interval_default.png)）を選択すると、日付範囲のみが変更されます。

![時間間隔](../../assets/time_interval.png)

すべてのレポートを初期の日付範囲と間隔に戻すには、**[!UICONTROL Restore Defaults]**&#x200B;をクリックするか、**[!UICONTROL Cancel]**&#x200B;をクリックします。

ダッシュボードの日付フィルターを指定すると、そのフィルターはそのダッシュボードにのみ適用されます。 他のダッシュボードに移動する場合は適用されません。

>[!NOTE]
>
>現在、`Cohort Reports`と`SQL Reports`は、ダッシュボードレベルで変更を適用する際には含まれていません。

## フィルターを保存

特定のストアのパフォーマンスを分析するには、右上隅のストアアイコン（![&#x200B; ストアフィルター](../../assets/store-filter.png)）をクリックします。 デフォルトでは、`Store Filter`は`All Stores`に設定されており、Commerce サイトで利用可能なすべての[&#x200B; ストアビュー](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html?lang=ja)のデータが表示されます。

>[!NOTE]
>
>[!DNL Commerce Intelligence] アカウント全体でストアフィルターが有効または無効になっています。 ダッシュボードに、フィルターの影響を受けないレポート （どの[!DNL Adobe Commerce] データにも組み込まれていないレポートなど）が含まれている場合、ストアフィルターが適用されたときに、これらのレポートは更新されません。 ストアの選択に基づいてレポートを更新する必要があると思われる場合、またはアカウント ストア フィルターが誤って無効になっていると思われる場合は、[&#x200B; サポート &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)にお問い合わせください。

`Store Filter`からストアを選択すると、ダッシュボード間を移動する際に、フィルターは選択内容を保持します。 選択範囲を保持すると、`All Stores`を選択するまで、選択したストアのデータをどこにでも表示できます。

## 共有ダッシュボードのフィルター

共有ダッシュボードの場合、1人のユーザーが日付フィルターを設定すると、ダッシュボードへのアクセス権を持つ他のユーザーに同じフィルターが適用されます。 ただし、この場合、ストアフィルターは適用されません。 ダッシュボードの所有者がストアフィルターを設定し、ダッシュボードを共有する場合、設定されたストアフィルターは別のユーザーに保持されません。 ダッシュボードフィルターを調整するには、ユーザーにダッシュボードへの[編集アクセス &#x200B;](../../data-user/dashboards/share-dashboard-with-users.md)が必要です。
