---
title: Adobe Commerceのユーザーと権限の管理
description: Commerce Intelligence ユーザーの管理方法について説明します。
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# ユーザー権限の管理

[!DNL Adobe Commerce Intelligence] は、組織全体の唯一の情報源となることを目的としています。 各ユーザーは、独自のダッシュボードのセットを持ち、それらを [&#x200B; 他のユーザーと共有 &#x200B;](../../data-user/dashboards/share-dashboard-with-users.md) できます。

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
| **Data Warehouse Manager へのアクセス** | ✔ |   |   |
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
>_&#x200B;**[!UICONTROL Standard]**&#x200B;ユーザーの [&#x200B; アクセスを特定の指標に制限 &#x200B;](../../administrator/user-management/restrict-metric-access.md) できます。_
>
>**[!UICONTROL Standard] _ユーザーは、追加の権限設定で請求にアクセスできます。_
>
>**[!UICONTROL Read-Only]** ユーザーは、共有されているダッシュボードのみを _表示_ できます。[!DNL Commerce Intelligence] でダッシュボードを作成または編集したり、新しいダッシュボードを検索してアカウントに追加したりすることはできません。 Adobeでは、自分またはチームの別のメンバーが管理する **[!UICONTROL Read-Only]** ユーザーと、特定のダッシュボードセットを共有することをお勧めします。 それらのダッシュボードのセットのクローンを作成しないでください。

## その他の権限：請求および技術 {#billingtech}

一般的な権限レベルに加えて、`Billing` と `Technical` という 2 つの他のユーザー指定も存在します。 これらの指定は、一般的な権限レベルで使用する必要があります。

### 請求

`Billing` ユーザーは請求ページにアクセスでき、支払い情報を変更できます。 また、Adobeから請求に関する連絡を受ける場合もあります。

`Admin` ユーザーはデフォルトで「`Billing`」タブにアクセスできますが、プロファイルで「`Standard`」チェックボックスを選択している場合は、`Billing` ユーザーもアクセスできます。

![&#x200B; 請求ページ &#x200B;](../../assets/billing.png)<!--{: width="550" height="363"}-->

### 技術

`Technical` ユーザーには固有の権限がありません。この設定は、組織内の技術担当者をマークするだけです。 これらのユーザーには、Adobeから技術的な問い合わせがある場合があります。

`Admin` ユーザーは、**[!UICONTROL Account Settings]**/**[!UICONTROL Create Users]** をクリックし、プロンプトに従って、自分のアカウントに新しいユーザーを追加できます。 [!DNL Commerce Intelligence] でユーザーが作成されると、招待している幸運な人に、アカウント設定プロセスを完了する方法を説明するメールが届きます。

`Admins`/**[!UICONTROL Account Settings]** をクリック **[!UICONTROL Manage Users]** ると、アカウント内のすべてのユーザーをいつでも表示できます。 このページには、ユーザーの権限と、ユーザーがアクセスできる指標およびダッシュボードが表示されます。
