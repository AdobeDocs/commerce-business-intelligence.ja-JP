---
title: 新しいアーキテクチャ
description: 新しいアーキテクチャに移行するメリットについて説明します。
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
source-git-commit: ddda796c9f32d22b1d679fc245eb11b92cd491cf
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# 新しいアーキテクチャ

[!DNL Adobe Commerce Intelligence] 製品チームとエンジニアリングチームは、昨年最も抜本的で要望の多い改善を実現することに重点を置いています。 Adobeは、新しいのリリースをお知らせします [!DNL Commerce Intelligence] これらの改善を実現する製品アーキテクチャ。

## 新しいアーキテクチャのメリット

* SQL を使用した計算列を含む、Data Warehouse内の列のタイプを作成します。
* 新しい列はすぐに使用できるようになります。
* データ待ち時間が大幅に改善されました。

## 技術的メリット

主な違いは上記の通りですが、主な変更点は更新サイクル中の計算の実行方法です。 更新のたびに、すべての列で計算が実行されることはなくなり、代わりにビジュアルReport Builderからオンデマンドで計算が実行されます。

### 新しいアーキテクチャへの移行

アカウントは基本的に異なる方法で作成されるので、Data Warehouseやレポートを新しいアーキテクチャアカウントに自動的に移行するプロセスはありません。 新しいアーキテクチャに移行するには、既存のアカウントを再実装する必要があります。

### 新しいアーキテクチャへの移行にかかるコスト

追加コストはありません。 Adobeでは、この新しいアカウントを作成して再実装を開始します。このアカウントは少なくとも 1 か月間無料です。 これにより、両方のアカウントを開く時間を確保できるので、再実装をより簡単に実行でき、チームのサービスにギャップが生じなくなります。

### 新しいアーキテクチャでアカウントを再実装するのに時間がかかる

再実装時間は、再構築する対象によって異なります。 Adobeでは、再実装に何が関係するかを把握するために、既存のアカウントで次の手順を実行することをお勧めします。

* レポート/ダッシュボードのコアセットを特定します。
* レポートの作成に必要な指標とディメンションを特定します。
* これらの指標およびディメンションを再作成するために必要な列を特定します。

これが完了すると、これらのコアレポートを再構築するために、新しいアーキテクチャData Warehouseに同期する必要があるデータがわかります。

### ヘルプ

この [!DNL Adobe Commerce Intelligence] [サービスチーム](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 再実装を追加費用で実行できます。 に連絡してください [Adobeアカウントチーム](../../guide-overview.md#Submitting-a-Support-Ticket) 新しいアカウントで作成する際に優先順位を付けるダッシュボードやレポートのリストを用意しておきます

### 既存のアーキテクチャの維持

これらの機能があなたにとって重要でない場合は、既存のアカウントに固執することができます。 既存のアカウントを保持するための追加費用はかかりません。 Adobeは、変更なしにこれらのアカウントを引き続きサポートします。
