---
title: データと更新情報
description: 更新サイクルのステータスを確認する方法を説明します。
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# データと更新情報

* [データが変更された理由](#datachange)
* [通常の更新と強制更新の違いは何ですか？](#regularforcedupdates)
* [更新サイクルに時間がかかるのはなぜですか。](#updatecycletime)
* [更新サイクルが完了したときに通知を受け取ることはできますか？](#notifyupdate)
* [の理由 [!DNL Google ECommerce] データがデータベースと異なる場合](#ecommdatabase)
* [データの不一致をトラブルシューティングするにはどうすればよいですか？](#datadiscrepancy)

## データが変更された理由 {#datachange}

新しいデータがData Warehouseに同期されるので、グラフの値は 1 日を通して変化する可能性があります。 また、既存のデータ列の値は、次の理由で変更される可能性があります。 [再チェック](../data-warehouse-mgr/cfg-data-rechecks.md). 再チェックは、注文ステータスの移動など、データ列内の変更された値を探すプロセスです `open` 対象： `shipped`.

いくつかの異なる方法があります [更新サイクルのステータスを確認するには](../../best-practices/check-update-cycle.md)ユーザーの権限設定に応じて調整します。

## 通常の更新と強制更新の違いは何ですか？ {#regularforcedupdates}

定期的なアップデートは次のとおりです **スケジュール** 強制更新中のプロセス **手動プロセスの開始**. ブラックアウト時間（または次の条件を満たす期間）がある場合 [!DNL Commerce Intelligence] はデータを更新しないでください）。更新を強制すると、ブラックアウト期間の制限を考慮しないサイクルが開始されます。

## 更新サイクルに時間がかかるのはなぜですか。 {#updatecycletime}

既に更新時間が長くなる原因には数多くの要因があります。 特定 [レプリケーション方法](../data-warehouse-mgr/cfg-replication-methods.md), [再検査頻度の増加](../data-warehouse-mgr/cfg-data-rechecks.md)、およびダッシュボードとグラフの数は、ほんの一部です。 Adobeのお勧め [一部の設定の再設定](../../best-practices/reduce-update-cycle-time.md) および [分析のためのデータベースの最適化](../../best-practices/opt-db-analysis.md) 更新時間を短縮する。

## 更新サイクルが完了したときに通知を受け取ることはできますか？ {#notifyupdate}

更新中の場合は、にリンクがあります `Connections` サイクルが完了した後にメール通知をリクエストするために使用できるページ。

## の理由[!DNL Google ECommerce]データがデータベースと異なる場合 {#ecommdatabase}

間の不一致 [!DNL Google Analytics] また、データベースは様々な理由で発生する可能性があります。 トラッキングが適切に有効になっていない場合や、匿名ユーザーがアクセスしている場合、クリックイベントが正しく機能していない場合などは、ほんの一例です。 売上高と注文件数が適切に表示されない場合、 [このトピックを参照してください](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) 問題を診断する。

## データの不一致をトラブルシューティングするにはどうすればよいですか？ {#datadiscrepancy}

Adobeは、一貫性のないデータを見ることがフラストレーションにつながる可能性があることを認識しています。 を使用してみてください [データ不一致チェックリスト](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html) または [データ書き出しのチュートリアル](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html) 問題を診断します。 まだ足がつまずいているなら、 [サポートに連絡する](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
