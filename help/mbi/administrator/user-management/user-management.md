---
title: Adobe Commerce ユーザーと権限の管理
description: Commerce Intelligence ユーザーの管理方法について説明します。
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
TQID: https://experienceleague.adobe.com/T3ZdoQW35n6CAJmDlOlfDVSI1eUA--e4RKZbOMF1BWY
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 406
ht-degree: 0%

---

# ユーザー権限の管理

[!DNL Adobe Commerce Intelligence]は、組織全体の信頼できる唯一の情報源となることを目的としています。 各ユーザーには独自のダッシュボードのセットがあり、[他のユーザーと共有できます](../../data-user/dashboards/share-dashboard-with-users.md)。

## ユーザー権限レベル

[!DNL Commerce Intelligence]には、アカウントの作成時に選択される、ユーザーに適用される一般的な権限レベルが3つあります。

* `Admin`
* `Standard`
* `Read-Only`

これらの権限により、ユーザーは特定のアクションを実行したり、[!DNL Commerce Intelligence]の特定の部分にアクセスしたりできます。 以下は、各権限レベルが[!DNL Commerce Intelligence]で実行できる処理の表です。

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **ユーザーの作成と管理** | ✔ |   |   |
| **電子メールの概要の作成** | ✔ | ✔ |   |
| **ダッシュボードの作成/編集/共有** | ✔ | ✔ |   |
| **ダッシュボードの表示** | ✔ | ✔ | ✔ |
| **ビジュアルレポートの作成/編集/削除** | ✔ | ✔* |   |
| **SQL レポートの作成/編集/削除** | ✔ |  |   |
| **ダッシュボードの複製** | ✔ |   |   |
| **統合の追加と管理** | ✔ |   |   |
| **Data Warehouse Managerにアクセス** | ✔ |   |   |
| **テーブルと列の同期/非同期** | ✔ |   |   |
| **指標の作成/編集** | ✔ |   |   |
| **フィルターセットの作成/編集** | ✔ |   |   |
| **計算列の作成/編集** | ✔ |   |   |
| **依存レポートのリストを作成** | ✔ |   |   |
| **アクセス システムの概要** | ✔ |   |   |
| **タイムゾーン設定へのアクセス** | ✔ |   |   |
| **請求へのアクセス** | ✔ | ✔** |   |
| **サポートへのお問い合わせ** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_特定の指標](../../administrator/user-management/restrict-metric-access.md)に対する&#x200B;**[!UICONTROL Standard]**ユーザーの[ アクセスを制限できます。_
>
>**[!UICONTROL Standard] _ユーザーは、追加の権限設定を使用して請求にアクセスできます。_
>
>**[!UICONTROL Read-Only]**&#x200B;人のユーザーは、共有された&#x200B;_表示_&#x200B;個のダッシュボードのみを使用できます。[!DNL Commerce Intelligence]で何かを作成または編集することはできず、アカウントを検索して新しいダッシュボードを追加することもできます。 Adobeでは、自分またはチームの他のメンバーが管理している&#x200B;**[!UICONTROL Read-Only]**&#x200B;人のユーザーと特定のダッシュボードのセットを共有することをお勧めします。 一連のダッシュボードを複製しないでください。

## 追加の権限：請求とテクニカル {#billingtech}

一般的な権限レベルに加えて、他の2つのユーザー指定（`Billing`と`Technical`）も存在します。 これらの指定は、一般的な権限レベルで使用する必要があります。

### 課金

`Billing`人のユーザーが請求ページにアクセスでき、支払い情報を変更できます。 また、Adobeから請求に関する質問を受けることもあります。

`Admin`人のユーザーはデフォルトで`Billing` タブにアクセスできますが、`Standard`人のユーザーは、プロファイルで`Billing` チェックボックスが選択されている場合もアクセスできます。

![請求ページ ](../../assets/billing.png)<!--{: width="550" height="363"}-->

### テクニカル

`Technical`人のユーザーには特定の権限がありません。この設定は、組織内の技術的な連絡先を示すだけです。 技術的な質問については、Adobeから連絡を取ることができます。

`Admin`人のユーザーは、**[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]**&#x200B;をクリックし、プロンプトに従ってアカウントに新しいユーザーを追加できます。 [!DNL Commerce Intelligence]でユーザーを作成すると、招待する幸運なユーザーに、アカウント設定プロセスの完了方法に関するメールが送信されます。

`Admins`は、**[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**&#x200B;をクリックすることで、いつでも自分のアカウント内のすべてのユーザーを表示できます。 このページには、ユーザーの権限と、ユーザーがアクセスできる指標とダッシュボードが表示されます。
