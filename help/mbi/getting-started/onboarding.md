---
title: オンボーディング
description: オンボーディングについて説明します。
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---

# オンボーディング

以下に関するオンボーディングに関する質問： `store` および `database` 設定により、レポートが正しく設定されていることを確認します。 これらの回答を活用して、お客様の店舗の設定に合わせて適切にカスタマイズされたレポートを配信します。

## ストア設定

- *あなたの店はゲストのチェックアウトを受け入れますか？*  — 選択 **はい** 顧客がアカウントに登録せずにストアから購入を許可する場合。

- `Timezone` - `timezone` レポートを表示する

- `Currency` - `currency` お客様の店が運営する

- `Your week starts on...`  — レポートで週の開始日にする曜日を選択します。

- *使用する Commerce のバージョンを教えてください。* - `currency` お客様の店が運営する

- *あなたの店は EU に本拠を置いていますか？*  — 答えた場合 `Yes` この質問に対しては、GDPR に準拠して、お客様のData Warehouseとすべてのデータを欧州連合でホストします。

## データベース設定

- `Database name`  — とは *MySQL データベースの名前* コマーストランザクションデータはどこにありますか。

- `Table prefix (optional)` - Commerce データベースに含まれるテーブルの先頭には何かが付いています ( 例： `store_`)? これは通常はそうではありませんが、カスタマイズが可能です。
