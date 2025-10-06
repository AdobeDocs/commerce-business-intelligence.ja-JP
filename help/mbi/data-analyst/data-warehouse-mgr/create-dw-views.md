---
title: Data Warehouse ビューの作成と使用
description: 既存のテーブルを変更して新しいウェアハウス型テーブルを作成する方法、または SQL を使用して複数のテーブルを結合または統合する方法について説明します。
exl-id: 5aa571c9-7f38-462c-8f1b-76a826c9dc55
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 6%

---

# Data Warehouse ビューの操作

このドキュメントでは、`Data Warehouse Views`/**[!UICONTROL Manage Data]** に移動してアクセス可能な **[!UICONTROL Data Warehouse Views]** の目的と使用について説明します。 以下に、アクティビティの概要とビューの作成方法を説明し、`Data Warehouse Views` を使用して [!DNL Facebook] ータと [!DNL AdWords] の支出データを統合する方法の例を示します。

## 一般用途

`Data Warehouse Views` の機能は、既存のテーブルを変更して新しいウェアハウス テーブルを作成する方法、または SQL を使用して複数のテーブルを結合または統合する方法です。 `Data Warehouse View` ークフローが作成され、更新サイクルで処理されると、次に示すように、`Data Warehouse Views` ドロップダウンの下の新しいテーブルとしてData Warehouseに入力されます。

![&#x200B; テーブル管理オプションを表示するData Warehouse インターフェイス &#x200B;](../../assets/Data_Warehouse.png)

ここから、新しいビューは他のテーブルと同様に機能し、新しい計算列を作成したり、指標とレポートを作成したりできます。

`Data Warehouse Views` は主に、類似しているが異なる複数のテーブルを統合して、すべてのレポートを 1 つの新しいテーブルで作成できるようにするために使用されます。 一般的な例としては、従来のデータベースとライブデータベースのテーブルを統合して履歴データと現在のデータを組み合わせたり、Facebook や AdWords などの複数の広告ソースを 1 つの `Consolidated ad spend` テーブルに組み合わせたりすることができます。

SQL に精通している場合、これらの統合例の両方で `UNION` 関数を使用していますが、新しいビューを作成する際には任意の PostgreSQL 構文および関数を使用できます。

## Data Warehouse ビューの作成と管理

以下に示すように、`Data Warehouse Views` / **[!UICONTROL Manage Data]** に移動して、新しい **[!UICONTROL Data Warehouse Views]** を作成し、既存のビューを削除できます。

![&#x200B; カスタムビュー設定を示す「Data Warehouseビュー」セクション &#x200B;](../../assets/Data_Warehouse_Views.png)

ここから、以下のサンプル手順に従ってビューを作成できます。

1. 既存のビューを監視する場合は、**[!UICONTROL New Data Warehouse View]** をクリックして空のクエリウィンドウを開きます。 空のクエリウィンドウが既に開いている場合は、次の手順に進みます。
1. `View Name` フィールドにと入力して、ビューに名前を付けます。 ここで指定される名前によって、Data Warehouseでのビューの表示名が決まります。 `View names` は、小文字、数字、アンダースコア（_）に制限されます。 その他の文字は使用できません。
1. 標準の PostgreSQL 構文を使用して、`Select Query` という名前のウィンドウにクエリを入力します。

   >[!NOTE]
   >
   >クエリでは、特定の列名を参照する必要があります。 `*` 文字を使用してすべての列を選択することは許可されていません。

1. 完了したら、「**[!UICONTROL Save]**」をクリックしてビューを保存します。 次回の完全更新サイクルで処理されるまで、ビューのステータスは一時的に `Pending` になります。次回の完全更新サイクルで、ステータスが `Active` に変わります。 更新で処理されると、ビューをレポートで使用できるようになります。

保存後は、`Data Warehouse View` ータの生成に使用される基になるクエリを編集できないことに注意してください。 `Data Warehouse View` の構造を調整する必要がある場合は、ビューを作成し、計算列、指標、またはレポートを元のビューから新しいビューに手動で移行する必要があります。 移行が完了したら、元のビューを安全に削除できます。 Adobe `Data Warehouse Views` れは編集できないので、クエリをData Warehouse ビューとして保存する前に、`SQL Report Builder` を使用してクエリの出力をテストすることをお勧めします。

## 例：[!DNL Facebook] および [!DNL Google AdWords] データ

この記事で前述した例の 1 つを詳しく見てください。[!DNL Facebook] と [!DNL AdWords] の支出データを新しい統合広告テーブルに統合します。 最も一般的には、以下のサンプルデータセットを使用した 2 つのテーブルの統合が含まれます。

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

[!DNL Facebook] キャンペーンと [!DNL Google AdWords] キャンペーンの両方を含んだ単一の広告費用テーブルを作成するには、SQL クエリを記述し、`UNION ALL` 関数を使用する必要があります。 `UNION ALL` 文は、各クエリの結果を 1 つの出力に追加する際に、複数の個別の SQL クエリを組み合わせるために最もよく使用されます。

PostgreSQL `UNION` ドキュメント [&#x200B; に概説されているように、言及する価値のある &#x200B;](https://www.postgresql.org/docs/8.3/queries-union.html) 文のいくつかの要件があります。

* すべてのクエリは、同じ数の列を返す必要があります
* 対応する列は、同じデータタイプである必要があります

`UNION` または `UNION ALL` ステートメントを実行する場合、最終的な出力内の列の名前は、最初のクエリの列の名前を反映しています。

通常、[!DNL Facebook] と [!DNL Google AdWords] の支出データを `Data Warehouse View` に統合するには、次のようなクエリを使用して、7 列のテーブルを作成する必要があります。

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
* データの `ad_source` ースや [!DNL AdWords] ストを簡単にフィルタリングできるように、[!DNL Facebook] という新しい列が作成されます。 このクエリは、両方のテーブルのすべてのデータを結合することに注意してください。 `ad_source` のような列を作成しない場合、特定のソースから支出を簡単に特定する方法はありません。

上記のクエリを `Data Warehouse View` として保存すると、次のように、[!DNL Facebook] と [!DNL AdWords] の両方の支出を含むテーブルが作成されます。

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

SQL の書き込みと `Data Warehouse Views` の作成は、テクニカルサポートには含まれていません。 ただし、[&#x200B; サービスチーム &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja) は、ビューの作成を支援します。 従来のデータベースを新しいデータベースに移行して、特定の分析のために 1 つのData Warehouse ビューを作成するといった作業に関しては、サポートチームがサポートを提供します。

通常、2～3 の同様に構造化されたテーブルを統合する目的で新しい `Data Warehouse View` ールを作成するには、5 時間のサービス時間が必要です。これは、約 1,250 ドルの作業になります。 ただし、以下に、必要な予想投資を増やす可能性のある一般的な要因を示します。

* 3 つ以上のテーブルを 1 つのビューに統合
* 複数のData Warehouse ビューの作成
* 複雑な結合ロジックまたはフィルター条件
* 異なるデータ構造を持つ 2 つ以上のテーブルの統合
