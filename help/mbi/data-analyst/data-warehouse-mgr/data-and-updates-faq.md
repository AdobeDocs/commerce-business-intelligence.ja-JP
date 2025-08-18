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
* [データがデ  [!DNL Google ECommerce]  タベースと異なる理由](#ecommdatabase)
* [データの不一致をトラブルシューティングするにはどうすればよいですか？](#datadiscrepancy)

## データが変更された理由 {#datachange}

新しいデータがData Warehouseに同期されるので、グラフの値は 1 日を通して変化する可能性があります。 また、既存のデータ列の値は、[ 再確認 ](../data-warehouse-mgr/cfg-data-rechecks.md) によって変更される場合があります。 再チェックは、注文ステータスが `open` から `shipped` に移動するなど、データ列で変更された値を探すプロセスです。

ユーザーの権限設定に応じて [ 更新サイクルのステータスを確認する ](../../best-practices/check-update-cycle.md) 方法はいくつかあります。

## 通常の更新と強制更新の違いは何ですか？ {#regularforcedupdates}

定期的な更新は **スケジュールされた** プロセスですが、強制更新は **ユーザーによって開始された手動のプロセス** です。 ブラックアウト時間（またはデータを更新 [!DNL Commerce Intelligence] ない期間）がある場合、更新を強制すると、ブラックアウト期間の制限を考慮しないサイクルが開始されます。

## 更新サイクルに時間がかかるのはなぜですか。 {#updatecycletime}

既に更新時間が長くなる原因には数多くの要因があります。 一部の [ レプリケーション方法 ](../data-warehouse-mgr/cfg-replication-methods.md)、[ より高い再チェック頻度 ](../data-warehouse-mgr/cfg-data-rechecks.md)、ダッシュボードとグラフの数は、ほんの一部に過ぎません。 Adobe更新時間を短縮するには、[ 設定の一部を再設定する ](../../best-practices/reduce-update-cycle-time.md) および [ 分析のためのデータベースの最適化 ](../../best-practices/opt-db-analysis.md) をお勧めします。

## 更新サイクルが完了したときに通知を受け取ることはできますか？ {#notifyupdate}

更新が進行中の場合は、サイクルが完了した後にメール通知をリクエストするために使用できるリンクが `Connections` ページに表示されます。

## データがデ [!DNL Google ECommerce] タベースと異なる理由 {#ecommdatabase}

[!DNL Google Analytics] とデータベースの間で不一致が発生する場合は、様々な理由があります。 トラッキングが適切に有効になっていない場合や、匿名ユーザーがアクセスしている場合、クリックイベントが正しく機能していない場合などは、ほんの一例です。 売上高と注文が適切に表示されない場合は、問題を診断するために [ このトピックを参照 ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=ja)。

## データの不一致をトラブルシューティングするにはどうすればよいですか？ {#datadiscrepancy}

Adobeは、一貫性のないデータを見ることがフラストレーションにつながる可能性があることを認識しています。 [ データの相違チェックリスト ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=ja) または [ データの書き出しチュートリアル ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=ja) を使用して、問題を診断してみてください。 まだ問題が解決しない場合は、[ サポートにお問い合わせください ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)。
