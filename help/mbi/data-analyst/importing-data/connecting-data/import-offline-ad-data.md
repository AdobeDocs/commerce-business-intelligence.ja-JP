---
title: その他の広告費データのインポート
description: オフラインまたはその他の広告費データを [!DNL Commerce Intelligence]にインポートする方法について説明します。
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/jx-MMry1-XGeM4htPkH6GC1Et5nYjyD7aWn3p-nmcC8
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 369
ht-degree: 0%

---

# その他の広告費データのインポート

広告費データをアップロードすると、広告コストとキャンペーンから獲得したユーザー`customer lifetime value (CLV)`を組み合わせて、キャンペーンのROIを測定できます。

## 広告コストデータのアップロード

広告費データを分析する最初のステップは、データを取得することです。 ほとんどの広告プラットフォームではレポートを書き出すことができるため、Adobeでは、広告プラットフォームから生データを書き出し、操作なしで[!DNL Commerce Intelligence]に直接アップロードすることをお勧めします。 Data Warehouseのデータに対して操作を実行できるので、作業を2倍にする必要はありません。

広告費データを書き出したら、[`File Upload`機能](../connecting-data/using-file-uploader.md)を使用してデータをData Warehouseに取り込みます。 同じ[!DNL Commerce Intelligence] テーブルに新しいデータを時間をかけてアップロードできます。

## オフラインソース

オンラインキャンペーンに加えて、ラジオや看板などのオフラインの広告を利用することもできます。 これらのケースを考慮して、コスト データを含むスプレッドシートを[!DNL Commerce Intelligence]に手動でアップロードできます。

広告費データを記録する`.csv` ファイルを作成する場合は、以下で説明するテーブル構造をお勧めします。 このトピックの下部には、例としてテンプレートファイルも添付されています。 推奨される列は次のとおりです。

* `ID` – これは、データベースがプライマリキーとして使用するデータ行ごとに一意の識別子です。 これは行ごとに異なる必要があります。
* `Date` - yyyy-mm-dd形式でキャンペーンを実行した日付です。
* `Amount` - キャンペーンに費やした金額です。
* `campaign` – これはキャンペーン名です。 [!DNL Google Analytics]を使用して他の広告費データを追跡している場合は、utm\_campaign名と一致する必要があります。
* `source` – これはソース名です。 [!DNL Google Analytics]を使用している場合は、`utm_source`の名前と一致する必要があります。
* `other` （オプション） – キャンペーンとコストのセグメンテーションに役立つ列を追加することもできます。 また、複数の異なるUTM キャンペーン名を、トラッキング目的で単一の一貫性のあるキャンペーンに要約することもできます。 これを手動で設定するのではなく、V-Lookup to a second sheetを使用して、各キャンペーン名を他の名前に一致させ、ここで動的に報告することをお勧めします。

## 関連

* [ [!DNL AdWords]  データを接続](../integrations/google-adwords.md)
* [広告キャンペーンのROIを高める](../../analysis/roi-ad-camp.md)
