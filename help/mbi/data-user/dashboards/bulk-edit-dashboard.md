---
title: ダッシュボードでのチャートの一括編集
description: ' [!DNL Commerce Intelligence]の一括編集機能の使用方法を説明します。'
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/FcFTKq9TvldFwo7nl-bGRyup1uxscjrnOutJcA-h-5c
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
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 260
ht-degree: 0%

---

# ダッシュボードでのチャートの一括編集

一括編集機能を使用すると、ダッシュボードでグラフの名前と日付を簡単に変更できます。 たとえば、特定のダッシュボードのすべてのチャートで、四半期ではなく月単位で、単一のストアとレポートを参照するように設定します。 すべてを手動で変更するのではなく、`bulk-editing`機能で作業します。 このトピックでは、次の使用方法について説明します。

* [&#x200B; [!DNL Find/Replace] 機能](#findreplace)

* [&#x200B; [!DNL Prepend Name] 機能](#prepend)

* [&#x200B; [!DNL Change Dates] 機能](#dates)

ただし、このことを考慮してください – *これらの変更は永続的である必要がありますか？*&#x200B;そうでない場合は、ダッシュボードを複製してから、新しいダッシュボードの日付を変更することを検討してください。 これにより、必要な変更を行いながら、元のダッシュボードを保持できます。

>[!NOTE]
>
>多数のレポートを変更する場合、更新プロセスに時間がかかる場合があります。

## [!DNL Find/Replace]の使用中 {#findreplace}

1. ダッシュボード名の横にある歯車（![歯車アイコン &#x200B;](../../assets/gear-icon.png)）アイコンをクリックし、[!UICONTROL Bulk Edit Reports] ウィンドウをクリックします。

1. ポップアップで「**[!UICONTROL Chart Title Find and Replace]**」をクリックします。

1. `Chart Title Find` フィールドに、検索する単語または文字を入力します。

1. `Replace With` フィールドに、`Find` フィールドの内容を置き換える単語または文字を入力します。

1. **[!UICONTROL Update Reports]**&#x200B;をクリックします。

例：

![一括編集](../../assets/bulk_edit.gif)

## `Chart Names`が保留中です {#prepend}

1. ダッシュボード名の横にある歯車（![歯車アイコン &#x200B;](../../assets/gear-icon.png)）アイコンをクリックし、[!UICONTROL Bulk Edit Reports] ウィンドウをクリックします。

1. ポップアップで「**[!UICONTROL Prepend Report Names]**」をクリックします。

1. グラフの前に付ける単語または文字を入力します。

1. **[!UICONTROL Update Reports]**&#x200B;をクリックします。

例：

![prepend](../../assets/prepend.gif)

## `Dates`を変更中 {#dates}

1. ダッシュボード名の横にある歯車（![歯車アイコン &#x200B;](../../assets/gear-icon.png)）アイコンをクリックし、[!UICONTROL Bulk Edit Reports] ウィンドウを選択します。

1. ポップアップウィンドウで「**[!UICONTROL Change Dates]**」をクリックします。

1. 新しい`Start/End Date`と`Time Interval`を設定します。 これらのフィールドは変更しないでください。

1. **[!UICONTROL Update Reports]**&#x200B;をクリックします。

例：

![日付の変更](../../assets/dates.gif)
