---
title: ダッシュボードでのグラフの一括編集
description: で一括編集機能を使用する方法を説明します [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# ダッシュボードでのグラフの一括編集

一括編集機能を使用すると、ダッシュボードのグラフの名前と日付を簡単に変更できます。 例えば、特定のダッシュボード上のすべてのグラフで、四半期ごとではなく月次ベースで 1 つのストアとレポートを参照するとします。 すべてを手動で変更するのではなく、 `bulk-editing` 機能が作業を行います。 このトピックでは、以下の使用方法を学びます。

* [この [!DNL Find/Replace] 機能](#findreplace)

* [この [!DNL Prepend Name] 機能](#prepend)

* [この [!DNL Change Dates] 機能](#dates)

とは言え、これを考慮に入れてください。 *これらの変更は永続的にする必要がありますか？* そうでない場合は、ダッシュボードを複製し、その後、新しいダッシュボードで日付を変更することを検討してください。 これにより、必要な変更を加えながら、元のダッシュボードを保持できます。

>[!NOTE]
>
>多数のレポートを変更する場合、更新プロセスには少し時間がかかる場合があります。

## 使用 [!DNL Find/Replace] {#findreplace}

1. 歯車（![](../../assets/gear-icon.png)） アイコンがダッシュボード名の隣に表示され、次に [!UICONTROL Bulk Edit Reports] ウィンドウ。

1. クリック **[!UICONTROL Chart Title Find and Replace]** ポップアップで。

1. が含まれる `Chart Title Find` フィールドに、検索する単語または文字を入力します。

1. が含まれる `Replace With` フィールドに、の内容を置き換える単語または文字を入力します `Find` フィールド。

1. クリック **[!UICONTROL Update Reports]**.

例：

![一括編集](../../assets/bulk_edit.gif)

## 先行 `Chart Names` {#prepend}

1. 歯車（![](../../assets/gear-icon.png)） アイコンがダッシュボード名の隣に表示され、次に [!UICONTROL Bulk Edit Reports] ウィンドウ。

1. クリック **[!UICONTROL Prepend Report Names]** ポップアップで。

1. グラフの前に付ける単語または文字を入力します。

1. クリック **[!UICONTROL Update Reports]**.

例：

![先頭に付加](../../assets/prepend.gif)

## 変更中 `Dates` {#dates}

1. 歯車（![](../../assets/gear-icon.png)） アイコンをクリックしてから、ダッシュボード名の横にある [!UICONTROL Bulk Edit Reports] ウィンドウ。

1. クリック **[!UICONTROL Change Dates]** ポップアップウィンドウで調整します。

1. 新しい `Start/End Date` および `Time Interval`. これらのフィールドは変更しないでください。

1. クリック **[!UICONTROL Update Reports]**.

例：

![日付の変更](../../assets/dates.gif)
