---
title: データチェックの設定
description: 変更可能な値を使用してデータ列を設定する方法を説明します。
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# データチェックの設定

データベーステーブルには、変更可能な値を持つデータ列を使用できます。 例えば、`orders` テーブルには `status` という列があるとします。 注文が最初にデータベースに書き込まれると、ステータス列には値 _保留中_ が含まれる場合があります。 注文は [0}Data Warehouse} でこの ](../data-warehouse-mgr/tour-dwm.md) 値でレプリケートされます。`pending`

注文ステータスは変更できますが、常に `pending` しいステータスであるとは限りません。 最終的には `complete` や `cancelled` になる可能性があります。 Data Warehouseでこの変更内容を確実に同期させるには、新しい値について列を再確認する必要があります。

これは、前述の [ レプリケーション方法 ](../data-warehouse-mgr/cfg-replication-methods.md) とどのように適合しますか。 再チェックの処理は、選択したレプリケーション方法によって異なります。 再チェックを設定する必要がないので、`Modified\_At` レプリケーション方法は変更する値を処理する場合に最適です。 `Auto-Incrementing Primary Key` メソッドと `Primary Key Batch Monitoring` メソッドでは、構成の再確認が必要です。

これらのメソッドのいずれかを使用する場合、再チェックのために変更可能な列にフラグを付ける必要があります。 これを行う方法は 3 つあります。

1. 再確認する更新フラグ列の一部として実行される監査プロセス。

   >[!NOTE]
   >
   >監査はサンプリングプロセスに依存し、列の変更はすぐには反映されない場合があります。

1. Data Warehouse Manager の列の横にあるチェックボックスをオンにし、「**[!UICONTROL Set Recheck Frequency]**」をクリックして、変更を確認するタイミングに適した時間間隔を選択すると、手動で設定できます。

1. [!DNL Adobe Commerce Intelligence] Data Warehouse チームのメンバーは、Data Warehouseを再チェックインする列を手動でマークできます。 変更可能な列がわかっている場合は、チームに連絡して、再チェックの設定をリクエストしてください。 リクエストに、列のリストと頻度を含めます。

## 頻度の再確認 {#frequency}

**ご存じでしたか？**
`primary key` 列で再チェックを設定しても、列の値が変更されたかはチェックされません。 テーブルで削除された行の有無が確認され、削除がData Warehouseからパージされます。

再チェックのフラグが設定されているカラムでは、再チェックの頻度も設定できます。 特定の列が頻繁に変更されない場合、頻繁でない再確認を選択すると [ 更新サイクルを最適化 ](../../best-practices/reduce-update-cycle-time.md) できます。

頻度オプションは次のとおりです。

* `always` – 更新時に再チェックが行われる
* `daily` – 宣言されたタイムゾーンの午前 0 時の後、最初に再チェックが行われます
* `weekly` – 再確認は、宣言されたタイムゾーンの毎週金曜日の午後 9 時の更新後に行われます
* `monthly` – 再確認は、宣言されたタイムゾーンの金曜日の午後 9 時以降に 4 週間ごとに行われます
* `once` – 次の更新（1 回限りの更新）でのみ発生

更新時間は同期が必要なデータ量に相関するので、Adobeでは更新のたびに代わりに `daily`、`weekly`、または `monthly` を選択して再確認することをお勧めします。

## 再チェック頻度の管理 {#manage}

再チェック頻度は、テーブル名をクリックしてから個々の列をチェックすることで、Data Warehouseで管理できます。 同期ステータスと再確認頻度（**Changes?** 列）は、テーブルの各列に表示されます。

再チェックの頻度を変更するには、変更する列の横にあるチェックボックスをクリックします。 次に、「**[!UICONTROL Set Recheck Frequency]**」ドロップダウンをクリックし、目的の頻度を設定します。

![](../../assets/dwm-recheck.png)

`Paused` の列に `Changes?` が表示される場合があります。 この値は、テーブルの [ レプリケーションメソッド ](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) が `Paused` に設定されている場合に表示されます。

[!DNL Adobe] では、これらの列を確認して、更新を最適化し、変更可能な列が再チェックされていることを確認することをお勧めします。 Adobe データの変更頻度を考慮して列の再チェック頻度が高い場合は、更新内容を最適化するために頻度を低くすることをお勧めします。

お問い合わせいただくか、現在のレプリケーション方法や再チェックについてご質問ください。

**関連：**

* [更新時間の短縮](../../best-practices/reduce-update-cycle-time.md)
* [分析のためのデータベースの最適化](../../best-practices/opt-db-analysis.md)
