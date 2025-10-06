---
title: 指標のフィルターセットの作成
description: 保存したフィルターセットを作成して、指標に適用する方法を説明します。
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# フィルターセットの作成

同様の方法でフィルタリングする必要がある指標が [!DNL Commerce Intelligence] 内に複数ある場合（例えばテスト注文を除外する場合）、保存済みのフィルターセットを作成して指標に適用できます。 これにより、指標を作成または編集する際に個々のフィルターを追加する必要がなくなるので、時間を節約できます。

詳しくは、[&#x200B; トレーニングビデオ &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) を参照してください。

>[!NOTE]
>
>[&#x200B; 管理者権限 &#x200B;](../../administrator/user-management/user-management.md) が必要です。

1. サイドバーの「**[!DNL Manage Data** > **Filter Sets]**」をクリックします。

   ![&#x200B; 「フィルターセットを追加」オプションを使用したフィルターセットインターフェイスの作成 &#x200B;](../../assets/create-filter-sets.png)

1. ページ上部の「**[!UICONTROL Add Filter Set]**」をクリックします。

1. フィルターする指標を含んだテーブルを選択します。

   例えば、`Total number of orders` 指標をフィルタリングし、`orders` テーブルに基づいて作成する場合は、そのテーブルを選択します。

1. `Filter Set` に名前を付けます。

1. 関連するすべてのフィルターを追加します。

   例えば、`Total number of orders` 指標に完了ステータスの注文のみを含める場合、ステータス = `complete` を持たないすべての注文を除外するフィルターを適用します。

1. フィルタ ロジックを検証し、括弧と演算子が正しく配置されていることを確認します（例：`\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`）。

   誤ったフィルターは、多くの場合、レポートと期待される結果との間 [!DNL Commerce Intelligence] データの不一致の原因です。

1. `Filter Set` を保存します。

フィルターセットを保存したら、同じテーブルを使用する任意の指標に適用できます。 例えば、`Filter Set` テーブルに `orders` を作成した場合、*など、このテーブルに基づいて作成された* 任意の指標 `Revenue` に適用できます。

>[!NOTE]
>
>`Filter Sets` は、[!DNL Commerce Intelligence] の計算列にも適用できます。 サポートに問い合わせることで、を介して [!DNL Commerce Intelligence] で作成されたデータディメンションにフィルターセットを適用するようリクエストできます。

## 関連

* [セグメント化とフィルタリングのベストプラクティス](../../best-practices/segment-filter.md)
