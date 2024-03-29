---
title: 更新サイクル時間の短縮
description: 更新サイクル時間を短縮する方法を説明します。
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# 更新サイクル処理時間の短縮

[!DNL Adobe Commerce Intelligence] は、1 日を通じてデータベースと同期して新しいデータをレプリケートし、ダッシュボードに常に最新の情報が表示されるようにします。

多くの要因が、既に長時間の更新時間を増やす可能性があります。 特定のレプリケーション方法、再確認頻度の増加、ダッシュボードとグラフの数が寄与しているのは、わずかです。 このトピックでは、更新時間を短縮するためのベストプラクティスをいくつか説明します。

## 再確認頻度を減らす

データベーステーブルには、値が変更可能なデータ列が存在する場合があります。 例えば、 **注文件数** という列があるかもしれないテーブル **ステータス**. 注文が最初にデータベースに書き込まれるとき、ステータス列に値が含まれている場合があります `pending`. 注文は、 [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) この `pending` の値です。

変更可能な列を指定する必要があります [更新された値に対して再チェックしました](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 長期間。 デフォルトでは、 [!DNL Commerce Intelligence] 更新のたびにこれらの列を再チェックしますが、再チェックおよびレプリケートされるデータが大量にある場合は、更新時間に悪影響を与える可能性があります。 Adobeでは、更新のたびに再確認を実行する代わりに、再確認の頻度を日別、週別、月別に設定することをお勧めします。

## 増分レプリケーションメソッドの使用

前述のように、長い更新時間は、再チェックとレプリケートが必要なデータの量に直接関連付けられます。 [増分レプリケーション方法](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) は、更新サイクル中に処理されるデータの量を大幅に削減できます。 可能な場合、Adobeは、増分メソッドをサポートするように、これらのメソッドを使用するか、データベースを変更することをお勧めします。

## ダッシュボードから未使用のグラフを削除

更新サイクルの終了時に、 [!DNL Commerce Intelligence] は、すべてのグラフに対してキャッシュ操作を実行します。 キャッシュにはデータが格納されるので、今後の情報のリクエストをより迅速に完了できます。 In [!DNL Commerce Intelligence]つまり、グラフは読み込むたびにデータに対してクエリを実行する必要がないので、ダッシュボードの読み込みは迅速に行われます。

次以降 [!DNL Commerce Intelligence] は、ダッシュボードで見つかったグラフに対してのみキャッシュ操作を実行します。未使用のグラフをダッシュボードから削除すると、更新時間が短縮されます。 同じグラフが複数のダッシュボードに存在する場合があることに注意してください。チームに問い合わせて、使用されていないグラフも削除したかどうかを確認してください。

>[!NOTE]
>
>ダッシュボードからグラフを削除しても、グラフは削除されません。 以下が可能です。 [いつでも付け直す](../data-user/dashboards/add-charts-dashboard.md).

## 分析用にデータベースを最適化する

再確認頻度、レプリケーション方法、グラフの有用性を再評価する以外に、次のこともできます。 [分析用にデータベースを最適化する](../best-practices/opt-db-analysis.md).

## 折り返し

これらのレコメンデーションを実装した後でも、更新時間が長く見える場合は、 [サポートチームに連絡する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
