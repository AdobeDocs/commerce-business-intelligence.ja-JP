---
title: SQL Report Builderの操作
description: SQL Report Builderを使用してデータと指標を監査し、結果をローカルデータベースのデータと比較する方法を説明します。
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Data Architect, Data Engineer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# [!DNL SQL Report Builder]

[!DNL SQL Report Builder] は主に新しいレポートを作成し、分析に基づいて繰り返し処理するために使用されますが、データや指標を効果的に監査するためにも使用できます。 次の情報では、[!DNL SQL Report Builder] を使用してデータと指標を監査し、結果をローカルデータベースのデータと比較する方法について説明します。

## 指標のクエリ

開始するには、**[!UICONTROL Report Builder > SQL Report Builder > Create Report]** に移動して [!DNL SQL Report Builder] を開きます。 [!DNL SQL] エディターのサイドバーを使用すると、指標の上にマウスポインターを置いて「**[!UICONTROL Insert]**」をクリックすることで、指標をクエリに直接挿入できます。 その指標のクエリ定義がエディターに追加されます。 定義には、次のコンポーネントが含まれます。

- 実行されている **指標操作** を次の例の `SUM()` で示します。
- `FROM` 句で示され **指標が構築される** テーブル。
- 指標に追加されたすべての **フィルター（およびフィルターセット）** 次の例の `WHERE` 句で示されます。
- データを並べ替える **タイムスタンプ** （年、月）のコンポーネント。次の例の `ORDER BY` 句で示されます。

クエリをより明確に表示するために、クエリフィールドでの表示方法を再書式設定できます。 準備ができたら、「`Run Query`」を選択します。 結果は、クエリの下のレポートパネルにテーブルとして表示されます。

![](../../assets/run-query-results.gif)

## クエリの制限

特定の不一致やデータセットを特定しようとしている場合は、ローカルデータベースに照らし合わせて確認するために、クエリを特定のサンプルに制限する必要があります。 それには、目的の制限に合わせてクエリを編集します。 次の例では、2013 年 1 月 1 日以降の売上高のみを含めるようにクエリを制限しています。 クエリを更新したら、もう一度 **[!UICONTROL Run Query]** を選択して結果を更新します。

![](../../assets/restricting-query.gif)

## 保存とエクスポート

レポートがニーズを満たしたら、レポートに明確な名前を付け、「**[!UICONTROL Save]**」をクリックし、保存するレポートのタイプとダッシュボードを選択します。 Adobeでは、指標を監査する場合、レポートを `Table` として保存し、テストダッシュボードに保存することをお勧めします。

レポートを保存したら、「`Go to Dashboard`」を選択してそのダッシュボードに移動します。 ここからデータを書き出すには、レポートを見つけて **書き出し**&#x200B;Options gear > Full `.csv` または **[!UICONTROL Full Excel Export]** を選択します。

![](../../assets/export-dboard-data.gif)

## カスタムクエリ

また、カスタムクエリを記述し、結果を書き出して、ローカルデータベースと比較することもできます。 [ クエリ最適化のガイドライン ](../../best-practices/optimizing-your-sql-queries.md) に従って、SQL エディターにクエリを記述します。 サイドバーの上部にあるボタンを使用すると、[!DNL SQL Report Builder] で使用できるテーブルと指標のリストを切り替えて、クエリに追加できます。 カスタムクエリがニーズに合ったら、レポートを保存して、ダッシュボードからそのデータを書き出すことができます。

>[!NOTE]
>
>データを監査した後に不一致が見つかった場合は、[ サポートへの問い合わせ：データの不一致 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) のサポートトピックを参照して、次に行う作業の詳細を確認してください。
