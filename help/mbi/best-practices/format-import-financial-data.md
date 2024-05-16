---
title: 財務データのフォーマットとインポート
description: 財務データの書式設定とインポート方法を説明します。
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 財務データのフォーマットとインポート

このトピックでは、で分析する財務データをインポートする最適な方法を説明します [!DNL Adobe Commerce Intelligence].

2 次元のクロスタブ データ テーブルは、多くの場合、財務データに使用される形式です。 列と行の両方のラベルで値が分類されるので、このタイプのレイアウトは人間の目やスプレッドシートツールで簡単に表示できるかもしれませんが、データベースには適していません。

![](../../mbi/assets/crosstab.png)

このデータをインポートして分析するには [!DNL Commerce Intelligence]を使用する場合、テーブルは 1 次元のリストにフラット化する必要があります。 フラット化すると、各データ値は複数のラベルによって分類され、すべてが 1 行に含まれます。各行は一意であるか、主キー列などの一意の識別子を持ちます。

![](../../mbi/assets/flattened.png)

## インポートする Excel ファイルのフォーマット

2 次元テーブルを使用してフラット化するには [!DNL Excel] ピボットテーブル：

1. 2 次元データ テーブルを使用してファイルを開きます。
1. ピボットテーブル ウィザードを開きます。 対象： [!DNL Windows]を使用する場合、ショートカットはです。 `Alt-D`. 対象： [!DNL Mac OS]、と入力します `Command-Option-P`.
1. を選択 **[!UICONTROL Multiple consolidated ranges]** をクリックして、 **[!UICONTROL Next]**.
1. を選択 **[!UICONTROL I will create the page fields]** をクリックして、 **[!UICONTROL Next]**.
1. ラベルを含む 2 次元テーブルのデータ・セット全体を選択します。 を確実にする `0` を目的のページフィールドの数に設定して、 **[!UICONTROL Next]**.
1. 新しいシートにピボットテーブルを作成し、 **[!UICONTROL Finish]**.
1. フィールドリストから列フィールドと行フィールドの選択を解除します。
1. 結果の数値をダブルクリックして、フラット化されたソースデータを新しいシートに表示します。
   ![](../../mbi/assets/pivot-table-double-click.png)
1. 別名で保存 `CSV` ファイル。

## まとめ

データ テーブルはリスト形式に変換され、元の情報がすべて保持されます。現在は、次の形式になります [インポート先 [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) 分析用。
