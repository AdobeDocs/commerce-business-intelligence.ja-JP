---
title: 金融データのフォーマットとインポート
description: 財務データの書式設定と読み込み方法について説明します。
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/O1WKa98rRVw1dcgNQPsORit2gmZNn1Wi7H-Q4J7KcA0
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 278
ht-degree: 0%

---

# 財務データのフォーマットとインポート

このトピックでは、[!DNL Adobe Commerce Intelligence]で分析するために財務データをインポートする最適な方法について説明します。

2次元のクロスタブデータテーブルは、一般的に財務データに使用される形式です。 値が列と行の両方のラベルで分類される場合、このタイプのレイアウトは、人間の目やスプレッドシートのツールでは見やすいかもしれませんが、データベースには適していません。

![ ピボットテーブルのレイアウトにデータを表示するクロスタブ形式](../../mbi/assets/crosstab.png)

このデータを[!DNL Commerce Intelligence]に読み込んで分析するには、テーブルを1次元のリストに統合する必要があります。 統合すると、各データ値は、1行の複数のラベルによって分類されます。各行は一意であるか、一意の識別子（プライマリキー列など）を持ちます。

![列レイアウトにデータを表示する統合された形式](../../mbi/assets/flattened.png)

## インポート用のExcel ファイルの書式設定

[!DNL Excel] ピボットテーブルを使用して2次元テーブルを統合するには：

1. 2次元データテーブルを含むファイルを開きます。
1. ピボットテーブル ウィザードを開きます。 [!DNL Windows]では、ショートカットは`Alt-D`です。 [!DNL Mac OS]に、`Command-Option-P`と入力します。
1. **[!UICONTROL Multiple consolidated ranges]**&#x200B;を選択し、**[!UICONTROL Next]**&#x200B;をクリックします。
1. **[!UICONTROL I will create the page fields]**&#x200B;を選択し、**[!UICONTROL Next]**&#x200B;をクリックします。
1. ラベルを含め、2次元テーブルのデータセット全体を選択します。 目的のページフィールド数に対して`0`が選択されていることを確認し、**[!UICONTROL Next]**&#x200B;をクリックします。
1. 新しいシートにピボットテーブルを作成し、**[!UICONTROL Finish]**&#x200B;をクリックします。
1. フィールドリストから列フィールドと行フィールドの選択を解除します。
1. 結果の数値をダブルクリックして、統合されたソースデータを新しいシートに表示します。
   ダブルクリックして展開することを示す![Excel ピボットテーブルのフィールドリスト ](../../mbi/assets/pivot-table-double-click.png)
1. `CSV` ファイルとして保存します。

## まとめ

データテーブルはリスト形式に変換され、元のすべての情報が保持され、分析用に[を [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md)にインポートできるようになりました。
