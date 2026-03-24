---
title: 最初の購入までの平均時間レポート
description: 初回購入までの平均時間レポートの使用方法を説明します。
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/LWbb4E4IMPQd-hUpsylSGt4lgrrvYI1VUhmovjvcfu4
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
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 258
ht-degree: 0%

---

# 最初の購入までの平均時間レポート

多くのAdobeのお客様は、ユーザーのグループの登録日から最初の購入日までの平均時間を示す`Average time to first purchase`という名前の指標とグラフを使用しています。 データは、時間が現在に近づくにつれて、ほぼ常に下に傾きます。

![最初の注文までの平均時間](../../assets/average-time-to-first-order.png)

これは、これらの新しい顧客が、結合日から1か月以上経過した購入履歴をまだ生成していないためです。 購入したことがない利用者は、（購入するまで）まったく含まれないため、新しい顧客グループでは平均的に下方に偏ります。

この指標を見る方法として、他にもいくつかの潜在的な方法があり、それがバイアスを引き起こします。 その一例をご紹介します。

## 例：最初の注文の`cohort`分析を実行する

`Users` ダッシュボードに`Time to first order cohort`という名前のグラフがある可能性があります。 このレポートでは、`Distinct buyers`指標を使用して、ユーザーを登録後`cohort`週間または数ヶ月でグループ化し、登録後の数週間または数ヶ月に最初の購入を行ったユーザーの比率（`0`から`1`の間）を表示します。

このグラフは、2014年12月に登録したユーザーについて、`0.56` （または`56%`）が最初の注文を2か月（例：2015年1月）までに行ったことを示す場合があります。

このコホート分析は、時間の経過に伴うユーザーのアクティブ化率を示す優れた指標です。 このグラフが平坦化または停滞し始め、それでも購入者へのコンバージョン率が100%に近くない場合は、メールキャンペーンで残りのユーザーをアクティブ化する時期が来ている可能性があります。
