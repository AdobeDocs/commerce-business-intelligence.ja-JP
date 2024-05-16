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

データベーステーブルには、変更可能な値を持つデータ列を使用できます。 例： **注文件数** という列がある可能性があります。 **ステータス**. 注文が最初にデータベースに書き込まれると、ステータス列に値が含まれる場合があります `pending`. この順序は、で複製されます。 [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) （これにより） `pending` の値。

変更可能な列は次でなければなりません： [更新された値を再チェック](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) 時間が経つにつれて。 デフォルトでは [!DNL Commerce Intelligence] 更新時にこれらの列を再チェックしますが、再チェックおよびレプリケートされるデータが大量にある場合は、更新時間に悪影響を与える可能性があります。 Adobeでは、更新ごとに再チェックを実行する代わりに、再チェックの頻度を日次、週次、月次のいずれかに設定することをお勧めします。

## 増分レプリケーション方法の使用

前述のように、更新時間の長さは、再確認およびレプリケートが必要なデータの量に直接相関します。 [増分レプリケーション方法](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) を使用すると、更新サイクル中に処理されるデータ量を大幅に削減できます。 Adobeでは、可能な限りこれらの手段を使用するか、増分方式をサポートするようにデータベースを変更することをお勧めします。

## ダッシュボードから未使用のグラフを削除

更新サイクルの終了時、 [!DNL Commerce Intelligence] すべてのグラフに対してキャッシュ操作を実行します。 キャッシュにはデータが格納されるため、今後の情報リクエストはより迅速に完了することができます。 対象： [!DNL Commerce Intelligence]つまり、グラフを読み込むたびにデータをクエリする必要がないので、ダッシュボードはすぐに読み込まれます。

以降 [!DNL Commerce Intelligence] は、ダッシュボード内で見つかったグラフに対してのみキャッシュ操作を実行し、ダッシュボードから未使用のグラフを削除すると、更新時間が短縮されます。 同じグラフが複数のダッシュボードに存在する可能性があることに注意してください。未使用のグラフも削除されていることをチームに確認してください。

>[!NOTE]
>
>ダッシュボードからグラフを削除しても、グラフは削除されません。 次のことができます [いつでも戻す](../data-user/dashboards/add-charts-dashboard.md).

## 分析用にデータベースを最適化

再確認の頻度、レプリケーションの方法、グラフの有用性を再評価する以外に、次のこともできます [分析用にデータベースを最適化](../best-practices/opt-db-analysis.md).

## まとめ

これらの推奨事項を実装しても更新時間が遅いと思われる場合は、 [サポートチームにお問い合わせください](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
