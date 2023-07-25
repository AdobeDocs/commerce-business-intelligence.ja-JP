---
title: Adobe Commerceユーザーと権限の管理
description: Commerce Intelligence ユーザーの管理方法を説明します。
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# ユーザー権限の管理

[!DNL Adobe Commerce Intelligence] は、組織全体の単一の情報源となることを意図しています。 各ユーザーは、独自のダッシュボードセットを持ち、これを実行できます [他のユーザーと共有する](../../data-user/dashboards/share-dashboard-with-users.md).

## ユーザー権限レベル

In [!DNL Commerce Intelligence]には、ユーザーに適用される次の 3 つの一般的な権限レベルがあります。これらはアカウントの作成時に選択されます。

* `Admin`
* `Standard`
* `Read-Only`

これらの権限を使用すると、ユーザーは特定のアクションを実行したり、 [!DNL Commerce Intelligence]. 次に、各権限レベルで実行できる操作の表を示します。 [!DNL Commerce Intelligence]:

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **ユーザーを作成/管理** | ✔ |   |   |
| **電子メールの概要の作成** | ✔ | ✔ |   |
| **ダッシュボードの作成、編集、共有** | ✔ | ✔ |   |
| **ダッシュボードを表示** | ✔ | ✔ | ✔ |
| **ビジュアルレポートを作成/編集/削除** | ✔ | ✔* |   |
| **SQL レポートの作成/編集/削除** | ✔ |  |   |
| **ダッシュボードの複製** | ✔ |   |   |
| **統合を追加/管理** | ✔ |   |   |
| **Data Warehouseマネージャへのアクセス** | ✔ |   |   |
| **テーブルと列の同期/非同期** | ✔ |   |   |
| **指標の作成/編集** | ✔ |   |   |
| **フィルターセットを作成/編集** | ✔ |   |   |
| **計算列を作成/編集** | ✔ |   |   |
| **依存レポートのリストの作成** | ✔ |   |   |
| **アクセスシステムの概要** | ✔ |   |   |
| **タイムゾーン設定にアクセス** | ✔ |   |   |
| **請求にアクセス** | ✔ | ✔** |   |
| **サポートに連絡** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_次の項目を制限できます。**[!UICONTROL Standard]**ユーザーの [特定の指標へのアクセス](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _ユーザーは、追加の権限設定で請求にアクセスできます。_
>
>**[!UICONTROL Read-Only]** ユーザーは次のみを実行できます _表示_ ダッシュボードが共有されていること。内で何も作成または編集できない [!DNL Commerce Intelligence]また、アカウントで新しいダッシュボードを検索して追加することもできません。 Adobeは、特定のダッシュボードセットをと共有することをお勧めします。 **[!UICONTROL Read-Only]** 自分やチームの他のメンバーが管理するユーザー ダッシュボードのセットを複製しないでください。

## 追加の権限：請求と技術 {#billingtech}

一般的な権限レベルに加えて、他にも 2 つのユーザー指定が存在します。 `Billing` および `Technical`. これらの指定は、一般的な権限レベルで使用する必要があります。

### 請求

`Billing` ユーザーは請求ページにアクセスでき、支払い情報を変更できます。 また、請求に関する質問にAdobeから連絡を受ける場合もあります。

`Admin` ユーザーは `Billing` タブはデフォルトでは表示されますが、 `Standard` ユーザーは、 `Billing` チェックボックスをオンにしているかどうかを把握できます。

![課金](../../assets/billing.png)<!--{: width="550" height="363"}-->

### 技術

`Technical` ユーザーに固有の権限がありません。この設定は、組織内の技術的な連絡先を示すだけです。 これらのユーザーは、技術的な質問に対してAdobeから連絡を受ける場合があります。

`Admin` ユーザーは、 **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** プロンプトに従って ユーザーが [!DNL Commerce Intelligence]招待しているラッキーな人には、アカウント設定プロセスの完了方法に関する電子メールの指示が届きます。

いつでも `Admins` は、 **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. このページには、ユーザーの権限と、ユーザーがアクセスできる指標およびダッシュボードが表示されます。
