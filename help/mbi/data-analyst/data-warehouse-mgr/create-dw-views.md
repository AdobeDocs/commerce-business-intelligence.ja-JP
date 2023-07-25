---
title: Data Warehouseビューの作成と使用
description: 既存の表を変更するか、SQL を使用して複数の表を結合または統合して、新しい倉庫内表を作成する方法について説明します。
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 9%

---

# Data Warehouseビューの操作

このドキュメントでは、の目的と使用方法を説明します。 `Data Warehouse Views` ～に移動してアクセスできる **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. その機能とビューの作成方法、およびの使用方法の例を次に示します `Data Warehouse Views` 統合する [!DNL Facebook] および [!DNL AdWords] 支出データ

## 汎用

この `Data Warehouse Views` 機能は、既存の表を変更するか、SQL を使用して複数の表を結合または統合することによって、新しい倉庫内表を作成する方法です。 1 回： `Data Warehouse View` が作成され、更新サイクルで処理されると、Data Warehouse内で、 `Data Warehouse Views` ドロップダウンに表示されます。

![](../../assets/Data_Warehouse.png)

ここから、新しいビューは他のテーブルと同様に機能し、新しい計算列を作成したり、その上に指標とレポートを作成したりできます。

`Data Warehouse Views` は、主に、類似しているが異なる複数のテーブルを統合し、すべてのレポートを 1 つの新しいテーブルに対して作成できるようにするために使用します。 一般的な例としては、レガシーデータベースおよびライブデータベースのテーブルを統合して履歴データと現在のデータを組み合わせたり、Facebookや AdWords などの複数の広告ソースを単数に組み合わせたりします `Consolidated ad spend` 表。

SQL に詳しい場合は、これらの統合の例の両方で、 `UNION` 関数を使用できますが、新しいビューを作成する際には、任意の PostgreSQL 構文と関数を使用できます。

## Data Warehouseビューの作成と管理

新規 `Data Warehouse Views` は次の場所に移動して作成でき、既存のビューを削除できます。 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**、以下に示すように。

![](../../assets/Data_Warehouse_Views.png)

ここから、以下のサンプル手順に従ってビューを作成できます。

1. 既存のビューを観察する場合は、 **[!UICONTROL New Data Warehouse View]** をクリックして、空白のクエリーウィンドウを開きます。 空白のクエリウィンドウが既に開いている場合は、次の手順に進みます。
1. ビューに名前を付けるには、 `View Name` フィールドに入力します。 ここで指定した名前によって、Data Warehouseのビューの表示名が決まります。 `View names` は、小文字、数字、アンダースコア (_) に制限されます。 その他の文字はすべて禁止されています。
1. 「 」というタイトルのクエリをウィンドウに入力します `Select Query`、標準の PostgreSQL 構文を使用します。

   >[!NOTE]
   >
   >クエリは、特定の列名を参照する必要があります。 の使用 `*`すべての列を選択する文字は使用できません。

1. 完了したら、「 **[!UICONTROL Save]** をクリックしてビューを保存します。 一時的に `Pending` 次の完全更新サイクルで処理されるまでのステータス。その時点で、ステータスは「 `Active`. 更新によって処理された後、ビューは、レポートで使用する準備が整いました。

保存後、基になるクエリを使用して `Data Warehouse View` は編集できません。 の構造を調整する必要がある場合 `Data Warehouse View`を使用する場合は、ビューを作成し、計算された列、指標またはレポートを元のビューから新しいビューに手動で移行する必要があります。 移行が完了したら、元のビューを安全に削除できます。 理由： `Data Warehouse Views` は編集できません。Adobeでは、 `SQL Report Builder` クエリをData Warehouse表示として保存する前に

## 例： [!DNL Facebook] および [!DNL Google AdWords] データ

