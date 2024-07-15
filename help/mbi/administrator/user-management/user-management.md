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

[!DNL Adobe Commerce Intelligence] は、組織全体の唯一の情報源となることを目的としています。 各ユーザーは、独自のダッシュボードのセットを持ち、それらを [ 他のユーザーと共有 ](../../data-user/dashboards/share-dashboard-with-users.md) できます。

## ユーザー権限レベル

[!DNL Commerce Intelligence] に、ユーザーに適用される一般的な権限レベルは 3 つあり、これらはアカウントの作成時に選択されます。

* `Admin`
* `Standard`
* `Read-Only`

これらの権限により、ユーザーは特定のアクションを実行したり、[!DNL Commerce Intelligence] ールの特定の部分にアクセスしたりできます。 各アクセス許可レベルでできることの表を次に示し [!DNL Commerce Intelligence] す。

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **ユーザーの作成/管理** | ✔ |   |   |
| **メール概要の作成** | ✔ | ✔ |   |
| **ダッシュボードの作成/編集/共有** | ✔ | ✔ |   |
| **ダッシュボードの表示** | ✔ | ✔ | ✔ |
| **ビジュアルレポートの作成/編集/削除** | ✔ | ✔* |   |
| **SQL レポートの作成/編集/削除** | ✔ |  |   |
| **ダッシュボードの複製** | ✔ |   |   |
| **統合の追加/管理** | ✔ |   |   |
| **Data Warehouseマネージャーへのアクセス** | ✔ |   |   |
| **テーブルと列の同期/同期解除** | ✔ |   |   |
| **指標の作成/編集** | ✔ |   |   |
| **フィルターセットの作成/編集** | ✔ |   |   |
| **計算列の作成/編集** | ✔ |   |   |
| **依存レポートのリストの作成** | ✔ |   |   |
| **アクセスシステムの概要** | ✔ |   |   |
| **タイムゾーン設定へのアクセス** | ✔ |   |   |
| **アクセス課金** | ✔ | ✔** |   |
| **サポートへのお問い合わせ** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_**[!UICONTROL Standard]**ユーザーの [ アクセスを特定の指標に制限 ](../../administrator/user-management/restrict-metric-access.md) できます。_
>
>**[!UICONTROL Standard] _ユーザーは、追加の権限設定で請求にアクセスできます。_
>
>**[!UICONTROL Read-Only]** ユーザーは、共有されているダッシュボードのみを _表示_ できます。[!DNL Commerce Intelligence] でダッシュボードを作成または編集したり、新しいダッシュボードを検索してアカウントに追加したりすることはできません。 Adobeは、自分またはチームの別のメンバーが管理するユーザー **[!UICONTROL Read-Only]**、特定のダッシュボードセットを共有することをお勧めします。 それらのダッシュボードのセットのクローンを作成しないでください。

## その他の権限：請求および技術 {#billingtech}

一般的な権限レベルに加えて、`Billing` と `Technical` という 2 つの他のユーザー指定も存在します。 これらの指定は、一般的な権限レベルで使用する必要があります。

### 請求

`Billing` ユーザーは請求ページにアクセスでき、支払い情報を変更できます。 また、Adobeから請求に関する問い合わせが来ることもあります。

`Admin` ユーザーはデフォルトで「`Billing`」タブにアクセスできますが、プロファイルで「`Billing`」チェックボックスを選択している場合は、`Standard` ユーザーもアクセスできます。

![ 請求 ](../../assets/billing.png)<!--{: width="550" height="363"}-->

### 技術

`Technical` ユーザーには固有の権限がありません。この設定は、組織内の技術担当者をマークするだけです。 これらのユーザーには、Adobeから技術的な問い合わせがある場合があります。

`Admin` ユーザーは、**[!UICONTROL Account Settings]**/**[!UICONTROL Create Users]** をクリックし、プロンプトに従って、自分のアカウントに新しいユーザーを追加できます。 [!DNL Commerce Intelligence] でユーザーが作成されると、招待している幸運な人に、アカウント設定プロセスを完了する方法を説明するメールが届きます。

**[!UICONTROL Account Settings]**/**[!UICONTROL Manage Users]** をクリック `Admins` ると、アカウント内のすべてのユーザーをいつでも表示できます。 このページには、ユーザーの権限と、ユーザーがアクセスできる指標およびダッシュボードが表示されます。
