---
title: その他の広告費用データのインポート
description: オフラインまたはその他の広告費用データのへのインポートについて説明します [!DNL Commerce Intelligence].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 0%

---

# その他の広告費用データのインポート

広告費用データをアップロードすると、広告コストとキャンペーンを組み合わせて、キャンペーン ROI を測定できます。 `customer lifetime value (CLV)` キャンペーンから取得したユーザーの。

## 広告コストデータのアップロード

広告費用データを分析する最初の手順は、データを取得することです。 ほとんどの広告プラットフォームではレポートをエクスポートできるので、Adobeでは、生データを広告プラットフォームからエクスポートして、に直接アップロードすることをお勧めします [!DNL Commerce Intelligence] 操作は必要ありません。 Data Warehouse内のデータに対して操作を実行できるので、作業を 2 倍にする必要はありません。

広告費用データを書き出したら、を使用します [`File Upload` 機能](../connecting-data/using-file-uploader.md) ：データをData Warehouseに取り込みます。 新しいデータを同じフォルダーにアップロードできます [!DNL Commerce Intelligence] テーブルの推移。

## オフラインソース

オンラインキャンペーンに加えて、ラジオやビルボードなどの広告をオフラインで使用することもできます。 このような場合は、コストデータを含むスプレッドシートをに手動でアップロードできます。 [!DNL Commerce Intelligence].

以下に説明するテーブル構造は、 `.csv` 広告費用データを記録するファイル。 このトピックの下部には、例としてテンプレートファイルも添付されています。 推奨される列は次のとおりです。

* `ID` - データベースでプライマリキーとして使用される各データ行の一意の ID です。 これは、行ごとに異なる必要があります。
* `Date` - キャンペーンが実行された日付（yyyy-mm-dd 形式）。
* `Amount`  – これはキャンペーンに費やした金額です。
* `campaign`  – これはキャンペーン名です。 を使用している場合 [!DNL Google Analytics] 他の広告費用データをトラッキングするには、utm\_campaign 名と一致する必要があります。
* `source` - ソース名。 を使用している場合 [!DNL Google Analytics]。これは、に一致する必要があります。 `utm_source` 名前。
* `other` （任意） – キャンペーンとコストのセグメント化に役立つ追加の列を組み込むこともできます。 また、トラッキング目的で、複数の異なる UTM キャンペーン名を単一の一貫性のあるキャンペーンにまとめる方法にもなります。 これを手動で設定するのではなく、V-Lookup を 2 番目のシートに使用して、各キャンペーン名をその他の名前と一致させ、動的にここにレポートすることをお勧めします。

## 関連

* [接続 [!DNL AdWords] データ](../integrations/google-adwords.md)
* [広告キャンペーンの ROI の向上](../../analysis/roi-ad-camp.md)
