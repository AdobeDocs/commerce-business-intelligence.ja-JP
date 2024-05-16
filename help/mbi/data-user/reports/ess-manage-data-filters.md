---
title: 指標のフィルターセットの作成
description: 保存したフィルターセットを作成して、指標に適用する方法を説明します。
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '268'
ht-degree: 0%

---

# フィルターセットの作成

に複数の指標がある場合 [!DNL Commerce Intelligence] 同様の方法でフィルタリングする必要がある場合（例えば、テスト注文を除外する場合）、保存済みのフィルターセットを作成して、指標に適用できます。 これにより、指標を作成または編集する際に個々のフィルターを追加する必要がなくなるので、時間を節約できます。

を参照してください。 [トレーニングビデオ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) を参照してください。

>[!NOTE]
>
>が必要 [管理者権限](../../administrator/user-management/user-management.md).

1. クリック **[!DNL Manage Data** > **Filter Sets]** サイドバーで。

   ![](../../assets/create-filter-sets.png)

1. クリック **[!UICONTROL Add Filter Set]** ページの上部

1. フィルターする指標を含んだテーブルを選択します。

   例えば、 `Total number of orders` 指標および指標は `orders` テーブル、そのテーブルを選択します。

1. に名前を付ける `Filter Set`.

1. 関連するすべてのフィルターを追加します。

   例えば、完了ステータスの注文のみを `Total number of orders` 指標の場合、ステータス =でないすべての注文を除外するフィルターを適用します `complete`.

1. フィルターロジックを検証し、括弧と演算子が正しく配置されていることを確認します。例： `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   多くの場合、間違ったフィルターが間のデータ不一致の原因です [!DNL Commerce Intelligence] レポートと予想される結果。

1. を保存します `Filter Set`.

フィルターセットを保存したら、同じテーブルを使用する任意の指標に適用できます。 例えば、 `Filter Set` 日 `orders` テーブル、適用先 *任意の指標* 次のような、このテーブルに基づいて作成されます `Revenue`.

>[!NOTE]
>
>`Filter Sets` は、の計算列にも適用できます [!DNL Commerce Intelligence]. で作成されたデータディメンションにフィルターセットを適用するようリクエストすることもできます。 [!DNL Commerce Intelligence] を使用して、サポートに問い合わせます。

## 関連

* [セグメント化とフィルタリングのベストプラクティス](../../best-practices/segment-filter.md)
