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
>が必要 [管理者権限](../../administrator/user-management/user-management.md).

ディメンションとは、指標と同じテーブル内のフィールドであり、その指標に基づいてグラフをフィルタリングまたはセグメント化するために使用できます。 例えば、売上高指標には、市区町村、都道府県、国、注文ステータス、クーポンコード、その他のタイプのディメンションが含まれることがあります。

## 複数の指標へのディメンションの追加

一度に 1 つ以上のディメンションを複数の指標に追加するには：

1. に移動 **[!UICONTROL Manage Data > Metrics]**.

1. クリック **[!UICONTROL Add Dimensions To Metric(s)]**.

1. ディメンションを含むテーブルを選択します。

1. が含まれる `Choose Metric(s) to Add Dimensions` 列で、ディメンションを追加する指標を選択します。 選択すると、 `Choose Dimensions to Add` 列が右側に表示されます。 選択した指標に追加するディメンションを確認します。

   ![](../../assets/Add_Dimensions.png)

1. レポートのいずれかのデータディメンションでセグメント化またはグループ化する場合は、次の点を確認します _Groupable_.

1. クリック **[!UICONTROL Add]**.

## 複数の指標からのディメンションの削除

複数の指標から 1 つ以上のディメンションを削除するには：

1. に移動 **[!UICONTROL Data > Metrics]**.

1. クリック **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. ディメンションを含むテーブルを選択します。

1. ディメンションを削除する指標を左側で、ディメンションを削除する指標を右側で選択します。

1. クリック **[!UICONTROL Remove]**.

1. ディメンションがレポートで使用されている場合、そのディメンションを使用しているグラフのリストを示す警告が表示されます。 クリック **[!UICONTROL Delete]** チェックされたディメンションとそのすべての依存（レポートを含む）を削除します。

## 指標でのディメンションの管理

**指標にディメンションを追加するには：**

1. に移動 **[!UICONTROL Data > Metrics]**.

1. クリック **[!UICONTROL Edit]** 新しいディメンションが必要な指標で。

1. が含まれる `Dimensions` セクションで、 `Add a dimension` 追加するディメンションをドロップダウンから選択します。

>[!NOTE]
>
>フィルターまたはグループ化の基準にするディメンションは、既にで追跡する必要があります [!DNL Commerce Intelligence]. 目的のディメンションが見つからない場合は、を使用して、データベース内の新しいデータ列のトラッキングを開始する必要がある場合があります [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) ページ。


**指標からディメンションを削除するには：**

1. に移動 **[!UICONTROL Manage Data > Metrics]**.

1. クリック **[!UICONTROL Edit]** 新しいディメンションが必要な指標で。

1. の下 `Dimensions` セクションで、削除するディメンションの横にある削除列のチェックボックスを選択します。

>[!NOTE]
>
>ディメンションを削除した後も、そのディメンションはData Warehouse内のテーブルの列として存在します。 任意の指標に追加し直して、これらのディメンションを使用して新しい指標を作成できます。 ディメンションが対応するデータ列をから削除するには、次の手順に従います [!DNL Commerce Intelligence]を使用してデータ列のトラックを解除するだけです。 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) ページ。

## 関連ドキュメント

* [セグメント化とフィルタリングのベストプラクティス](../../best-practices/segment-filter.md)
