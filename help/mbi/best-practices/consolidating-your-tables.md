---
title: テーブルの統合
description: テーブルとデータベースを統合する方法について説明します。
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
role: Admin, User
feature: Commerce Tables, Data Integration
TQID: 'https://experienceleague.adobe.com/HC5REx483htdfFigZPxcrZeD5byyJKk-beQqnEARt1E'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%
---
# テーブルの統合

複数のストアフロントまたは複数の市場で運営している場合は、類似のデータベースが個別に保存されている可能性があります。 [!DNL Adobe Commerce Intelligence]では、異なるデータベースの類似したテーブルを簡単にまとめることができます。

例えば、`Market A`の`orders` テーブルと`Market B`の同様の`orders` テーブルがあります。 [!DNL Commerce Intelligence]は両方のテーブルを統合でき、特定の市場でセグメント化することに加えて、`Market A`と`B`の両方から集計注文データを見ることができます。

テーブルの統合を機能させるには、入力テーブルが&#x200B;**同様に構造化**&#x200B;されている必要があります。 つまり、すべての入力テーブルには、統合テーブルに必要なデータ列が含まれている必要があります。

このトピックでは、統合テーブルの最も一般的な使用例と、独自のテーブルを作成するために必要な次の手順について説明します。

## 統合テーブルを使用する場合の推奨事項

以下では、システムで統合テーブルを使用することが適切な場合について説明します。

### 複数のweb サイトからのデータの統合

複数のブランドやweb サイトで販売している場合、各ブランドやweb サイトの表の構造が類似している可能性があります。

例えば、web サイト `A`用の`orders` テーブルと、web サイト `B`用の別の類似した`orders` テーブルがある場合があります。 このような状況では、web サイト `A`および`B`から`orders` テーブルを統合すると便利な場合があります。 これにより、web サイト `A`および`B`からの合計売上高と注文数を確認できるだけでなく、これら2つのweb サイトで指標をセグメント化できます。

### レガシーデータの統合

多くの企業では、データベースを一度にまたは別のタイミングでリファクタリングしており、古いデータベースのデータが常に新しいシステムに変換されるとは限りません。 統合テーブルを使用して、従来のテーブルのキー列をアクティブなシステムのキー列と結合できます。 これにより、履歴を通じてデータの統合分析を実行できます。

### アクティブユーザー分析のためのイベントの組み合わせ

アンケートに答える、ゲームをプレイする、購入する、友人を紹介するなど、オーディエンスがいくつかのことができるweb サイトを想像してみてください。 通常、これらの各イベントは独自のテーブルに保存されます。 このため、特定の期間内に少なくとも1つのアクションを実行した個別のユーザーの数を分析することが困難になります。

統合テーブルを使用して、すべてのユーザーの1つの統合リストを作成し、これらのイベントがいつ発生したかを作成できます。 その後、統合テーブルでクエリを実行して、そのような分析を簡単に実行できます。

Data Warehouseの他のすべてのテーブルと同様に、別の種類のグラフや分析を強化するために列を追加できます。

## 統合表の作成、表示または更新

Data Warehouseに統合テーブルを追加する場合は、[!DNL Commerce Intelligence] [ サポート ](../guide-overview.md#Submitting-a-Support-Ticket)にお問い合わせください。

>[!NOTE]
>
>統合されたテーブルは`Data Warehouse Manager`では表示できないため、これらのテーブルの表示と更新は[!DNL Commerce Intelligence]のサポートによってのみ実行できます。
