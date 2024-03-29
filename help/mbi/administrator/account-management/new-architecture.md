---
title: 新しいアーキテクチャ
description: 新しいアーキテクチャに移行する利点について説明します。
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
source-git-commit: ddda796c9f32d22b1d679fc245eb11b92cd491cf
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---

# 新しいアーキテクチャ

[!DNL Adobe Commerce Intelligence] 製品およびエンジニアリングチームは、昨年において、最も大規模で要望の高い改善を可能にすることに焦点を当ててきました。 Adobeが新しい [!DNL Commerce Intelligence] これらの改善を実現する製品アーキテクチャ。

## 新しいアーキテクチャのメリット

* SQL を使用した計算列を含む、Data Warehouse内の列のタイプを作成します。
* 新しい列をすぐに使用できます。
* データ遅延が大幅に改善されました。

## 技術上のメリット

主な違いは上記のとおりですが、主な変更点は、更新サイクル中の計算の実行方法です。 計算は、更新のたびにすべての列で実行されるわけではなく、VisualReport Builderからオンデマンドで実行されます。

### 新しいアーキテクチャへの移行

アカウントは基本的に異なる方法で構築されるので、Data Warehouseやレポートを新しいアーキテクチャアカウントに移行する自動プロセスはありません。 新しいアーキテクチャに移行するには、既存のアカウントを再実装する必要があります。

### 新しいアーキテクチャへの移行に要するコスト

追加コストはありません。 Adobeは、再実装を開始するためにこの新しいアカウントを作成します。このアカウントは、少なくとも 1 ヶ月は無料です。 これにより、両方のアカウントを開いて再実装をより簡単に実行でき、チームがサービスにギャップを持たないようにすることができます。

### 新しいアーキテクチャでアカウントを再実装するのに必要な時間

再実装にかかる時間は、再構築する対象によって異なります。 Adobeでは、既存のアカウントで次の手順を実行して、再実装に関与する内容を把握することをお勧めします。

* 主要なレポート/ダッシュボードのセットを特定します。
* これらのレポートの作成に必要な指標とディメンションを特定します。
* これらの指標およびディメンションの再作成に必要な列を特定します。

この作業が完了したら、新しいアーキテクチャData Warehouseと同期して、これらのコアレポートを再構築する必要があるデータを把握します。

### ヘルプの表示

The [!DNL Adobe Commerce Intelligence] [サービスチーム](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) を使用して再実装を実行し、追加コストをかけることができます。 お問い合わせ [Adobeアカウントチーム](../../guide-overview.md#Submitting-a-Support-Ticket) 新しいアカウントでの作成を優先するダッシュボード/レポートのリストを提供する準備をします。

### 既存のアーキテクチャの使用

これらの機能が重要でない場合は、既存のアカウントをそのまま使用できます。 既存のアカウントを維持するための追加費用は発生しません。 Adobeは、変更を加えずに、引き続きこれらのアカウントをサポートします。
