---
title: 指標に対する目標の追跡
description: 売上、新規登録ユーザー、注文など、実際のデータに対するビジネス目標を追跡するためのダッシュボードの設定方法を説明します。
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
TQID: https://experienceleague.adobe.com/gT-FJxqVg3X9fuXe-4kWErttYJ6qSMD4eqNvOITNNtQ
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 402
ht-degree: 0%

---

# パフォーマンス指標に対する目標の追跡

ほとんどのクライアントは&#x200B;**ビジネス目標**&#x200B;を追跡したいと考えていますが、[!DNL Adobe Commerce Intelligence]でこれが可能であることに気づきません。 このトピックでは、売上、新規登録ユーザー、注文など、実際のデータに対してビジネス目標を追跡するためのダッシュボードを設定する方法を説明します。 また、次のようなダッシュボードで、前年比のパフォーマンスを比較する方法についても説明します。

実際の指標のパフォーマンスに対する目標の追跡を示す![ ダッシュボード ](../../assets/Goals-_dashboard_2.png)

開始する前に、[ ファイルアップローダー](../importing-data/connecting-data/using-file-uploader.md)を確認し、特定の期間のビジネス目標を定義していることを確認する必要があります。

## はじめに

まず、ビジネス向けの特定の日次、月次、四半期ごとの目標を含むファイルをアップロードする必要があります。

[ ファイルアップローダー](../importing-data/connecting-data/using-file-uploader.md)と以下の画像を使用して、ファイルをフォーマットできます。 [!DNL Commerce Intelligence]でクライアントが追跡する最も一般的なターゲットには、注文、収益、新規登録アカウントなどがあります。

目標と指標を追跡するための![Excel スプレッドシート テンプレート ](../../assets/Goals-_Excel.png)

## 指標

ターゲットごとに新しい指標を1つ作成します。 例えば、月間収益と受注目標をアップロードする場合、2つの新しい指標を作成する必要があります。

* **月間売上目標**
* **`Monthly goals`** テーブル内
* この指標は&#x200B;**合計**&#x200B;を実行します
* **`Revenue target`**&#x200B;列
* **`Month`** タイムスタンプで注文

* **月次注文数ターゲット**
* **`Monthly goals`** テーブル内
* この指標は&#x200B;**合計**&#x200B;を実行します
* **`Orders target`**&#x200B;列
* **`Month`** タイムスタンプで注文

* **月間新規登録済みアカウントのターゲット**
* **`Monthly goals`** テーブル内
* この指標は&#x200B;**合計**&#x200B;を実行します
* **`New registered accounts target`**&#x200B;列
* **`Month`** タイムスタンプで注文

## レポート

ターゲットを分析する際には、静的値と視覚的なチャートを組み合わせると便利です。 収益パフォーマンスのトラッキングに役立つ3つのレポート例を紹介します。

* **目標を達成するために残った収益**
* 指標`A`: `Revenue`
* 
  [!UICONTROL指標]: `Revenue`

* 指標`B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* 
  [!UICONTROL数式]: `(B-A)`
* 
  [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]: （必要な期間を選択）
* 
  [!UICONTROL Interval]: `Month`
* 
  [!UICONTROL チャートタイプ]: `Scalar`

* **売上目標**
* 指標`A`: `Revenue`
* 
  [!UICONTROL指標]: `Revenue`

* 指標`B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* 指標`C`: `Revenue (amount change since previous year)` （非表示）
* 
  [!UICONTROL指標]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: （昨年の今月）
* 
  [!UICONTROL数式]: `(A-C)`
* 
  [!UICONTROL Format]: `Currency`

* `Multiple Y-Axes`をオフにする
* [!UICONTROL Time period]: （関連する任意の期間）*
* 
  [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

売上目標に関する上記のレポートが完成したら、注文、登録済みアカウント、または目標ファイルにアップロードしたその他の値に関する同じレポートを作成できます。

すべてのレポートをまとめた後、必要に応じてダッシュボード上でレポートを整理できます。 結果は、このページの上部の画像のように見えます。
