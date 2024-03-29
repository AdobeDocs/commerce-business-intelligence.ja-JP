---
title: データチェックの設定
description: 変更可能な値を持つデータ列を設定する方法を説明します。
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# データチェックの設定

データベーステーブルには、値が変更可能なデータ列が存在する場合があります。 例えば、 `orders` という列があるかもしれないテーブル `status`. 注文が最初にデータベースに書き込まれるとき、ステータス列に値が含まれている場合があります _保留中_. 注文は、 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) この `pending` の値です。

注文のステータスは、必ずしも `pending` ステータス。 最終的には `complete` または `cancelled`. Data Warehouseがこの変更を確実に同期するには、列で新しい値を再度チェックする必要があります。

これがとどのように適合するか [レプリケーションメソッド](../data-warehouse-mgr/cfg-replication-methods.md) それは話し合われましたか？ 再チェックの処理は、選択したレプリケーション方法に応じて異なります。 The `Modified\_At` 再チェックを設定する必要がないので、変更する値を処理するにはレプリケーション方法が最適です。 The `Auto-Incrementing Primary Key` および `Primary Key Batch Monitoring` メソッドでは再確認の設定が必要です。

これらの方法のいずれかを使用する場合は、変更可能な列に再チェック用のフラグを設定する必要があります。 これをおこなう方法は 3 つあります。

1. 再確認する更新フラグ列の一部として実行される監査プロセス。

   >[!NOTE]
   >
   >監査はサンプリングプロセスに依存しており、変更される列がすぐに取り込まれない場合があります。

1. 自分で設定するには、Data Warehouseマネージャの列の横にあるチェックボックスをオンにして、 **[!UICONTROL Set Recheck Frequency]**&#x200B;を選択し、変更を確認する必要がある場合に適した時間間隔を選択します。

1. のメンバー [!DNL Adobe Commerce Intelligence] Data Warehouseチームは、列を手動でマークして、Data Warehouseを再確認できます。 変更可能な列がわかっている場合は、チームに連絡して、再チェックが設定されていることを要求します。 リクエストと共に、列のリストと頻度を含めます。

## 頻度を再確認 {#frequency}

**知ってたの？**
の再チェックの設定 `primary key` 列は、変更された値を確認しません。 テーブルで削除された行がチェックされ、削除はData Warehouseからパージされます。

列に再確認用のフラグが設定されている場合は、再確認の実行頻度を設定することもできます。 特定の列が頻繁に変更されない場合は、より頻繁に再チェックを選択すると、 [更新サイクルを最適化する](../../best-practices/reduce-update-cycle-time.md).

頻度オプションは次のとおりです。

* `always`  — 更新のたびに再チェックが実行されます
* `daily`  — 宣言されたタイムゾーンの午前 0 時以降の最初の更新が再確認されます
* `weekly`  — 宣言されたタイムゾーンに対して毎週 9 時以降の金曜日の更新が再確認されます
* `monthly`  — 宣言されたタイムゾーンに対して 4 週間おきに金曜日の午後 9 時に更新が行われる
* `once`  — 次回の更新（1 回限りの更新）でのみ発生

更新時間は同期する必要のあるデータ量に関連付けられているので、Adobeでは `daily`, `weekly`または `monthly` 更新のたびに、代わりにを再度オンにします。

## 再チェック頻度の管理 {#manage}

再確認頻度は、テーブル名をクリックし、個々の列を確認することで、Data Warehouseで管理できます。 同期ステータスと再確認頻度 ( **変更？** 列 ) は、テーブルの各列に対して表示されます。

再チェックの頻度を変更するには、変更する列の横にあるチェックボックスをクリックします。 次に、 **[!UICONTROL Set Recheck Frequency]** ドロップダウンを開き、目的の頻度を設定します。

![](../../assets/dwm-recheck.png)

時々、 `Paused` （内） `Changes?` 列。 この値は、テーブルの [複製法](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) が `Paused`.

[!DNL Adobe] では、これらの列を確認して更新内容を最適化し、変更可能な列が再度チェックされるようにすることをお勧めします。 データの変更頻度が高い列の再確認頻度が高い場合は、Adobeで更新を最適化するために、値を小さくすることをお勧めします。

現在のレプリケーション方法や再確認についてのご質問やご質問は、お問い合わせください。

**関連：**

* [更新時間の短縮](../../best-practices/reduce-update-cycle-time.md)
* [分析用にデータベースを最適化中](../../best-practices/opt-db-analysis.md)
