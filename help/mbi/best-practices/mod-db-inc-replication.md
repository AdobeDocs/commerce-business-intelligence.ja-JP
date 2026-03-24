---
title: 増分レプリケーションをサポートするためのデータベースの変更
description: 増分レプリケーションをサポートするようにデータベースを変更する方法について説明します。
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/VH5mhfRJteAxiQAmh14TzhnAqym65X6SFRMGuSuEvwM
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 334
ht-degree: 0%

---

# 増分レプリケーションのサポート

現在、テーブルで増分レプリケーションが許可されていない場合は、考えられる解決策について次の推奨事項を参照してください。

## 変更日時の変更

最も理想的なレプリケーション方法である`Modified At` メソッドは、`datetime`列を使用して、新しいデータや更新されたデータを検出します。 このメソッドを使用するテーブルの`datetime`列にはインデックスを作成する必要があり、いつでもnull値を含めることはできません。

テーブルに`datetime`列がない場合は、インデックス `modified at`列を追加できます。 Null値は`modified at`列では使用できません。 各行に列が入力されていることを確認します。

`Modified At` メソッドが意図したとおりに動作することを確認するために、テーブルから行を削除することはできません。 代わりに、`deleted`列をテーブルに追加して、行を無効としてマークする必要があります。 この列は、行が無効な場合は`1`、それ以外の場合は`0`を返します。 その後、この列を使用して、指標とレポートを作成する際に無効な行を除外できます。

## 1つの自動インクリメントプライマリキーの変更

`Modified At` メソッドを有効にできない場合は、プライマリキーの自動増分が次の最適なオプションです。 新しいデータは、Data Warehouseの現在の最大値よりも高いプライマリキー値を検索することで、この方法を使用してテーブルで検出されます。

この方法を使用するテーブルは、プライマリキーを自動的に増分する整数の1列であることを忘れないでください。 このメソッドをデータベースで使用するには、次の変更を行います。

* プライマリキーが複合キーまたは非整数の場合、プライマリキーを自動増分整数に変更します
* プライマリキーが1つの整数列であるが、キーを非順番に割り当てることができる場合は、プライマリキーを自動増分に変更します

## まとめ

テーブルを少し変更することで、より高速で効率的な増分レプリケーション方法を活用できます。 ただし、これができない場合でも、[更新時間の短縮](../best-practices/reduce-update-cycle-time.md)および[ データベースの最適化](../best-practices/opt-db-analysis.md)に他の手順を実行できます。
