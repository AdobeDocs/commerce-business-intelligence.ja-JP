---
title: SQL Report Builderの操作
description: SQL Report Builderを使用してデータと指標を監査し、結果をローカルデータベースのデータと比較できるようにする方法について説明します。
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
role: Admin, Developer, User
feature: Reports, Data Warehouse Manager, SQL Report Builder
TQID: https://experienceleague.adobe.com/7Yx7Kpir-xjz5TPuajN7CFsLjWAbY0AT3bKtBabA5Wk
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 507
ht-degree: 0%

---

# [!DNL SQL Report Builder]

[!DNL SQL Report Builder]は、主に新しいレポートを作成し、分析を繰り返すために使用されますが、データと指標を効果的に監査するためにも使用できます。 次の情報では、[!DNL SQL Report Builder]を使用してデータと指標を監査し、結果をローカルデータベースのデータと比較する方法について説明します。

## 指標のクエリ

開始するには、[!DNL SQL Report Builder]に移動して&#x200B;**[!UICONTROL Report Builder > SQL Report Builder > Create Report]**&#x200B;を開きます。 [!DNL SQL] エディターのサイドバーを使用して、指標にカーソルを合わせて&#x200B;**[!UICONTROL Insert]**&#x200B;をクリックすると、指標をクエリに直接挿入できます。 これにより、その指標のクエリ定義がエディターに追加されます。 定義には、次のコンポーネントが含まれます。

- **指標の操作**&#x200B;が実行されています。以下の例では、`SUM()`が示しています。
- 指標が作成される&#x200B;**の** テーブルは、`FROM`句で示されます。
- 指標に追加された&#x200B;**フィルター（およびフィルターセット）**&#x200B;はすべて、次の例の`WHERE`句で示されています。
- データを注文する&#x200B;**タイムスタンプ** （年、月）のコンポーネント。以下の例の`ORDER BY`句で示されます。

クエリをより明確に表示するには、クエリフィールドでの表示方法を再形式できます。 準備ができたら、`Run Query`を選択します。 結果は、クエリの下のレポートパネルにテーブルとして入力されます。

![SQL クエリの実行と結果の表示のアニメーション化されたデモ &#x200B;](../../assets/run-query-results.gif)

## クエリの制限

特定の不一致またはデータのセットを特定する場合は、クエリを特定のサンプルに限定して、ローカルデータベースと照合する必要があります。 これを行うには、目的の制限に合わせてクエリを編集します。 次の例では、2013年1月1日以降の収益のみを含めるようにクエリを制限しています。 クエリを更新したら、もう一度&#x200B;**[!UICONTROL Run Query]**&#x200B;を選択して結果を更新します。

![&#x200B; フィルターを使用したクエリ制限のアニメーション化されたデモ &#x200B;](../../assets/restricting-query.gif)

## 保存とエクスポート

レポートがニーズを満たしたら、レポートに明確な名前を付け、**[!UICONTROL Save]**&#x200B;をクリックし、保存するレポートのタイプとダッシュボードを選択します。 指標を監査する場合、Adobeでは、レポートを`Table`として保存し、テストダッシュボードに保存することをお勧めします。

レポートが保存されたら、`Go to Dashboard`を選択して、そのダッシュボードに移動します。 そこから、レポートを見つけて、**[!UICONTROL Options gear > Full `.csv`Export]**&#x200B;または&#x200B;**[!UICONTROL Full Excel Export]**&#x200B;を選択してデータを書き出すことができます。

![&#x200B; ダッシュボードデータの書き出しのアニメーション化されたデモ &#x200B;](../../assets/export-dboard-data.gif)

## カスタムクエリ

また、カスタムクエリを作成し、結果を書き出して、ローカルデータベースと比較することもできます。 クエリ最適化[の](../../best-practices/optimizing-your-sql-queries.md) ガイドラインに従って、SQL エディターにクエリを記述します。 サイドバーの上部にあるボタンを使用して、[!DNL SQL Report Builder]で使用できるテーブルと指標のリストを切り替え、クエリに追加できます。 カスタムクエリがニーズに合ったら、レポートを保存し、そのデータをダッシュボードから書き出すことができます。

>[!NOTE]
>
>データを監査した後に不一致が見つかった場合は、[&#x200B; サポートへの連絡：データの不一致](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html) サポートのトピックで、次に行う処理について詳しく確認してください。
