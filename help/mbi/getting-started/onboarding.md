---
title: オンボーディング
description: オンボーディングについて説明します。
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 0%

---

# オンボーディング

以下に関するオンボーディングに関する質問： `store` および `database` を設定することで、レポートが正しく設定されていることを確認します。 Adobeは、これらの回答を使用して、お客様の店舗の設定に合わせて正確にカスタマイズされたレポートを提供します。

## ストア設定

- *あなたの店はゲストのチェックアウトを受け入れますか？*  — 選択 **はい** 顧客がアカウントに登録せずにストアから購入を許可する場合。

- `Timezone` - `timezone` レポートを表示する

- `Currency` - `currency` お客様の店が運営する

- `Your week starts on...`  — レポートで週の開始日にする曜日を選択します。

- *使用する Commerce のバージョンを教えてください。* - `currency` お客様の店が運営する

- *あなたの店は EU に本拠を置いていますか？*  — 答えた場合 `Yes` この質問に対して、Adobeは、GDPR に準拠して、Data Warehouseと EU 内のすべてのデータをホストします。

## データベース設定

- `Database name`  — とは *MySQL データベースの名前* コマーストランザクションデータはどこにありますか。

- `Table prefix (optional)` - Commerce データベースに含まれるテーブルの先頭には何かが付いています ( 例： `store_`)? これは通常はそうではありませんが、カスタマイズが可能です。
