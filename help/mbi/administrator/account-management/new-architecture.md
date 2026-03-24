---
title: 新しいアーキテクチャ
description: 新しいアーキテクチャに移行するメリットをご紹介します。
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
TQID: https://experienceleague.adobe.com/EtbKFT7OKaTZQ55XNz0NwpxQNSXyazk47dGwKhETNjM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 390
ht-degree: 0%

---

# 新しいアーキテクチャ

[!DNL Adobe Commerce Intelligence]製品チームとエンジニアリング チームは、この1年間、要求の高い改善を可能な限り大規模に行うことに注力してきました。 Adobeは、これらの改良を実現する新しい[!DNL Commerce Intelligence]製品アーキテクチャの提供を発表できることを嬉しく思います。

## 新しいアーキテクチャの利点

* Data Warehouseで、SQLを使用した計算列など、列のタイプを作成します。
* 新しい列はすぐに使用できます。
* データ待ち時間が大幅に改善されます。

## 技術的利点

主な違いは上記に記載されていますが、主な変更は、更新サイクル中に計算が実行される方法です。 計算は、更新のたびに各列で実行されなくなりました。代わりに、Visual Report Builderからオンデマンドで実行されます。

### 新しいアーキテクチャへの移行

アカウントの基本的な構成が異なるため、Data Warehouseまたはレポートを新しいアーキテクチャアカウントに移行する自動プロセスはありません。 新しいアーキテクチャに移行するには、既存のアカウントを再実装する必要があります。

### 新しいアーキテクチャへの移行コスト

追加費用なし！ Adobeでは、この新しいアカウントを作成して、少なくとも1か月無料で再実装を開始できます。 これにより、両方のアカウントを開設する時間を確保できるため、より簡単に再実装を行うことができ、チームのサービスにギャップが生じないようにすることができます。

### 新しいアーキテクチャでアカウントを再実装するのに必要な時間

再実装にかかる時間は、再構築する内容によって異なります。 Adobeでは、既存のアカウントで次の手順を実行して、再実装に関する情報を取得することをお勧めします。

* レポート/ダッシュボードのコアセットを特定する。
* レポートを作成するために必要な指標とディメンションを特定します。
* 指標とディメンションを再作成するために必要な列を特定します。

コアレポートを再構築するためには、新しいアーキテクチャであるData Warehouseと同期する必要があるデータを把握できます。

### ヘルプの取得

[!DNL Adobe Commerce Intelligence] [&#x200B; サービスチーム &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)は、追加費用で再実装を実行できます。 [Adobe アカウントチーム &#x200B;](../../guide-overview.md#Submitting-a-Support-Ticket)に連絡し、新しいアカウントでの作成を優先するダッシュボード/レポートのリストを提供する準備をしてください

### 既存のアーキテクチャを維持

これらの機能が重要でない場合は、既存のアカウントを使用することができます。 既存アカウントを維持するための追加費用は発生しません。 Adobeでは、変更がなくても引き続きこれらのアカウントをサポートします。
