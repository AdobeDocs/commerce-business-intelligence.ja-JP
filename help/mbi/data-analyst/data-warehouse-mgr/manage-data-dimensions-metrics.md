---
title: データディメンションの管理
description: ディメンションとは何かを説明し、指標に基づいてグラフをフィルタリングしたりセグメント化したりするために使用できます。
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# データディメンションの管理

>[!NOTE]
>
>[ 管理者権限 ](../../administrator/user-management/user-management.md) が必要です。

ディメンションとは、指標と同じテーブル内のフィールドであり、その指標に基づいてグラフをフィルタリングまたはセグメント化するために使用できます。 例えば、売上高指標には、市区町村、都道府県、国、注文ステータス、クーポンコード、その他のタイプのディメンションが含まれることがあります。

## 複数の指標へのディメンションの追加

一度に 1 つ以上のディメンションを複数の指標に追加するには：

1. **[!UICONTROL Manage Data > Metrics]** に移動します。

1. 「**[!UICONTROL Add Dimensions To Metric(s)]**」をクリックします。

1. ディメンションを含むテーブルを選択します。

1. `Choose Metric(s) to Add Dimensions` 列で、ディメンションを追加する指標を選択します。 選択すると、右側に `Choose Dimensions to Add` 列が表示されます。 選択した指標に追加するディメンションを確認します。

   ![](../../assets/Add_Dimensions.png)

1. レポートのいずれかのデータディメンションでセグメント化またはグループ化する場合は、それらが _グループ化可能_ であることを確認します。

1. 「**[!UICONTROL Add]**」をクリックします。

## 複数の指標からのディメンションの削除

複数の指標から 1 つ以上のディメンションを削除するには：

1. **[!UICONTROL Data > Metrics]** に移動します。

1. 「**[!UICONTROL Remove Dimensions From Metric(s)]**」をクリックします。

1. ディメンションを含むテーブルを選択します。

1. ディメンションを削除する指標を左側で、ディメンションを削除する指標を右側で選択します。

1. 「**[!UICONTROL Remove]**」をクリックします。

1. ディメンションがレポートで使用されている場合、そのディメンションを使用しているグラフのリストを示す警告が表示されます。 「**[!UICONTROL Delete]**」をクリックすると、チェックされたディメンションとそのすべての依存（レポートを含む）が削除されます。

## 指標でのディメンションの管理

**指標にディメンションを追加するには：**

1. **[!UICONTROL Data > Metrics]** に移動します。

1. 新し **[!UICONTROL Edit]** ディメンションを追加する指標をクリックします。

1. 「`Dimensions`」セクションで、「`Add a dimension`」ドロップダウンを使用して、追加するディメンションを選択します。

>[!NOTE]
>
>フィルターまたはグループ化の基準にするディメンションは、既に [!DNL Commerce Intelligence] で追跡されている必要があります。 目的のディメンションが見つからない場合は、[Data Warehouse](../data-warehouse-mgr/tour-dwm.md) ページからデータベースの新しいデータ列のトラッキングを開始する必要がある場合があります。


**指標からディメンションを削除するには：**

1. **[!UICONTROL Manage Data > Metrics]** に移動します。

1. 新し **[!UICONTROL Edit]** ディメンションを追加する指標をクリックします。

1. 「`Dimensions`」セクションで、削除するディメンションの横にある削除列のチェックボックスを選択します。

>[!NOTE]
>
>ディメンションを削除した後も、そのディメンションはData Warehouse内のテーブルの列として存在します。 任意の指標に追加し直して、これらのディメンションを使用して新しい指標を作成できます。 ディメンションが対応するデータ列を [!DNL Commerce Intelligence] から削除するには、[Data Warehouse](../data-warehouse-mgr/tour-dwm.md) ページでデータ列のトラックを解除します。

## 関連ドキュメント

* [セグメント化とフィルタリングのベストプラクティス](../../best-practices/segment-filter.md)
