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

データベーステーブルには、変更可能な値を持つデータ列を使用できます。 例： `orders` という列がある可能性があります。 `status`. 注文が最初にデータベースに書き込まれると、ステータス列に値が含まれる場合があります _保留中_. この順序は、で複製されます。 [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) （これにより） `pending` の値。

注文ステータスは変更できますが、 `pending` ステータス。 最終的には、 `complete` または `cancelled`. Data Warehouseでこの変更内容を確実に同期させるには、新しい値について列を再確認する必要があります。

との適合 [レプリケーション方法](../data-warehouse-mgr/cfg-replication-methods.md) 話し合われたの？ 再チェックの処理は、選択したレプリケーション方法によって異なります。 この `Modified\_At` 再チェックを設定する必要がないので、レプリケーション方法は、変更される値を処理する場合に最適です。 この `Auto-Incrementing Primary Key` および `Primary Key Batch Monitoring` メソッドには、再確認の設定が必要です。

これらのメソッドのいずれかを使用する場合、再チェックのために変更可能な列にフラグを付ける必要があります。 これを行う方法は 3 つあります。

1. 再確認する更新フラグ列の一部として実行される監査プロセス。

   >[!NOTE]
   >
   >監査はサンプリングプロセスに依存し、列の変更はすぐには反映されない場合があります。

1. Data Warehouseマネージャーの列の横にあるチェックボックスをオンにし、 **[!UICONTROL Set Recheck Frequency]**&#x200B;を選択し、変更をチェックするタイミングに適した時間間隔を選択します。

1. のメンバー [!DNL Adobe Commerce Intelligence] Data Warehouseチームは、Data Warehouseを再チェックインする列を手動でマークできます。 変更可能な列がわかっている場合は、チームに連絡して、再チェックの設定をリクエストしてください。 リクエストに、列のリストと頻度を含めます。

## 頻度の再確認 {#frequency}

**ご存じでしたか？**
再チェックの設定 `primary key` 列の値が変更されていないかをチェックしません。 テーブルの削除された行がチェックされ、削除がData Warehouseからパージされます。

再チェックのフラグが設定されているカラムでは、再チェックの頻度も設定できます。 特定の列が頻繁に変更されない場合、頻繁でない再確認を選択すると、次のことが可能になります [更新サイクルの最適化](../../best-practices/reduce-update-cycle-time.md).

頻度オプションは次のとおりです。

* `always`  – 更新のたびに再確認が行われる
* `daily`  – 再確認は、宣言されたタイムゾーンの午前 0 時の後に最初に行われます
* `weekly`  – 再確認は、宣言されたタイムゾーンの毎週金曜日の午後 9 時以降に行われます
* `monthly`  – 再確認は、宣言されたタイムゾーンの金曜日の午後 9 時以降、4 週間ごとに行われます
* `once`  – 次の更新（1 回限りの更新）でのみ発生

更新時間は同期が必要なデータの量に相関するため、Adobeでは次の項目を選択することをお勧めします `daily`, `weekly`、または `monthly` すべての更新の代わりに再確認します。

## 再チェック頻度の管理 {#manage}

再チェックの頻度は、テーブル名をクリックしてから個々の列をチェックすることで、Data Warehouseで管理できます。 同期中のステータスと再確認頻度（ **変更？** 列）は、テーブルの各列に表示されます。

再チェックの頻度を変更するには、変更する列の横にあるチェックボックスをクリックします。 次に、 **[!UICONTROL Set Recheck Frequency]** ドロップダウンから目的の頻度を選択して設定します。

![](../../assets/dwm-recheck.png)

時々は見るかもしれない `Paused` が含まれる `Changes?` 列。 この値は、テーブルの [複製方法](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) はに設定されています。 `Paused`.

[!DNL Adobe] では、これらの列を確認して、更新を最適化し、変更可能な列が再チェックされていることを確認することをお勧めします。 データの変更頻度を考慮して列の再チェック頻度が高い場合、Adobeでは、更新を最適化するために頻度を低くすることをお勧めします。

お問い合わせいただくか、現在のレプリケーション方法や再チェックについてご質問ください。

**関連：**

* [更新時間の短縮](../../best-practices/reduce-update-cycle-time.md)
* [分析のためのデータベースの最適化](../../best-practices/opt-db-analysis.md)
