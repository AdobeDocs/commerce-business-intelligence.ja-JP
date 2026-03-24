---
title: 更新サイクルを短縮
description: 更新サイクル時間を短縮する方法を説明します。
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/DFlzL9E95teiWI31j7qWRU8Ab6GkbFX7iPPdaxGq48A
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 0%

---

# 更新サイクルの処理時間を短縮

[!DNL Adobe Commerce Intelligence]は、1日中データベースと同期して新しいデータをレプリケートし、ダッシュボードに常に最新の情報が表示されるようにします。

更新時間がすでに長くなる要因が数多くあります。 特定のレプリケーション方法、より高い再チェック頻度、ダッシュボード数やチャート数などは、ほんの一部の要因に過ぎません。 ここでは、更新時間を短縮するためのベストプラクティスについて説明します。

## リチェック頻度を減らす

データベーステーブルには、変更可能な値を持つデータ列を含めることができます。 例えば、**orders** テーブルには、**status**&#x200B;という列がある場合があります。 注文が最初にデータベースに書き込まれると、ステータス列に値`pending`が含まれる場合があります。 注文は、この[値で](../data-analyst/data-warehouse-mgr/tour-dwm.md)Data Warehouse`pending`にレプリケートされます。

変更可能な列は、更新された値[に対して時間の経過とともに](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md)再チェックする必要があります。 デフォルトでは、[!DNL Commerce Intelligence]は更新のたびに列を再チェックしますが、再チェックしてレプリケートするデータの量が多い場合、更新時間に悪影響を与える可能性があります。 Adobeでは、更新のたびにリチェックを実行するのではなく、リチェック頻度を日単位、週単位、月単位に設定することをお勧めします。

## 増分レプリケーション方法の使用

前述したように、更新時間の長さは、データの再チェックとレプリケートが必要な量に直接関係しています。 [増分レプリケーション方法](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md)は、更新サイクル中に処理されるデータ量を大幅に削減できます。 可能であれば、Adobeでは、これらのメソッドを使用するか、増分方式をサポートするためにデータベースを修正することをお勧めします。

## 未使用のチャートをダッシュボードから削除

更新サイクルの終了時に、[!DNL Commerce Intelligence]はすべてのグラフに対してキャッシュ操作を実行します。 キャッシュにはデータが保存されるため、今後の情報要求をより迅速に完了できます。 [!DNL Commerce Intelligence]では、チャートが読み込まれるたびにデータをクエリする必要がないため、ダッシュボードの読み込みが速くなります。

[!DNL Commerce Intelligence]は、ダッシュボード内のチャートに対してのみキャッシュ操作を実行するため、ダッシュボードから未使用のチャートを削除すると、更新時間が短縮されます。 同じチャートが複数のダッシュボードに存在する場合もあることに留意してください。チームに連絡して、未使用のチャートも削除したことを確認してください。

>[!NOTE]
>
>ダッシュボードからグラフを削除しても、グラフは削除されません。 [いつでも追加できます](../data-user/dashboards/add-charts-dashboard.md)。

## 分析のためのデータベースの最適化

再チェック頻度、レプリケーション方法、およびチャートの有用性を再評価することに加えて、分析のためにデータベースを[最適化することもできます](../best-practices/opt-db-analysis.md)。

## まとめ

これらの推奨事項を実装しても更新時間が遅いと思われる場合は、[&#x200B; サポートチームにお問い合わせください](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)。
