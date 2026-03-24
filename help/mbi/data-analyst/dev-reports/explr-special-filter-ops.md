---
title: 特別なフィルター演算子
description: レポートの作成時や指標の作成時にフィルターで使用されるいくつかの特殊な演算子について説明します。
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xUfPCWqheQFIG9faVsA5PEWiyn6hLO-Rrm8jPzmaWiw
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 143
ht-degree: 0%

---

# フィルターオプション

このトピックでは、`operators` レポートの作成時`filters`または[指標の作成時](../../tutorials/using-visual-report-builder.md){: target="_blank"}に[を使用した例をいくつか紹介します。](../../data-user/reports/ess-manage-data-metrics.md){: target="_blank"}

## `Filter Operators`

* パターン一致の`LIKE`。 これは、ワイルドカード文字% （可変文字数のワイルドカードの場合）または_（ワイルドカードの一文字の場合）で使用する必要があります。  例えば、制限`LIKE \_ake%`は、`Jake Stein`、`Jake Smith`、または`Fake Smith`に対してtrueを返します。  `Drake Smith`に対してfalseが返されます。

* `NOT LIKE`は上記のパターン一致と似ていますが、一致しないパターンをチェックします。

* `IS`は、列が`NULL`か空かを確認します。

* `IS NOT`は上記の`IS`演算子と似ていますが、NULL以外の列をチェックします。

* `IN`は、値がコンマ区切りリストに存在するかどうかを確認します。 （例えば、「Color `IN` red, orange」は、color `equal to` red OR color `equal to` orangeと同等です）。

* `NOT IN`は上記の`IN`と似ていますが、値が存在しないかどうかをチェックします。
