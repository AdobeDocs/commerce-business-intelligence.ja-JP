---
title: 指標に対する目標の追跡
description: 売上高、新規登録ユーザー、注文の推移など、実際のデータに対してビジネス目標を追跡するのに役立つダッシュボードの設定方法を説明します。
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# パフォーマンス指標に対する目標の追跡

ほとんどのクライアントは、**ビジネス目標** を追跡したいと考えていますが、[!DNL Adobe Commerce Intelligence] ではこれが可能であるとは認識していません。 このトピックでは、売上高、新規登録ユーザー、注文の推移など、実際のデータに対してビジネス目標を追跡するのに役立つダッシュボードの設定方法を説明します。 また、次のようなダッシュボードで、前年比のパフォーマンスを比較する方法についても説明します。

![&#x200B; 実際の指標のパフォーマンスに対する目標のトラッキングを示すダッシュボード &#x200B;](../../assets/Goals-_dashboard_2.png)

開始する前に、[&#x200B; ファイルアップローダ &#x200B;](../importing-data/connecting-data/using-file-uploader.md) を確認し、特定の期間のビジネス目標が定義されていることを確認する必要があります。

## はじめに

まず、ビジネスの特定の日次/月次/四半期次ターゲットを含むファイルをアップロードする必要があります。

[&#x200B; ファイルアップローダ &#x200B;](../importing-data/connecting-data/using-file-uploader.md) と以下の画像を使用して、ファイルをフォーマットできます。 [!DNL Commerce Intelligence] で顧客が追跡する最も一般的なターゲットには、注文、売上高、新規登録済みアカウントが含まれます。

![&#x200B; 目標と指標を追跡するための Excel スプレッドシートテンプレート &#x200B;](../../assets/Goals-_Excel.png)

## 指標

各ターゲットに対して 1 つの新しい指標を作成します。 例えば、月次の売上高と注文のターゲットをアップロードする場合は、2 つの新しい指標を作成する必要があります。

* **月間収益目標**
* **`Monthly goals`** のテーブル内
* このメトリックは **Sum** を実行します。
* **`Revenue target`** 列
* **`Month`** タイムスタンプで並べ替え

* **月次オーダーのターゲット**
* **`Monthly goals`** のテーブル内
* このメトリックは **Sum** を実行します。
* **`Orders target`** 列
* **`Month`** タイムスタンプで並べ替え

* **新規登録アカウントの月次ターゲット**
* **`Monthly goals`** のテーブル内
* このメトリックは **Sum** を実行します。
* **`New registered accounts target`** 列
* **`Month`** タイムスタンプで並べ替え

## レポート

ターゲットを分析する際に、静的な値と視覚的なグラフを組み合わせると便利です。 次に、売上高のパフォーマンスの追跡を開始するための 3 つのサンプルレポートを示します。

* **目標を達成するための残りの売上高**
* 指標 `A`: `Revenue`
* &#x200B;
  [!UICONTROL 指標]: `Revenue`

* 指標 `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* &#x200B;
  [!UICONTROL 数式]: `(B-A)`
* &#x200B;
  [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]: （必要な関連期間）
* &#x200B;
  [!UICONTROL Interval]: `Month`
* &#x200B;
  [!UICONTROL グラフ タイプ]: `Scalar`

* **収益目標**
* 指標 `A`: `Revenue`
* &#x200B;
  [!UICONTROL 指標]: `Revenue`

* 指標 `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* 指標 `C`: `Revenue (amount change since previous year)` （非表示）
* &#x200B;
  [!UICONTROL 指標]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: （昨年今月）
* &#x200B;
  [!UICONTROL 数式]: `(A-C)`
* &#x200B;
  [!UICONTROL Format]: `Currency`

* `Multiple Y-Axes` をオフにする
* [!UICONTROL Time period]: （必要な関連期間）*
* &#x200B;
  [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

売上高目標の上記のレポートを完了したら、目標ファイルのアップロードに含めた注文、登録済みアカウント、その他の値に関する目標について、同一のレポートを作成できます。

すべてのレポートをコンパイルした後、必要に応じてダッシュボード上で整理できます。 結果は、このページの上部の画像のようになります。
