---
title: 指標に対する目標の追跡
description: 売上高、新規登録ユーザー、注文件数など、実際のデータに基づいてビジネス目標を追跡するのに役立つダッシュボードを設定する方法を説明します。
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# パフォーマンス指標に対する目標の追跡

多くのお客様は、多くの場合、 **ビジネス目標**&#x200B;が、 [!DNL MBI]. この記事では、売上高、新規登録ユーザー、注文件数など、実際のデータに基づいてビジネス目標を追跡する際に役立つダッシュボードを設定する方法について説明します。 また、次のようなダッシュボードで、前年比のパフォーマンスの比較方法も示します。

![](../../assets/Goals-_dashboard_2.png)

使用を開始する前に、 [ファイルアップローダ](../importing-data/connecting-data/using-file-uploader.md) また、一定の期間、ビジネス目標を定義したことを確認します。

## はじめに

最初に、ビジネスに関する特定の日別/月別/四半期別ターゲットを含むファイルをアップロードする必要があります。

以下を使用して、 [ファイルアップローダ](../importing-data/connecting-data/using-file-uploader.md) および以下の画像を使用して、ファイルの形式を設定します。 クライアントが追跡する最も一般的なターゲット [!DNL MBI] 注文件数、売上高、新規登録済みアカウントが含まれます。

![](../../assets/Goals-_Excel.png)

## 指標

各ターゲットに対して 1 つの新しい指標を作成する必要があります。 例えば、月別の売上高と注文のターゲットをアップロードする場合、2 つの新しい指標を作成する必要があります。

* **月別収益ターゲット**
* 内 **`Monthly goals`** 表
* この指標では **合計**
* の **`Revenue target`** 列
* 発注元： **`Month`** timestamp

* **月次注文のターゲット**
* 内 **`Monthly goals`** 表
* この指標では **合計**
* の **`Orders target`** 列
* 発注元： **`Month`** timestamp

* **毎月の新規登録アカウントのターゲット**
* 内 **`Monthly goals`** 表
* この指標では **合計**
* の **`New registered accounts target`** 列
* 発注元： **`Month`** timestamp

## レポート

これまでと同様に、ターゲットを分析する際には、静的な値と視覚的なグラフが混在していると便利です。 次に、売上高パフォーマンスの追跡を開始するための 3 つのレポートの例を示します。

* **目標達成に残る収益**
* 指標 `A`: `Revenue`
* 

   [!UICONTROL 指標]: `Revenue`

* 指標 `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* 
   [!UICONTROL 数式]: `(B-A)`
* 

   [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]:（任意の期間）
* 
   [!UICONTROL Interval]: `Month`
* 

   [!UICONTROL グラフの種類]: `Scalar`

* **収益目標**
* 指標 `A`: `Revenue`
* 

   [!UICONTROL 指標]: `Revenue`

* 指標 `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* 指標 `C`: `Revenue (amount change since previous year)` （非表示）
* 
   [!UICONTROL 指標]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]:（今月前年）
* 
   [!UICONTROL 数式]: `(A-C)`
* 

   [!UICONTROL Format]: `Currency`

* オフにする `Multiple Y-Axes`
* [!UICONTROL Time period]:（任意の関連期間）*
* 
   [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

上記の売上高目標レポートを完了したら、注文、登録済みアカウント、または目標ファイルのアップロードに含めたその他の値に関する目標に関して、同じレポートを作成できます。

すべてのレポートをコンパイルした後、必要に応じてダッシュボードで整理できます。 最終的な結果は、このページの上部にある画像のように見える場合があります。
