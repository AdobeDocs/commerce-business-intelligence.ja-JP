---
title: Adobe Commerce Intelligenceの導入
description: Adobe Commerce Intelligenceのオンボーディングについて詳しく見る。
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/36wmj-7QyDdemBWFwHTf1NJkd4H06tED9FZPqhFz8eg
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: b5f00040-57a0-4a6d-a39e-383b1936c2c9id: f42e0a1a-0d79-488d-a83f-f2c30672b137
subfeature_v2: id: bcbf87e7-9b75-4596-bffe-0f376b4c73a7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 194
ht-degree: 0%

---

# オンボーディング [!DNL Adobe Commerce Intelligence]

`store`と`database`の設定に関するオンボーディングの質問では、レポートを正しく設定していることを確認します。 これらの質問に答えて、Adobeでは、ストアの設定に合わせて正確にカスタマイズされたレポートを提供します。

## ストア設定

- *お客様のストアはゲストチェックアウトを受け付けていますか？* – 顧客がアカウントに登録せずにストアから購入できるようにする場合は、**yes**&#x200B;を選択します。

- `Timezone` - レポートを表示する`timezone`を選択します。

- `Currency` - ストアが操作する`currency`を選択します。

- `Your week starts on...` - レポートで週の開始日にする曜日を選択します。

- *どのバージョンのCommerceをお使いですか？* - ストアが操作する`currency`を選択します。

- *お客様の店舗は欧州連合に拠点を置いていますか？* – この質問に`Yes`と回答した場合、AdobeはGDPRに準拠して、Data Warehouseとすべてのデータを欧州連合でホストします。

## データベース設定

- `Database name` - Commerce トランザクションデータが格納されている&#x200B;*データベース [!DNL MySQL]の*&#x200B;名を教えてください。

- `Table prefix (optional)` - Commerce データベースに含まれるテーブルには、何か（例：`store_`）が先頭に付いていますか？ これは通常はそうではありませんが、カスタマイズして行うことができます。
