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

これは、既存のグラフのセットを再作成しながら、パースペクティブを変更する場合（例えば、データビュー、マーケット、Web サイト、ストアが異なる場合）に役立ちます。 ダッシュボードを複製した後、新しい各グラフを編集して、その指標、データビュー、フィルターまたはグループ化を変更できます。

1. ダッシュボードのクローンを作成するには、 **[!UICONTROL Options]** をクリックします。

1. ドロップダウンで、 **[!UICONTROL Save As]**.

1. プロンプトが表示されたら、 `New Dashboard Name`. Adobeでは、ダッシュボードに含まれる情報を一目で示す名前を推奨します。

   たとえば、次の名前のダッシュボードを複製するとします。 `Customer Activity`. このダッシュボードには、フィラデルフィアの所在地に関する顧客のアクティビティ情報が含まれていましたが、新しいニューヨーク市の所在地に関するダッシュボードを作成する場合は、 このダッシュボードには、と名前を付けることができます。 `New York City - Customer Activity`.

1. 以下を使用します。 `Chart Title Find` および `Chart Title Replace` フィールドを指定して、 `Philadelphia` タイトル内でを次に置き換えます。 `New York City`.

   これらのフィールドに値を入力しない場合、 `(2)` は、新しいダッシュボードのすべてのグラフタイトルの最後にを自動的に追加します。

1. クリック **[!UICONTROL Save]** をクリックして、ダッシュボードのクローンを作成します。

例：

![ダッシュボードの複製](../../assets/datgif.gif)
