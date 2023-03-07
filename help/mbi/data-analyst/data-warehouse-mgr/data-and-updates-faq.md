---
title: データと更新情報
description: 更新サイクルのステータスを確認する方法を説明します。
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 0%

---

# データと更新情報

* [データが変更された理由](#datachange)
* [通常の更新と強制更新の違いは何ですか？](#regularforcedupdates)
* [更新サイクルに長い時間がかかるのはなぜですか？](#updatecycletime)
* [更新サイクルが完了したら通知を受け取ることはできますか？](#notifyupdate)
* [の理由 [!DNL Google ECommerce] データベースに異なるデータがある場合](#ecommdatabase)
* [データの相違をトラブルシューティングする方法を教えてください。](#datadiscrepancy)

## データが変更された理由 {#datachange}

グラフの値は、Data Warehouseに新しいデータが同期されるので、1 日を通じて変化する可能性があります。 また、既存のデータ列の値は、 [再チェック](../data-warehouse-mgr/cfg-data-rechecks.md). 再確認とは、データ列で変更された値（注文ステータスが次の場所から移動した場合など）を検索するプロセスです。 `open` から `shipped`.

いくつかの異なる方法があります [更新サイクルのステータスを確認するには](../../best-practices/check-update-cycle.md)に設定されます。

## 通常の更新と強制更新の違いは何ですか？ {#regularforcedupdates}

定期的な更新は次のとおりです **予定** 強制更新中のプロセス **自分が開始した手動プロセス**. ブラックアウト時間がある場合、または [!DNL MBI] はデータを更新しないでください。更新を強制すると、ブラックアウト期間の制限を考慮しないサイクルが開始されます。

## 更新サイクルに長い時間がかかるのはなぜですか？ {#updatecycletime}

多くの要因が、既に長時間の更新時間を増やす可能性があります。 特定 [レプリケーションメソッド](../data-warehouse-mgr/cfg-replication-methods.md), [再検査頻度の増加](../data-warehouse-mgr/cfg-data-rechecks.md)ダッシュボードとグラフの数はほんの数の寄稿者に過ぎません。 Adobeが推奨 [設定の一部の再設定](../../best-practices/reduce-update-cycle-time.md) および [分析用にデータベースを最適化中](../../best-practices/opt-db-analysis.md) 更新時間を短縮する。

## 更新サイクルが完了したら通知を受け取ることはできますか？ {#notifyupdate}

更新が進行中の場合、 `Connections` サイクルが完了した後に電子メール通知をリクエストするために使用できるページ。

## の理由[!DNL Google ECommerce]データベースに異なるデータがある場合 {#ecommdatabase}

の不一致 [!DNL Google Analytics] そしてあなたのデータベースは様々な理由で生じる可能性がある トラッキングが適切に有効になっていない場合、匿名を訪問し、クリックイベントが正しく機能しない場合の例はいくつかあります。 売上高と注文が正しく表示されない場合、 [この記事を使用](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=en) 問題を診断する。

## データの相違をトラブルシューティングする方法を教えてください。 {#datadiscrepancy}

Adobeは、一貫性のないデータを見ると不満を招く可能性があることを認識しています。 その場合は、 [データ不一致チェックリスト](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=en) または [データ書き出しのチュートリアル](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=en) 問題を診断する。 もしまだつまずいていれば [連絡先サポート](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