この記事で前述した例の 1 つを詳しく見てみましょう。統合 [!DNL Facebook] および [!DNL AdWords] データを新しく統合された広告テーブルに使用する。 最も一般的に、2 つのテーブルの統合に関連しています。この場合、サンプルのデータセットは次のようになります。

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | ee | 60 | 2017-05-05 00:00:00 | 2000 | 10.2 |
| 2 | ggg | 40 | 2017-05-23 00:00:00 | 900 | 4.6 |
| 3 | aa | 22 | 2017-06-12 00:00:00 | 400 | 2.5 |
| 4 | ee | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | fff | 280 | 2017-07-10 00:00:00 | 10200 | 28.5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aa | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | ddd | 12 | 2017-05-15 00:00:00 | 800 | 2.5 |
| 3 | aa | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | aa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | cc | 5 | 2017-07-06 00:00:00 | 300 | 1.2 |

両方を含む単一の広告費用テーブルを作成するには [!DNL Facebook] および [!DNL Google AdWords] キャンペーンの場合は、SQL クエリを作成し、 `UNION ALL` 関数に置き換えます。 A `UNION ALL` 文は、複数の個別の SQL クエリを組み合わせながら、各クエリの結果を 1 つの出力に追加する場合に最もよく使用されます。

次に示す要件がいくつかあります。 `UNION` PostgreSQL で概要を説明するように、言及する価値のあるステートメント [ドキュメント](https://www.postgresql.org/docs/8.3/queries-union.html):

* すべてのクエリは同じ数の列を返す必要があります
* 対応する列は、同じデータタイプを持つ必要があります

の実行時 `UNION` または `UNION ALL` 文内の列の名前は、最終出力内の列の名前が、最初のクエリでの列の名前を反映しています。

通常、 [!DNL Facebook] および [!DNL Google AdWords] データを～に使う `Data Warehouse View` 次のようなクエリを使用して、7 つの列を持つテーブルを作成する必要があります。

```sql
    SELECT
        "_id" as id,
        'AdWords' as ad_source,
        "date",
        "campaign",
        "adCost" as spend,
        "impressions",
        "adClicks" as clicks
    FROM campaigns67890
    UNION
    SELECT
        "_id" as id,
        'Facebook' as ad_source,
        "date_start" as date,
        "campaign_name" as campaign,
        "spend",
        "impressions",
        "clicks"
    FROM facebook_ads_insights_12345
```

上記に関する重要な点を 2 つ示します。

* 明確にするため、すべての列は、すべてのクエリで名前が一致するように、上にエイリアスされます。 ただし、これは必須ではありません。 SELECT クエリで列が呼び出される順序は、列の並び順を示します。
* 新しい列 `ad_source` フィルタリングを容易にするために作成されました。 [!DNL AdWords] または [!DNL Facebook] データ。 このクエリは、両方のテーブルのすべてのデータを組み合わせることに注意してください。 次のような列を作成しない場合 `ad_source`を使用する場合、特定のソースから支出を簡単に識別する方法はありません。

上記のクエリを `Data Warehouse View` は、 [!DNL Facebook] および [!DNL AdWords] 以下のような費用。

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | aa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | ee | 10.2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | ddd | 2.5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | ggg | 4.6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aa | 2.5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | ee | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | cc | 1.2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | fff | 28.5 | 10200 | 280 |

各広告ソースに対して個別のマーケティング指標のセットを作成するのではなく、上記の表を使用して 1 つの指標のセットのみを作成し、すべての広告を取り込むことができます。

**その他のヘルプが必要な場合は、**

SQL の記述と作成 `Data Warehouse Views` はテクニカルサポートに含まれていません。 ただし、 [サービスチーム](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) では、ビューの作成に関する支援を提供します。 従来のData Warehouseを新しいデータベースで移行して、特定の分析用に単一のデータベースビューを作成するなど、あらゆる点でサポートチームがお手伝いします。

通常、 `Data Warehouse View` 2～3 の同様の構造を持つテーブルを統合するためには、5 時間のサービス時間が必要となります。これは、約 1,250 ドルの作業に変換されます。 しかし、以下は、必要な投資を増やす可能性がある一般的な要因です。

* 3 つ以上のテーブルを 1 つのビューに統合
* 複数のData Warehouseビューの作成
* 複雑な結合ロジックまたはフィルター条件
* 異なるデータ構造を持つ複数のテーブルの統合
