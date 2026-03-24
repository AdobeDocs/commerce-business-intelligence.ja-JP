---
title: データと更新情報
description: 更新サイクルのステータスを確認する方法を説明します。
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/qT3lojSuve8jHgNVKoJCUW82cN2QK497wFX8NVbptWI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 481
ht-degree: 0%

---

# データと更新情報

* [データが変更された理由](#datachange)
* [定期アップデートと強制アップデートの違いは何ですか？](#regularforcedupdates)
* [更新サイクルに時間がかかるのはなぜですか？](#updatecycletime)
* [更新サイクルの完了時に通知を受け取ることはできますか？](#notifyupdate)
* [&#x200B; [!DNL Google ECommerce]  データがデータベースと異なるのはなぜですか？](#ecommdatabase)
* [データの不一致のトラブルシューティング方法を教えてください。](#datadiscrepancy)

## データが変更された理由 {#datachange}

新しいデータがData Warehouseに同期されるため、チャートの値は1日を通して変化する可能性があります。 また、既存のデータ列の値は、[rechecks](../data-warehouse-mgr/cfg-data-rechecks.md)により変更される可能性があります。 リチェックとは、`open`から`shipped`に移動する注文ステータスなど、データ列の変更された値を検索するプロセスです。

ユーザーの権限設定に応じて、更新サイクルのステータスを確認するには、いくつかの方法[があります](../../best-practices/check-update-cycle.md)。

* **[!UICONTROL Read-Only]と[!UICONTROL Standard] ユーザー** - ページの右上にあるアイコンにカーソルを合わせると、最後のデータポイントがいつプルされたかを確認できます。
* **[!UICONTROL Admin]ユーザー** – 最後のデータポイントとアカウント統合のステータスアイコンを表示できます。 詳細については、**[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**&#x200B;に移動して、現在の更新ステータスと、最後に完了した更新の時刻を確認します。
* **API メソッド** - Update Cycle Status APIを使用して、完了した最新の更新サイクルを取得できます。

更新サイクルのステータスの確認について詳しくは、[更新サイクルのステータスの確認](../../best-practices/check-update-cycle.md)を参照してください。

## 定期アップデートと強制アップデートの違いは何ですか？ {#regularforcedupdates}

定期的な更新は&#x200B;**スケジュール済み** プロセスですが、強制的な更新は&#x200B;**手動プロセスで開始されます**。 ブラックアウト時間（または[!DNL Commerce Intelligence]がデータを更新しない期間）がある場合、強制的に更新すると、ブラックアウト期間の制限を尊重しないサイクルが開始されます。

## 更新サイクルに時間がかかるのはなぜですか？ {#updatecycletime}

更新時間がすでに長くなる要因が数多くあります。 特定の[&#x200B; レプリケーション方法](../data-warehouse-mgr/cfg-replication-methods.md)、[より高いリチェック頻度](../data-warehouse-mgr/cfg-data-rechecks.md)、およびダッシュボードとグラフの数は、ほんの一部の貢献者です。 Adobeでは、更新時間を短縮するために、[一部の設定の再構成](../../best-practices/reduce-update-cycle-time.md)と[分析のためにデータベースを最適化](../../best-practices/opt-db-analysis.md)することをお勧めします。

## 更新サイクルの完了時に通知を受け取ることはできますか？ {#notifyupdate}

更新が進行中の場合、**[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]** ページにリンクがあり、サイクルが完了するとメール通知をリクエストするために使用できます。 更新が進行中でない場合は、更新を強制的に開始するリンクが表示されます。

## [!DNL Google ECommerce] データがデータベースと異なるのはなぜですか？ {#ecommdatabase}

[!DNL Google Analytics]とお客様のデータベースとの間には、様々な理由で不一致が発生する可能性があります。 トラッキングが適切に有効になっていない、シークレットにアクセスしているユーザー、正しく機能していないクリックイベントなどはその一例です。 収益と注文が正しく表示されない場合は、[このトピック &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=ja)を参照して問題を診断してください。

## データの不一致のトラブルシューティング方法を教えてください。 {#datadiscrepancy}

Adobeでは、一貫性のないデータを確認することは、顧客のフラストレーションを招く恐れがあることを認識しています。 [&#x200B; データの不一致チェックリスト &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=ja)または[&#x200B; データ書き出しチュートリアル &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=ja)を使用して、問題を診断してください。 まだ行き詰まっている場合は、[&#x200B; サポートにお問い合わせください](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)。
