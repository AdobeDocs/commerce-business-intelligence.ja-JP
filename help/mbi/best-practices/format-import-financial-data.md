---
title: 財務データのフォーマットとインポート
description: 財務データのフォーマットとインポートの方法を説明します。
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 財務データのフォーマットとインポート

このトピックでは、分析用に財務データをインポートする最適な方法について説明します。 [!DNL Adobe Commerce Intelligence].

2 次元のクロスタブデータテーブルは、多くの場合、財務データに使用される形式です。 列と行の両方のラベルで分類された値を使用すると、このタイプのレイアウトは、人間の目やスプレッドシートツールで簡単に表示できますが、データベースにはわかりにくくなります。

![](../../mbi/assets/crosstab.png)

でこのデータをインポートおよび分析するには [!DNL Commerce Intelligence]の場合、テーブルは 1 次元のリストにフラット化する必要があります。 統合する場合、各データ値は、1 つの行にすべて含まれる複数のラベルで分類されます。各行は一意であるか、一意の識別子（例：プライマリキー列）を持ちます。

![](../../mbi/assets/flattened.png)

## 読み込む Excel ファイルの形式設定

2 次元テーブルを統合するには、 [!DNL Excel] ピボットテーブル：

1. 2 次元のデータテーブルを含んだファイルを開きます。
1. ピボットテーブルウィザードを開きます。 In [!DNL Windows]の場合、ショートカットは `Alt-D`. In [!DNL Mac OS]，と入力します。 `Command-Option-P`.
1. 選択 **[!UICONTROL Multiple consolidated ranges]** をクリックします。 **[!UICONTROL Next]**.
1. 選択 **[!UICONTROL I will create the page fields]** をクリックします。 **[!UICONTROL Next]**.
1. ラベルを含む 2 次元テーブルのデータセット全体を選択します。 以下を確認します。 `0` を選択して、「 」をクリックします。 **[!UICONTROL Next]**.
1. 新しいシートにピボットテーブルを作成し、 **[!UICONTROL Finish]**.
1. フィールドリストの列フィールドと行フィールドの選択を解除します。
1. 結果の数値をダブルクリックすると、新しいシートに統合されたソースデータが表示されます。
   ![](../../mbi/assets/pivot-table-double-click.png)
1. 名前を付けて保存 `CSV` ファイル。

## 折り返し

データテーブルはリスト形式に変換され、元の情報はすべて保持されました。これで、 [読み込み先 [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) 分析用。
