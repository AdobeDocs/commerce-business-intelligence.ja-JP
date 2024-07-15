---
title: Adobe Commerce Intelligenceのオンボード
description: Adobe Commerce Intelligenceのオンボーディングについて説明します。
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Onboarding [!DNL Adobe Commerce Intelligence]

`store` と `database` の設定に関連するオンボーディングの質問により、レポートを正しく設定していることを確認します。 これらの回答を使用して、Adobeはストアの設定に合わせて正確に調整されたレポートを提供します。

## ストアの設定

- *お店ではゲストのチェックアウトは受け付けていますか？* - アカウントを登録せずに顧客がストアから購入できるようにする場合は、「**はい**」を選択します。

- `Timezone` - レポートの表示 `timezone` を選択します。

- `Currency` - ストアが動作する `currency` を選択します。

- `Your week starts on...` - レポートで週の開始日とする曜日を選択します。

- *Commerceのどのバージョンを使用していますか？* - ストアが動作する `currency` を選択します。

- *貴社の店舗は EU に拠点を置いていますか？* – この質問に対して `Yes` と答えた場合は、GDPR に準拠して、AdobeがData Warehouseとすべてのデータを欧州連合でホストします。

## データベース設定

- `Database name` - Commerce トランザクションデータが格納されている [!DNL MySQL] データベースの *名前* は何ですか？

- `Table prefix (optional)` - Commerce データベースに含まれるテーブルの先頭に何か付加はありますか（例：`store_`）? これは通常は当てはまらないが、カスタマイズが可能である。
