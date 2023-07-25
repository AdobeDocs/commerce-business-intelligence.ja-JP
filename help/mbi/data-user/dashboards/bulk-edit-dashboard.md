---
title: ダッシュボードでのグラフの一括編集
description: の一括編集機能の使用方法を説明します。 [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# ダッシュボードでのグラフの一括編集

一括編集機能を使用すると、ダッシュボードでグラフの名前や日付を簡単に変更できます。 例えば、特定のダッシュボード上のすべてのグラフで、四半期ごとではなく、1 つの店舗を参照し、月単位でレポートを作成するとします。 すべてを手動で変更するのではなく、 `bulk-editing` 機能を使用して作業を行います。 このトピックでは、以下の使用方法を学びます。

* [この [!DNL Find/Replace] 機能](#findreplace)

* [この [!DNL Prepend Name] 機能](#prepend)

* [この [!DNL Change Dates] 機能](#dates)

とはいえ、この点を考えてみましょう。 *これらの変更は永続的に行う必要がありますか？* そうでない場合は、ダッシュボードのクローンを作成し、新しいダッシュボードで日付を変更することを検討してください。 これにより、元のダッシュボードを保持したまま、必要な変更を加えることができます。

>[!NOTE]
>
>多数のレポートを変更する場合は、更新プロセスに少し時間がかかる可能性があります。

## 使用 [!DNL Find/Replace] {#findreplace}

1. 歯車 (![](../../assets/gear-icon.png)) アイコンをクリックし、 [!UICONTROL Bulk Edit Reports] ウィンドウ

1. クリック **[!UICONTROL Chart Title Find and Replace]** を選択します。

1. 内 `Chart Title Find` フィールドに、検索する単語または文字を入力します。

1. 内 `Replace With` フィールドに、 `Find` フィールドに入力します。

1. クリック **[!UICONTROL Update Reports]**.

例：

![一括編集](../../assets/bulk_edit.gif)

## 保留中 `Chart Names` {#prepend}

1. 歯車 (![](../../assets/gear-icon.png)) アイコンをクリックし、 [!UICONTROL Bulk Edit Reports] ウィンドウ

1. クリック **[!UICONTROL Prepend Report Names]** を選択します。

1. グラフの前に付ける単語または文字を入力します。

1. クリック **[!UICONTROL Update Reports]**.

例：

![前付け](../../assets/prepend.gif)

## 変更 `Dates` {#dates}

1. 歯車 (![](../../assets/gear-icon.png)) アイコンをクリックし、 [!UICONTROL Bulk Edit Reports] ウィンドウ

1. クリック **[!UICONTROL Change Dates]** をクリックします。

1. 新しい `Start/End Date` および `Time Interval`. これらのフィールドは変更しないでおくこともできます。

1. クリック **[!UICONTROL Update Reports]**.

例：

![変更日](../../assets/dates.gif)
