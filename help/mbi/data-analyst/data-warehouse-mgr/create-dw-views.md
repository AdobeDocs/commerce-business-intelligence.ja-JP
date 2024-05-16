---
title: Data Warehouseビューの作成と使用
description: 既存のテーブルを変更して新しいウェアハウス型テーブルを作成する方法、または SQL を使用して複数のテーブルを結合または統合する方法について説明します。
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 6%

---

# Data Warehouseビューの操作

このドキュメントでは、の目的と使用について説明します `Data Warehouse Views` に移動してアクセス可能 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**. 次に、機能とビューの作成方法を説明し、の使用方法の例を示します `Data Warehouse Views` 連結する [!DNL Facebook] および [!DNL AdWords] 費用データ。

## 一般用途

この `Data Warehouse Views` この機能は、既存のテーブルを変更したり、SQL を使用して複数のテーブルを結合または統合したりして、新しいウェアハウス テーブルを作成する方法です。 1 回 `Data Warehouse View` が更新サイクルで作成および処理され、の下の新しいテーブルとしてData Warehouseに入力されます。 `Data Warehouse Views` 次に示すように、ドロップダウンを使用します。

![](../../assets/Data_Warehouse.png)

ここから、新しいビューは他のテーブルと同様に機能し、新しい計算列を作成したり、指標とレポートを作成したりできます。

`Data Warehouse Views` 主に、類似しているが異なる複数のテーブルを統合して、すべてのレポートを 1 つの新しいテーブルで作成できるようにするために使用されます。 一般的な例としては、従来のデータベースとライブデータベースのテーブルを統合して履歴データと現在のデータを組み合わせたり、Facebookや AdWords などの複数の広告ソースを 1 つの広告に組み合わせたりすることができます `Consolidated ad spend` テーブル。

SQL に精通している場合、これらの統合の例ではどちらも `UNION` 関数ですが、新しいビューを作成する際には任意の PostgreSQL 構文と関数を使用できます。

## Data Warehouseビューの作成と管理

新規 `Data Warehouse Views` に移動することで、を作成したり、既存のビューを削除したりできます。 **[!UICONTROL Manage Data]** > **[!UICONTROL Data Warehouse Views]**&#x200B;を次に示します。

![](../../assets/Data_Warehouse_Views.png)

ここから、以下のサンプル手順に従ってビューを作成できます。

1. 既存のビューを確認する場合は、をクリックします **[!UICONTROL New Data Warehouse View]** をクリックして、空のクエリ ウィンドウを開きます。 空のクエリウィンドウが既に開いている場合は、次の手順に進みます。
1. を入力して、ビューに名前を付けます。 `View Name` フィールド。 ここで指定した名前によって、Data Warehouseのビューの表示名が決まります。 `View names` は、小文字、数字、アンダースコア（_）に制限されます。 その他の文字は使用できません。
1. という名前のウィンドウにクエリを入力します。 `Select Query`標準の PostgreSQL 構文を使用します。

   >[!NOTE]
   >
   >クエリでは、特定の列名を参照する必要があります。 の使用 `*`すべての列を選択する文字は許可されていません。

1. 完了したら、 **[!UICONTROL Save]** ビューを保存します。 現在のビューには一時的に `Pending` 次回の完全更新サイクルで処理されるまでのステータス。次のサイクルで処理された時点で、ステータスがに変わります。 `Active`. 更新で処理されると、ビューをレポートで使用できるようになります。

保存後、基になるクエリがの生成に使用されることに注意してください `Data Warehouse View` 編集できません。 構造を調整する必要がある場合 `Data Warehouse View`の場合は、ビューを作成し、計算列、指標またはレポートを元のビューから新しいビューに手動で移行する必要があります。 移行が完了したら、元のビューを安全に削除できます。 なぜなら `Data Warehouse Views` は編集できません。Adobeでは、 `SQL Report Builder` クエリをData Warehouseビューとして保存する前に。

## 例： [!DNL Facebook] および [!DNL Google AdWords] データ

この記事で前述した例の 1 つを詳しく見てください。統合 [!DNL Facebook] および [!DNL AdWords] データを新しい統合広告テーブルに費やします。 最も一般的には、以下のサンプルデータセットを使用した 2 つのテーブルの統合が含まれます。

`Ad source: Google AdWords`

`Table name: campaigns67890`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | 経過週 | 60 | 2017-05-05 00:00:00 | 2000 | 10.2 |
| 2 | ggg | 40 | 2017-05-23 00:00:00 | 900 | 4.6 |
| 3 | aaa | 22 | 2017-06-12 00:00:00 | 400 | 2.5 |
| 4 | 経過週 | 350 | 2017-06-30 00:00:00 | 14500 | 35 |
| 5 | fff | 280 | 2017-07-10 00:00:00 | 10200 | 28.5 |

`Ad source: Facebook`

`Table name: facebook_ads_insights_12345`

`Sample data:`

