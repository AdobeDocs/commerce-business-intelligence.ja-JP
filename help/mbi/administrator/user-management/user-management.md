---
title: Adobe Commerceのユーザーと権限の管理
description: Commerce Intelligence ユーザーの管理方法について説明します。
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# ユーザー権限の管理

[!DNL Adobe Commerce Intelligence] は、組織全体の唯一の情報源となることを目的としています。 各ユーザーは、独自のダッシュボードセットを持ち、それらを使用することができます [他のユーザーと共有](../../data-user/dashboards/share-dashboard-with-users.md).

## ユーザー権限レベル

対象： [!DNL Commerce Intelligence]には、ユーザーに適用される一般的な権限レベルが 3 つあり、アカウントの作成時に選択されます。

* `Admin`
* `Standard`
* `Read-Only`

これらの権限により、ユーザーは特定のアクションを実行したり、の特定の部分にアクセスしたりできます。 [!DNL Commerce Intelligence]. 以下の表に、各アクセス許可レベルでできることについて示します [!DNL Commerce Intelligence]:

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **ユーザーの作成/管理** | ✔ |   |   |
| **メール概要の作成** | ✔ | ✔ |   |
| **ダッシュボードの作成/編集/共有** | ✔ | ✔ |   |
| **ダッシュボードの表示** | ✔ | ✔ | ✔ |
| **ビジュアル レポートの作成/編集/削除** | ✔ | ✔* |   |
| **SQL レポートの作成/編集/削除** | ✔ |  |   |
| **ダッシュボードの複製** | ✔ |   |   |
| **統合の追加/管理** | ✔ |   |   |
| **Data Warehouseマネージャーへのアクセス** | ✔ |   |   |
| **テーブルと列の同期/同期解除** | ✔ |   |   |
| **指標の作成/編集** | ✔ |   |   |
| **フィルターセットの作成/編集** | ✔ |   |   |
| **計算列の作成/編集** | ✔ |   |   |
| **依存レポートのリストを作成** | ✔ |   |   |
| **アクセス システムの概要** | ✔ |   |   |
| **タイムゾーン設定へのアクセス** | ✔ |   |   |
| **請求にアクセス** | ✔ | ✔** |   |
| **サポートに連絡** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_以下を制限できます&#x200B;**[!UICONTROL Standard]**ユーザーの [特定の指標へのアクセス](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _ユーザーは、追加の権限設定で請求にアクセスできます。_
>
>**[!UICONTROL Read-Only]** のユーザーのみ _表示_ 共有されているダッシュボード。では何も作成または編集できません [!DNL Commerce Intelligence]また、新しいダッシュボードを検索してアカウントに追加することもできません。 Adobeでは、特定のダッシュボードセットをと共有することをお勧めします **[!UICONTROL Read-Only]** 自分またはチームの別のメンバーが維持するユーザー。 それらのダッシュボードのセットのクローンを作成しないでください。

## その他の権限：請求および技術 {#billingtech}

一般的な権限レベルに加えて、次の 2 つのユーザー指定も存在します。 `Billing` および `Technical`. これらの指定は、一般的な権限レベルで使用する必要があります。

### 請求

`Billing` ユーザーは請求ページにアクセスでき、支払い情報を変更できます。 また、Adobeから請求に関する問い合わせが来ることもあります。

`Admin` ユーザー： `Billing` tab キーがデフォルトで使用されますが、 `Standard` また、次の項目を持っている場合、ユーザーはアクセス権を取得できます `Billing` プロファイルでチェックボックスが選択されている。

![課金](../../assets/billing.png)<!--{: width="550" height="363"}-->

### 技術

`Technical` ユーザーには固有の権限はありません。この設定は、組織内の技術担当者をマークするだけです。 これらのユーザーには、Adobeから技術的な問い合わせがある場合があります。

`Admin` ユーザーは、次の項目をクリックして新しいユーザーをアカウントに追加できます。 **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** とプロンプトに従います。 ユーザーの作成後 [!DNL Commerce Intelligence]招待した幸運な人には、アカウント設定プロセスを完了する方法を記載した電子メールが届きます。

いつでも、 `Admins` をクリックすると、自分のアカウントのすべてのユーザーを表示できます。 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. このページには、ユーザーの権限と、ユーザーがアクセスできる指標およびダッシュボードが表示されます。
