---
title: 初回購入までの平均時間レポート
description: 平均初回購入時間レポートの使用方法を説明します。
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 330832e2668024b00edb2b7c49b92bb042bd004a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# 初回購入までの平均時間レポート

多くのAdobeのお客様には、 `Average time to first purchase`：ユーザーのグループ登録日から初回購入日までの平均時間を表示します。 時間が現在に近づくにつれ、データはほぼ常に下方に傾く。

![初回注文までの平均時間](../../assets/average-time-to-first-order.png)

これは、新しいお客様が、参加日から 1 ヶ月以上経った購入を生み出す機会をまだ持っていないためです。 一度も購入したことのないユーザーは（購入するまで）含まれないので、新しいグループの顧客の平均は下方向に傾きます。

この指標を見る他の潜在的な方法がいくつかあり、バイアスが少なくなります。 1 つの例を見てみましょう。

## 例： `cohort` 一次分析

グラフを表示できます。 `Users` ダッシュボード名 `Time to first order cohort`. このレポートは、 `Distinct buyers` 指標、ユーザーをグループ化 `cohort` 登録の週または月、および割合 ( `0` および `1`) の分類を含めることをお勧めします。

グラフには、2014 年 12 月に登録したユーザーの場合、 `0.56` ( または `56%`) が月 2 日（例：2015 年 1 月）に初回注文しました。

コホート分析は、ユーザーのアクティブ化率の推移を示す良い指標です。 このグラフがフラット化またはプラトー化し始め、まだ 100%の購入者へのコンバージョンに近づいていない場合は、電子メールキャンペーンを通じて残りのユーザーをアクティブ化する時間が来る可能性があります。
