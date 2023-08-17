---
title: MongoDB のデータモデリング
description: 問題を引き起こすデータパターンを回避する方法を説明します。
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 1%

---

# [!DNL MongoDB] データモデリング

条件 [!DNL Adobe Commerce Intelligence] 取り込む [!DNL MongoDB] データを使用する場合は、そのデータをリレーショナルモデルに変換します。

悪い知らせ：ほとんどのデータパターンは問題を引き起こしませんが、次のようにはサポートされないデータパターンがいくつかあります。 [!DNL Commerce Intelligence]リレーショナルモデルへの変換が原因です。

良い知らせ：これらのパターンはすべて避けることができます。

## サブネスト化された配列 {#subnested}

コレクションが次の例のような場合、 [!DNL Commerce Intelligence] は、items 配列内のデータのみをレプリケートします。 サブ項目配列のデータは取り込まれません。

```bash
    {
        _id: 0000000000000001
        items: [
            {
                _id: 0000000000000002
               subItems: [
                   {
                       _id: 0000000000000003
                      name: "Donut"
                      description: "glazed"
                   }
               ]
            }
        ]
    }
```

## 変数オブジェクトキー {#varobjectkeys}

可変オブジェクトキーを持つオブジェクトを含むコレクションは、 [!DNL Commerce Intelligence]. 例：

```bash
    {
        _id: 0000000000000001
        friends: {
            0000000000000002: "Jimmy",
            0000000000000004: "Roger",
            0000000000000005: "Susan"
        },
    }
```

これは通常、オブジェクトが使用されている場合に発生し、配列の方が適切です。 次に、上記の例を再度実行します。

```bash
    {
        _id: 0000000000000001
        friends: [
            { friend_id: 0000000000000002, name: "Jimmy" },
            { friend_id: 0000000000000004, name: "Roger" },
            { friend_id: 0000000000000005, name: "Susan"}
        ]
    }
```
