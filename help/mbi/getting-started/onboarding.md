---
title: Adobe Commerce Intelligence のオンボーディング
description: Adobe Commerce Intelligence のオンボーディングについて説明します。
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# オンボーディング [!DNL Adobe Commerce Intelligence]

に関連するオンボーディングの質問 `store` および `database` 設定レポートを正しく設定していることを確認します。 これらの回答を使用して、Adobeはストアの設定に合わせて正確に調整されたレポートを提供します。

## ストアの設定

- *お店はゲストのチェックアウトを受け付けていますか。*  – を選択 **はい** 顧客がアカウントを登録せずにストアから購入することを許可している場合。

- `Timezone`  – を選択します `timezone` にレポートを表示します。

- `Currency`  – を選択します `currency` その店が営業している。

- `Your week starts on...` - レポートで週の開始日とする曜日を選択します。

- *Commerceのどのバージョンを使用していますか？*  – を選択します `currency` その店が営業している。

- *お店は欧州連合に拠点を置いていますか？*  – 次の場合： `Yes` この質問に対しては、Adobeは、GDPR に準拠して、Data Warehouseとすべてのデータを欧州連合（EU）でホストします。

## データベース設定

- `Database name`  – とは *の名前 [!DNL MySQL] データベース* Commerce トランザクションデータの格納場所

- `Table prefix (optional)`  – は、Commerce データベースに含まれるテーブルの先頭に何かを付加したものです（例： `store_`）? これは通常は当てはまらないが、カスタマイズが可能である。
