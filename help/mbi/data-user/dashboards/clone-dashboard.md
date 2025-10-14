---
title: ダッシュボードの複製
description: ダッシュボードの複製方法を説明します。
exl-id: f0bfa786-ab01-4c55-9d8a-ed002c2321b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# ダッシュボードの複製

ダッシュボードを複製すると、ダッシュボード内のすべてのレポートを新しいダッシュボードにコピーできます。

これは、既存のグラフのセットを再作成しても、パースペクティブ（異なるデータビュー、異なるマーケット、異なる web サイトまたはストアなど）を変更する場合に便利です。 ダッシュボードを複製した後、新しい各グラフを編集して、指標、データビュー、フィルターまたはグループ化を変更できます。

1. ダッシュボードのクローンを作成するには、画面の上部にある「**[!UICONTROL Options]**」をクリックします。

1. ドロップダウンで、「**[!UICONTROL Save As]**」をクリックします。

1. プロンプトが表示されたら、`New Dashboard Name` を入力します。 Adobeでは、ダッシュボードに含まれる情報を一目で把握できる名前を使用することをお勧めします。

   例えば、`Customer Activity` という名前のダッシュボードをクローンするとします。 このダッシュボードには、フィラデルフィアの場所の顧客アクティビティ情報が含まれていましたが、新しいニューヨーク市区町村用のダッシュボードを作成するとします。 このダッシュボードには `New York City - Customer Activity` という名前を付けることができます。

1. `Chart Title Find` および `Chart Title Replace` フィールドを使用して、タイトルに `Philadelphia` が含まれるすべてのグラフを検索し、`New York City` に置き換えます。

   これらのフィールドに値を入力しない場合、新しいダッシュボードのすべてのグラフタイトルの末尾に `(2)` が自動的に追加されます。

1. 「**[!UICONTROL Save]**」をクリックして、ダッシュボードのクローンを作成します。

例：

![&#x200B; ダッシュボードの複製 &#x200B;](../../assets/datgif.gif)
