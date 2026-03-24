---
title: 指標のフィルターセットの作成
description: 保存したフィルターセットを作成して指標に適用する方法を説明します。
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/Y3SA-ypB62c0mwZ6uqAOQUyrISc5Tu8yqClrGwXspoU
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 277
ht-degree: 0%

---

# フィルターセットの作成

同様の方法でフィルタリングする必要がある指標が[!DNL Commerce Intelligence]に複数ある場合（テスト注文のフィルタリングなど）、保存されたフィルターセットを作成して指標に適用できます。 これにより、指標を作成または編集する際に個々のフィルターを追加する必要がなくなるため、時間を節約できます。

詳しくは、[&#x200B; トレーニング ビデオ &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html)を参照してください。

>[!NOTE]
>
>[管理者権限](../../administrator/user-management/user-management.md)が必要です。

1. サイドバーの&#x200B;**[!DNL Manage Data** > **Filter Sets]**&#x200B;をクリックします。

   ![&#x200B; フィルターセットの追加オプションを使用したフィルターセットの作成インターフェイス &#x200B;](../../assets/create-filter-sets.png)

1. ページの上部にある「**[!UICONTROL Add Filter Set]**」をクリックします。

1. フィルターする指標を含むテーブルを選択します。

   例えば、`Total number of orders`指標をフィルタリングし、`orders` テーブル上に構築する場合は、そのテーブルを選択します。

1. `Filter Set`に名前を付けます。

1. 関連するフィルターをすべて追加します。

   例えば、ステータスが完了の注文のみを`Total number of orders`指標に含める場合は、ステータス = `complete`を持たないすべての注文を除外するフィルターを適用します。

1. フィルターロジックを確認し、括弧と演算子が正しく配置されていることを確認します（例：`\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`）。

   [!DNL Commerce Intelligence]件のレポートと予想される結果の間にデータの相違が生じる原因として、多くの場合、フィルターが正しくありません。

1. `Filter Set`を保存します。

フィルターセットを保存した後、同じテーブルを使用している任意の指標に適用できます。 例えば、`Filter Set` テーブルで`orders`を作成した場合、このテーブル上に構築されている&#x200B;*などの*&#x200B;すべての指標`Revenue`に適用できます。

>[!NOTE]
>
>`Filter Sets`は、[!DNL Commerce Intelligence]の計算列にも適用できます。 [!DNL Commerce Intelligence]で作成されたデータディメンションにフィルターセットを適用するには、サポートにお問い合わせください。

## 関連

* [セグメンテーションとフィルタリングのベストプラクティス](../../best-practices/segment-filter.md)
