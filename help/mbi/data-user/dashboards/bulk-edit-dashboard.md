---
title: ダッシュボードでのグラフの一括編集
description: ' [!DNL Commerce Intelligence] で一括編集機能を使用する方法について説明します。'
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# ダッシュボードでのグラフの一括編集

一括編集機能を使用すると、ダッシュボードのグラフの名前と日付を簡単に変更できます。 例えば、特定のダッシュボード上のすべてのグラフで、四半期ごとではなく月次ベースで 1 つのストアとレポートを参照するとします。 すべてを手動で変更するのではなく、`bulk-editing` 機能で作業を行います。 このトピックでは、以下の使用方法を学びます。

* [ [!DNL Find/Replace]  機能](#findreplace)

* [ [!DNL Prepend Name]  機能](#prepend)

* [ [!DNL Change Dates]  機能](#dates)

ただし、次の点を考慮してください。*これらの変更は永続的である必要がありますか？* そうでない場合は、ダッシュボードを複製してから、新しいダッシュボードで日付を変更することを検討してください。 これにより、必要な変更を加えながら、元のダッシュボードを保持できます。

>[!NOTE]
>
>多数のレポートを変更する場合、更新プロセスには少し時間がかかる場合があります。

## [!DNL Find/Replace] の使用 {#findreplace}

1. ダッシュボード名の横にある歯車（![ 歯車アイコン ](../../assets/gear-icon.png)）アイコンをクリックし、[!UICONTROL Bulk Edit Reports] ウィンドウをクリックします。

1. ポップアップの **[!UICONTROL Chart Title Find and Replace]** をクリックします。

1. `Chart Title Find` フィールドに、検索する単語または文字を入力します。

1. `Replace With` フィールドに、`Find` フィールドの内容を置き換える単語または文字を入力します。

1. 「**[!UICONTROL Update Reports]**」をクリックします。

例：

![ 一括編集 ](../../assets/bulk_edit.gif)

## 先行 `Chart Names` {#prepend}

1. ダッシュボード名の横にある歯車（![ 歯車アイコン ](../../assets/gear-icon.png)）アイコンをクリックし、[!UICONTROL Bulk Edit Reports] ウィンドウをクリックします。

1. ポップアップの **[!UICONTROL Prepend Report Names]** をクリックします。

1. グラフの前に付ける単語または文字を入力します。

1. 「**[!UICONTROL Update Reports]**」をクリックします。

例：

![ 先頭に付加 ](../../assets/prepend.gif)

## `Dates` の変更 {#dates}

1. ダッシュボード名の横にある歯車（![ 歯車アイコン ](../../assets/gear-icon.png)）アイコンをクリックし、[!UICONTROL Bulk Edit Reports] ウィンドウを選択します。

1. ポップアップウィンドウで「**[!UICONTROL Change Dates]**」をクリックします。

1. 新しい `Start/End Date` と `Time Interval` を設定します。 これらのフィールドは変更しないでください。

1. 「**[!UICONTROL Update Reports]**」をクリックします。

例：

![ 日付変更 ](../../assets/dates.gif)
