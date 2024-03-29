---
title: その他の広告費用データのインポート
description: オフラインまたは他の広告費用データをにインポートする方法を説明します。 [!DNL Commerce Intelligence].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# その他の広告費用データのインポート

広告費用データをアップロードすると、広告コストと `customer lifetime value (CLV)` キャンペーンから取得したユーザー数を格納できます。

## 広告コストデータをアップロード中

広告支出データを分析する最初の手順は、データを取得することです。 ほとんどの広告プラットフォームではレポートの書き出しが可能なので、Adobeでは、広告プラットフォームから生データを書き出し、直接にアップロードすることをお勧めします。 [!DNL Commerce Intelligence] 操作しないで Data Warehouse内のデータに対して操作を実行できるので、作業を倍増する必要はありません。

広告費用データを書き出したら、 [`File Upload` 機能](../connecting-data/using-file-uploader.md) データをData Warehouseに取り込む 新しいデータを同じにアップロードできます [!DNL Commerce Intelligence] 表を示します。

## オフラインソース

オンラインキャンペーンに加えて、ラジオや広告掲示板など、オフラインで広告を表示することもできます。 このような状況を考慮するには、にコストデータを含むスプレッドシートを手動でアップロードします。 [!DNL Commerce Intelligence].

次に示す表構造は、 `.csv` 広告費用データを記録するファイル。 また、例として、このトピックの下部にテンプレートファイルが添付されています。 推奨される列は次のとおりです。

* `ID`  — データベースがプライマリキーとして使用する各データ行の一意の識別子です。 これは、行ごとに異なる必要があります。
* `Date`  — キャンペーンの実行日を yyyy-mm-dd 形式で表します。
* `Amount`  — キャンペーンに費やした金額。
* `campaign`  — これはキャンペーン名です。 を使用している場合、 [!DNL Google Analytics] その他の広告費用データを追跡するには、utm\_campaign 名と一致する必要があります。
* `source`  — これはソース名です。 を使用している場合、 [!DNL Google Analytics]の場合、これは `utm_source` 名前。
* `other` （オプション） — キャンペーンやコストのセグメント化に役立つ追加の列を組み込むこともできます。 また、複数の異なる UTM キャンペーン名を 1 つの一貫したキャンペーンにまとめて、追跡目的で使用することもできます。 これを手動で設定するのではなく、2 番目のシートに対して V-Lookup を使用して、各キャンペーン名を「その他の名前」と照合し、ここで動的にレポートするとよいでしょう。

## 関連

* [接続 [!DNL AdWords] データ](../integrations/google-adwords.md)
* [広告キャンペーンの ROI の向上](../../analysis/roi-ad-camp.md)
