---
title: SQLReport Builder
description: SQLReport Builderを使用してデータと指標を監査し、結果とローカルデータベースのデータを比較する方法を説明します。
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Data Architect, Data Engineer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 0%

---

# [!DNL SQL Report Builder]

The [!DNL SQL Report Builder] は、主に新しいレポートを作成し、分析を繰り返し実行するために使用されますが、データと指標を効果的に監査するためにも使用できます。 次の情報では、 [!DNL SQL Report Builder] 結果をローカルデータベースのデータと比較できます。

## 指標のクエリ

利用を開始するには、 [!DNL SQL Report Builder] 移動して **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. サイドバーは、 [!DNL SQL] エディターを使用して、指標の上にマウスポインターを置いて「 **[!UICONTROL Insert]**. これにより、その指標のクエリ定義がエディターに追加されます。 定義には、次のコンポーネントが含まれます。

- The **指標操作** 実行され、次のように示される `SUM()` を次の例に示します。
- The **～に関するテーブル** 指標が構築され、 `FROM` 句を使用します。
- 任意 **フィルタ（およびフィルタセット）** が指標に追加され、 `WHERE` 句を使用して、以下の例で使用します。
- のコンポーネント **timestamp** （年、月）データを並べ替える際に、 `ORDER BY` 句を使用して、以下の例で使用します。

クエリをより明確に表示するには、クエリフィールドでの表示形式を変更します。 準備が整ったら、「 」を選択します。 `Run Query`. 結果は、クエリの下のレポートパネルにテーブルとして表示されます。

![](../../assets/run-query-results.gif)

## クエリの制限

特定の不一致やデータのセットを特定する場合は、クエリを特定のサンプルに制限して、ローカルデータベースに対して確認する必要があります。 これをおこなうには、クエリを編集して、目的の制限に合わせます。 次の例では、クエリを制限して 2013 年 1 月 1 日以降の売上高のみを含めます。 クエリを更新した後、 **[!UICONTROL Run Query]** を再度クリックして、結果を更新します。

![](../../assets/restricting-query.gif)

## 保存とエクスポート

レポートがニーズを満たしたら、レポートに別の名前を付け、「 **[!UICONTROL Save]**&#x200B;をクリックし、保存するレポートの種類とダッシュボードを選択します。 指標を監査する場合、Adobeでは、レポートを `Table` テストダッシュボードに保存します。

レポートを保存したら、「 」を選択してそのダッシュボードに移動します。 `Go to Dashboard`. ここから、レポートを見つけて、「 」を選択することで、データをエクスポートできます。 **[!UICONTROL Options gear > Full `.csv`書き出し]** または **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## カスタムクエリ

また、カスタムクエリを記述し、結果を書き出してローカルデータベースと比較することもできます。 次に、 [クエリ最適化のガイドライン](../../best-practices/optimizing-your-sql-queries.md)を使用する場合は、SQL エディターでクエリを記述します。 サイドバーの上部にあるボタンを使用して、テーブルのリストと、 [!DNL SQL Report Builder] をクリックし、クエリに追加します。 カスタムクエリがニーズに合ったら、レポートを保存し、ダッシュボードからそのデータを書き出すことができます。

>[!NOTE]
>
>データの監査後に不一致が見つかった場合は、 [サポートへの問い合わせ：データの相違](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) 次の作業の詳細については、サポートトピックを参照してください。