| **`_id`** | **`campaign`** | **`adClicks`** | **`date`** | **`impressions`** | **`adCost`** |
|--- |--- |--- |--- |--- |--- |
| 1 | aaa | 25 | 2017-05-01 00:00:00 | 1200 | 5 |
| 2 | ddd | 12 | 2017-05-15 00:00:00 | 800 | 2.5 |
| 3 | aaa | 40 | 2017-05-22 00:00:00 | 2000 | 7 |
| 4 | aaa | 110 | 2017-06-08 00:00:00 | 6000 | 10 |
| 5 | ccc | 5 | 2017-07-06 00:00:00 | 300 | 1.2 |

両方を含む単一の広告費用テーブルを作成するには [!DNL Facebook] および [!DNL Google AdWords] キャンペーンの場合は、SQL クエリを記述し、を使用する必要があります `UNION ALL` 関数。 A `UNION ALL` 文は、各クエリの結果を 1 つの出力に追加する際に、複数の個別の SQL クエリを組み合わせるために最もよく使用されます。

には、いくつかの要件があります `UNION` postgreSQL で概説されているように、言及する価値のあるステートメント [詳細を見る](https://www.postgresql.org/docs/8.3/queries-union.html):

* すべてのクエリは、同じ数の列を返す必要があります
* 対応する列は、同じデータタイプである必要があります

を実行する場合 `UNION` または `UNION ALL` ステートメントでは、最終的な出力内の列の名前は、最初のクエリの列の名前を反映しています。

通常、を統合します [!DNL Facebook] および [!DNL Google AdWords] データを～に費やす `Data Warehouse View` では、次のようなクエリを使用して、7 つの列を持つテーブルを作成する必要があります。

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

上記に関するいくつかの重要な点を以下に示します。

* わかりやすくするために、すべての列はこれらよりもエイリアス化され、すべてのクエリで名前が一致するようになります。 ただし、これは要件ではありません。 SELECT クエリでカラムが呼び出される順序によって、カラムの並び方が決まります。
* という新しい列 `ad_source` を作成して、フィルタリングを容易にする [!DNL AdWords] または [!DNL Facebook] データ。 このクエリは、両方のテーブルのすべてのデータを結合することに注意してください。 のような列を作成しない場合 `ad_source`、特定のソースから支出を識別する簡単な方法はありません。

上記のクエリをとして保存 `Data Warehouse View` 両方を含むテーブルを作成します [!DNL Facebook] および [!DNL AdWords] 次のような費用：

| **`id`** | **`ad_source`** | **`date`** | **`campaign`** | **`spend`** | **`impressions`** | **`clicks`** |
|--- |--- |--- |--- |--- |--- |--- |
| **1** | [!DNL Facebook] | 2017-05-01 00:00:00 | aaa | 5 | 1200 | 25 |
| **1** | [!DNL Google AdWords] | 2017-05-05 00:00:00 | 経過週 | 10.2 | 2000 | 60 |
| **2** | [!DNL Facebook] | 2017-05-15 00:00:00 | ddd | 2.5 | 800 | 12 |
| **2** | [!DNL Google AdWords] | 2017-05-23 00:00:00 | ggg | 4.6 | 900 | 40 |
| **3** | [!DNL Facebook] | 2017-05-22 00:00:00 | aaa | 7 | 2000 | 40 |
| **3** | [!DNL Google AdWords] | 2017-06-12 00:00:00 | aaa | 2.5 | 400 | 22 |
| **4** | [!DNL Facebook] | 2017-06-08 00:00:00 | aaa | 10 | 6000 | 110 |
| **4** | [!DNL Google AdWords] | 2017-06-30 00:00:00 | 経過週 | 35 | 14500 | 350 |
| **5** | [!DNL Facebook] | 2017-07-06 00:00:00 | ccc | 1.2 | 300 | 5 |
| **5** | [!DNL Google AdWords] | 2017-07-10 00:00:00 | fff | 28.5 | 10200 | 280 |

広告ソースごとに個別のマーケティング指標セットを作成するのではなく、上記の表を使用して単一の指標セットを作成するだけで、すべての広告を取り込むことができます。

**その他のヘルプをお探しですか？**

SQL の記述と作成 `Data Warehouse Views` は、テクニカルサポートには含まれていません。 ただし、 [サービスチーム](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) ビューの作成に役立ちます。 従来のデータベースを新しいデータベースに移行して、特定の分析のために 1 つのData Warehouseビューを作成するといった作業は、サポートチームがサポートします。

通常、新しいの作成 `Data Warehouse View` 2～3 の同様に構造化されたテーブルを統合する場合、5 時間のサービス時間が必要になり、これは約 1,250 ドルの作業になります。 ただし、以下に、必要な予想投資を増やす可能性のある一般的な要因を示します。

* 3 つ以上のテーブルを 1 つのビューに統合
* 複数のData Warehouseビューの作成
* 複雑な結合ロジックまたはフィルター条件
* 異なるデータ構造を持つ 2 つ以上のテーブルの統合
