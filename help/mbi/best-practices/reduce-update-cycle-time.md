---
title: 更新サイクル時間の短縮
description: 更新サイクル時間を短縮する方法について説明します。
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# 更新サイクルの処理時間を短縮

[!DNL Adobe Commerce Intelligence] は、1 日を通じてデータベースと同期して新しいデータをレプリケートし、ダッシュボードに常に最新の情報を表示できるようにします。

既に更新時間が長くなる原因には、多くの要因が考えられます。 特定のレプリケーション方法、再確認頻度の向上、ダッシュボードとグラフの数は、ほんの一部に過ぎません。 このトピックでは、更新時間を短縮するためのベストプラクティスについて説明します。

## 再チェックの頻度を減らす

データベーステーブルには、変更可能な値を持つデータ列を使用できます。 例えば、**orders** テーブルには、**status** という列がある場合があります。 注文が最初にデータベースに書き込まれると、ステータス列に値 `pending` が含まれる場合があります。 注文は [0&rbrace;Data Warehouse&rbrace; でこの &#x200B;](../data-analyst/data-warehouse-mgr/tour-dwm.md) 値でレプリケートされます。`pending`

変更可能な列は、時間の経過と共に [&#x200B; 更新された値について再チェック &#x200B;](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) される必要があります。 デフォルト [!DNL Commerce Intelligence] は、更新時にこれらの列を再チェックしますが、再チェックおよびレプリケートされるデータが大量にある場合は、更新時間に悪影響を与える可能性があります。 Adobeでは、すべての更新で再チェックを実行する代わりに、再チェックの頻度を日単位、週単位または月単位に設定することをお勧めします。

## 増分レプリケーション方法の使用

前述のように、更新時間の長さは、再確認およびレプリケートが必要なデータの量に直接相関します。 [&#x200B; 増分レプリケーション方法 &#x200B;](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) を使用すると、更新サイクル中に処理されるデータ量を大幅に削減できます。 可能な限り、Adobeでは、増分処理をサポートするために、これらの手法を使用するか、データベースを変更することをお勧めします。

## ダッシュボードから未使用のグラフを削除

更新サイクルの最後に、[!DNL Commerce Intelligence] はすべてのグラフに対してキャッシュ操作を実行します。 キャッシュにはデータが格納されるため、今後の情報リクエストはより迅速に完了することができます。 [!DNL Commerce Intelligence] では、グラフを読み込むたびにデータをクエリする必要がないので、ダッシュボードはすぐに読み込まれます。

[!DNL Commerce Intelligence] はダッシュボード内で見つかったグラフのキャッシュ操作のみを実行するので、ダッシュボードから未使用のグラフを削除すると、更新時間が短縮されます。 同じグラフが複数のダッシュボードに存在する可能性があることに注意してください。未使用のグラフも削除されていることをチームに確認してください。

>[!NOTE]
>
>ダッシュボードからグラフを削除しても、グラフは削除されません。 [&#x200B; いつでも追加して戻す &#x200B;](../data-user/dashboards/add-charts-dashboard.md) ことができます。

## 分析用にデータベースを最適化

再確認の頻度、レプリケーションの方法、グラフの有用性を再評価する以外に、[&#x200B; 分析のためにデータベースを最適化 &#x200B;](../best-practices/opt-db-analysis.md) することもできます。

## まとめ

これらの推奨事項を実装しても更新時間が遅いと思われる場合は、[&#x200B; サポートチームにお問い合わせください &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)。
