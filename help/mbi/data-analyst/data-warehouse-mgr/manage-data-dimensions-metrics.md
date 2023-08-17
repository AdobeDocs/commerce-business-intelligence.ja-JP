---
title: データディメンションの管理
description: ディメンションとは何かを説明し、指標に基づいてグラフのフィルタリングやセグメント化に使用できます。
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

ディメンションは、指標と同じテーブル内のフィールドで、その指標に基づいてグラフのフィルタリングやセグメント化に使用できます。 例えば、売上高指標には、市区町村、都道府県、国、注文のステータス、クーポンコード、その他のタイプのディメンションを含めることができます。

## 複数の指標へのディメンションの追加

1 つ以上のディメンションを複数の指標に一度に追加するには：

1. に移動します。 **[!UICONTROL Manage Data > Metrics]**.

1. クリック **[!UICONTROL Add Dimensions To Metric(s)]**.

1. ディメンションを含むテーブルを選択します。

1. Adobe Analytics の `Choose Metric(s) to Add Dimensions` 列で、ディメンションを追加する指標を選択します。 選択した後、 `Choose Dimensions to Add` 列が右側に表示されます。 選択した指標に追加するディメンションを確認します。

   ![](../../assets/Add_Dimensions.png)

1. レポート上の任意のデータディメンションでセグメント化またはグループ化する場合は、次のように指定します。 _グループ化可能_.

1. クリック **[!UICONTROL Add]**.

## 複数の指標からのディメンションの削除

複数の指標から 1 つ以上のディメンションを削除するには：

1. に移動します。 **[!UICONTROL Data > Metrics]**.

1. クリック **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. ディメンションを含むテーブルを選択します。

1. 左側のディメンションから削除する指標と、右側のディメンションを選択します。

1. クリック **[!UICONTROL Remove]**.

1. ディメンションがレポートで使用中の場合は、警告が表示され、ディメンションを使用しているグラフのリストが表示されます。 クリック **[!UICONTROL Delete]** ：チェック済みのディメンションとすべての依存（レポートを含む）を削除します。

## 指標でのディメンションの管理

**指標にディメンションを追加するには：**

1. に移動します。 **[!UICONTROL Data > Metrics]**.

1. クリック **[!UICONTROL Edit]** 新しいディメンションを追加する指標です。

1. Adobe Analytics の `Dimensions` セクションで、 `Add a dimension` 追加するディメンションを選択するドロップダウン。

>[!NOTE]
>
>フィルターまたはグループ化に使用するディメンションは、で既に追跡されている必要があります。 [!DNL Commerce Intelligence]. 目的のディメンションが見つからない場合は、データベースで、 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) ページに貼り付けます。


**指標からディメンションを削除するには：**

1. に移動します。 **[!UICONTROL Manage Data > Metrics]**.

1. クリック **[!UICONTROL Edit]** 新しいディメンションを追加する指標です。

1. の下 `Dimensions` セクションで、削除するディメンションの横にある削除列のチェックボックスをオンにします。

>[!NOTE]
>
>ディメンションを削除しても、そのディメンションはData Warehouseのテーブルの列として存在します。 任意の指標にその指標を再度追加し、これらのディメンションを使用して新しい指標を作成できます。 ディメンションが対応するデータ列をから削除するには [!DNL Commerce Intelligence]を使用する場合は、 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) ページに貼り付けます。

## 関連ドキュメント

* [セグメント化とフィルタリングのベストプラクティス](../../best-practices/segment-filter.md)
