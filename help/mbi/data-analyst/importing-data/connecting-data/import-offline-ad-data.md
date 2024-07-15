---
title: その他の広告費用データのインポート
description: オフラインまたはその他の広告費用データの  [!DNL Commerce Intelligence] へのインポートについて説明します。
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# その他の広告費用データのインポート

広告費用データをアップロードすると、広告コストとキャンペーンから獲得したユーザー `customer lifetime value (CLV)` を組み合わせることで、キャンペーンの ROI を測定できます。

## 広告コストデータのアップロード

広告費用データを分析する最初の手順は、データを取得することです。 ほとんどの広告プラットフォームではレポートを書き出すことができるので、Adobeでは、生データを広告プラットフォームから書き出し、操作せずに直接 [!DNL Commerce Intelligence] にアップロードすることをお勧めします。 Data Warehouse内のデータに対して操作を実行できるので、作業を 2 倍にする必要はありません。

広告費用データを書き出したら、[`File Upload` 機能を使用して ](../connecting-data/using-file-uploader.md) データをData Warehouseに取り込みます。 同じ [!DNL Commerce Intelligence] テーブルに新しいデータを経時的にアップロードできます。

## オフラインソース

オンラインキャンペーンに加えて、ラジオやビルボードなどの広告をオフラインで使用することもできます。 このような場合は、コストデータを含むスプレッドシートを [!DNL Commerce Intelligence] に手動でアップロードできます。

以下に説明するテーブル構造は、`.csv` ファイルを作成して広告費用データを記録する際に推奨されます。 このトピックの下部には、例としてテンプレートファイルも添付されています。 推奨される列は次のとおりです。

* `ID` - データベースでプライマリキーとして使用される各データ行の一意の ID です。 これは、行ごとに異なる必要があります。
* `Date` - キャンペーンが実行された日付（yyyy-mm-dd 形式）。
* `Amount` - キャンペーンに費やした金額です。
* `campaign` - キャンペーン名です。 [!DNL Google Analytics] を使用して他の広告費用データを追跡する場合は、utm\_campaign 名と一致する必要があります。
* `source` - ソース名。 [!DNL Google Analytics] を使用している場合は、`utm_source` 名と一致する必要があります。
* `other` （任意） – キャンペーンとコストのセグメント化に役立つ追加の列を組み込むこともできます。 また、トラッキング目的で、複数の異なる UTM キャンペーン名を単一の一貫性のあるキャンペーンにまとめる方法にもなります。 これを手動で設定するのではなく、V-Lookup を 2 番目のシートに使用して、各キャンペーン名をその他の名前と一致させ、動的にここにレポートすることをお勧めします。

## 関連

* [Connect [!DNL AdWords] data](../integrations/google-adwords.md)
* [広告キャンペーンの ROI の向上](../../analysis/roi-ad-camp.md)
