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

この [!DNL SQL Report Builder] 主に新しいレポートを作成し、分析に基づいて繰り返し処理するために使用されますが、データや指標を効果的に監査するためにも使用できます。 次の情報では、を使用してデータと指標を監査する方法を説明します [!DNL SQL Report Builder] 結果をローカルデータベースのデータと比較できるようにします。

## 指標のクエリ

開始するには、を開きます [!DNL SQL Report Builder] に移動します。 **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. サイドバーは次で使用できます [!DNL SQL] エディターで指標の上にマウスポインターを置き、をクリックすることで、指標をクエリに直接挿入できます **[!UICONTROL Insert]**. その指標のクエリ定義がエディターに追加されます。 定義には、次のコンポーネントが含まれます。

- この **指標演算** 実行中（で示される） `SUM()` 以下の例ではです。
- この **のテーブル** 指標が構築され、 `FROM` 句。
- 任意 **フィルター（およびフィルターセット）** 指標に追加され、によって示されている `WHERE` 次の例の句。
- のコンポーネント **timestamp** データの順序付けの対象となる年、月（ `ORDER BY` 次の例の句。

クエリをより明確に表示するために、クエリフィールドでの表示方法を再書式設定できます。 準備ができたら、 `Run Query`. 結果は、クエリの下のレポートパネルにテーブルとして表示されます。

![](../../assets/run-query-results.gif)

## クエリの制限

特定の不一致やデータセットを特定しようとしている場合は、ローカルデータベースに照らし合わせて確認するために、クエリを特定のサンプルに制限する必要があります。 それには、目的の制限に合わせてクエリを編集します。 次の例では、2013 年 1 月 1 日以降の売上高のみを含めるようにクエリを制限しています。 クエリを更新した後、 **[!UICONTROL Run Query]** を繰り返して、結果を更新します。

![](../../assets/restricting-query.gif)

## 保存とエクスポート

レポートがニーズを満たしたら、レポートに明確な名前を付けて、 **[!UICONTROL Save]**&#x200B;をクリックし、保存するレポートのタイプとダッシュボードを選択します。 指標を監査する場合、Adobeはレポートをとして保存することをお勧めします `Table` テストダッシュボードに保存します。

レポートを保存したら、次のオプションを選択してそのダッシュボードに移動します。 `Go to Dashboard`. ここから、レポートを見つけて選択することで、データを書き出すことができます。 **[!UICONTROL Options gear > Full `.csv`Export]** または **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## カスタムクエリ

また、カスタムクエリを記述し、結果を書き出して、ローカルデータベースと比較することもできます。 次に [クエリの最適化のガイドライン](../../best-practices/optimizing-your-sql-queries.md)SQL エディターでクエリを記述します。 サイドバーの上部にあるボタンを使用すると、で使用できるテーブルと指標のリストを切り替えることができます [!DNL SQL Report Builder] そして、それらをクエリに追加します。 カスタムクエリがニーズに合ったら、レポートを保存して、ダッシュボードからそのデータを書き出すことができます。

>[!NOTE]
>
>データを監査した後で不一致が見つかった場合は、を確認します [サポートへの問い合わせ：データの不一致](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) 次に何をするかの詳細については、サポートトピックを参照してください。
