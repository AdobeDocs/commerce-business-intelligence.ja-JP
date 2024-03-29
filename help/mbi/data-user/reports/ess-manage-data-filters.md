---
title: 指標のフィルターセットの作成
description: 保存済みフィルターセットを作成し、指標に適用する方法を説明します。
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# フィルターセットの作成

に複数の指標がある場合 [!DNL Commerce Intelligence] 同様の方法でフィルタリングする必要がある（テスト注文をフィルタリングするなど）場合は、保存済みのフィルターセットを作成して指標に適用できます。 指標を作成または編集する際に個々のフィルターを追加する必要がないので、時間を節約できます。

詳しくは、 [トレーニングビデオ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) を参照してください。

>[!NOTE]
>
>が必要 [管理者権限](../../administrator/user-management/user-management.md).

1. クリック **[!DNL Manage Data** > **Filter Sets]** サイドバーに表示されます。

   ![](../../assets/create-filter-sets.png)

1. クリック **[!UICONTROL Add Filter Set]** をクリックします。

1. フィルタリングする指標を含むテーブルを選択します。

   例えば、 `Total number of orders` 指標を使用し、 `orders` テーブルを選択し、そのテーブルを選択します。

1. に名前を付けます。 `Filter Set`.

1. 関連するすべてのフィルターを追加します。

   例えば、「完了」ステータスの注文のみを `Total number of orders` 指標を使用する場合、ステータス= `complete`.

1. フィルターロジックを検証し、括弧と演算子が正しく配置されていることを確認します。例： `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   誤ったフィルターは、多くの場合、 [!DNL Commerce Intelligence] レポートおよび期待される結果。

1. を保存します。 `Filter Set`.

フィルターセットを保存した後、同じテーブルを使用する任意の指標に適用できます。 例えば、 `Filter Set` の `orders` テーブルを次に適用できます。 *任意の指標* このテーブルに基づいて作成される `Revenue`.

>[!NOTE]
>
>`Filter Sets` また、 [!DNL Commerce Intelligence]. フィルターセットの適用を、 [!DNL Commerce Intelligence] を介して、サポートに連絡します。

## 関連

* [セグメント化とフィルタリングのベストプラクティス](../../best-practices/segment-filter.md)
