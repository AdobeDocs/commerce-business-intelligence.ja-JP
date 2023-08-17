---
title: Onboarding Adobe Commerce Intelligence
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

以下に関するオンボーディングに関する質問： `store` および `database` を設定することで、レポートが正しく設定されていることを確認します。 Adobeは、これらの回答を使用して、お客様の店舗の設定に合わせて正確にカスタマイズされたレポートを提供します。

## ストア設定

- *あなたの店はゲストのチェックアウトを受け入れますか？*  — 選択 **はい** 顧客がアカウントに登録せずにストアから購入を許可する場合。

- `Timezone`  — を選択します。 `timezone` レポートを表示する

- `Currency`  — を選択します。 `currency` お客様の店が運営する

- `Your week starts on...`  — レポートで週の開始日にする曜日を選択します。

- *使用する Commerce のバージョンを教えてください。*  — を選択します。 `currency` お客様の店が運営する

- *あなたの店は EU に本拠を置いていますか？*  — 答えた場合 `Yes` この質問に対して、Adobeは、GDPR に準拠して、Data Warehouseと EU 内のすべてのデータをホストします。

## データベース設定

- `Database name`  — とは *名前 [!DNL MySQL] データベース* コマーストランザクションデータはどこにありますか。

- `Table prefix (optional)` - Commerce データベースに含まれるテーブルの先頭には何かが付いています ( 例： `store_`)? これは通常はそうではありませんが、カスタマイズが可能です。
