---
title: デクリタリング [!DNL Commerce Intelligence] アカウント
description: クリーンアップ方法を学ぶ [!DNL Commerce Intelligence] アカウント。
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# クリーンアップ [!DNL Adobe Commerce Intelligence] アカウント

一緒にいたかどうか [!DNL Commerce Intelligence] 6 か月か 6 年間、適切なアカウントを維持することは、組織がプラットフォームを最大限に活用する上で最も重要です。 時間の経過と共に、不要になったユーザー、ダッシュボード、レポート、指標および列が自然に存在します。 例えば、1 回限りの使用用にレポートを作成して忘れた場合や、会社を離脱したユーザーのアカウントを非アクティブ化しなかった場合などです。

を使用 [すべての要素に対して標準化され、明確な命名](../best-practices/naming-elements.md)) を [!DNL Commerce Intelligence] アカウント、以下のアカウント監査手順は、ユーザーにとって煩雑で不要な分析を減らすのに役立ちます。 その他の利点として、次のものがあります。 [更新サイクルが速くなる可能性がある](../best-practices/reduce-update-cycle-time.md).

## 手順 1：アクティブでないユーザーの特定

アカウントをクリーンアップする最初の手順は、会社を退社したユーザーや使用しなくなったユーザーなど、非アクティブなユーザーのアカウントを非アクティブ化することです [!DNL Commerce Intelligence] 現在の役割で使用されます。

これをおこなうには、右上のナビゲーションバーで会社の名前をクリックし、 **[!UICONTROL Manage Users]**. 次に、非アクティブ化するユーザーを選択し、 **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>必要な操作 [管理者権限](../administrator/user-management/user-management.md) 」をクリックします。

>[!WARNING]
>
>ユーザーを非アクティブ化すると、そのユーザーが作成したグラフ、ダッシュボード、およびその他のアセットが削除されます。 これらのアセットを保持する場合は、 [!DNL Commerce Intelligence] [サポート](../guide-overview.md#Submitting-a-Support-Ticket) チームを開いてください。 サポートは、これらのアセットを別のユーザーに転送する際に役立ちます。

### ユーザーの再アクティブ化

ユーザーを再アクティブ化するには、非アクティブ化されたのと同じ電子メールアドレスを持つアカウントを再作成し、ユーザーを再招待します。また、ユーザーのアクセス権と所有するデータがログイン時に復元されます。

## 手順 2：未使用のダッシュボードとレポートを削除する

アカウントを監査する次の手順は、未使用のダッシュボードとレポートを削除することです。

>[!NOTE]
>
>必要な操作 `Admin` または `Standard` [ユーザー権限](../administrator/user-management/user-management.md) 」をクリックします。

を持つすべてのユーザー `Admin` または `Standard` にアクセスして、レポートとダッシュボードを作成できます。 そのため、これらの権限を持つすべてのユーザーは、未使用のレポートを識別および削除するために、次の手順に従う必要があります。

### ダッシュボードとレポートの確認

何かを削除する前に、レポートとダッシュボードを確認して、何が使用されているかを評価する必要があります。 一方、 **[!UICONTROL find unused reports]** 以下に説明する機能を使用すると、初期レビューを行うと、クリーンアップ作業の生産性が大幅に向上します。

### ダッシュボードとレポートの削除

ダッシュボードとレポートにアクセスしたら、アカウントのクリーンアップを開始できます。

**ダッシュボードからレポートを削除するには**

1. ダッシュボードで、削除するレポートを見つけます。
1. 選択 **[!UICONTROL Options]** をクリックします。
1. クリック **[!UICONTROL Remove From Dashboard]**.

**ダッシュボード全体を削除するには**

1. 選択 **[!UICONTROL Manage Data]**&#x200B;その後、**[!UICONTROL Dashboards**].
1. 削除するダッシュボードをクリックします。
1. クリック **[!UICONTROL Delete Dashboard]**.

また、 **[!UICONTROL Dashboard Options]**&#x200B;を、 **[!UICONTROL Delete]** をダッシュボード自体に追加する必要があります。

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>ダッシュボードを削除しても、そのダッシュボード内のレポートは削除されないので、レポートを削除するには、もう 1 つ手順を実行する必要があります。

**未使用のレポートを削除するには**

1. 選択 **[!UICONTROL Manage Data]**&#x200B;を、 **[!UICONTROL Reports]**.
1. 次を確認します。 **未使用のレポートのみを表示** ボックスがメトリックリストの下に表示されます。 これにより、ダッシュボードや電子メールの概要で使用されないレポートのリストが作成されます。
1. 削除するレポートを選択します。 レポートリストの上にあるチェックボックスをクリックして、「すべて」を選択できます。
1. クリック **[!UICONTROL Delete Selected]**.

未使用レポートの削除プロセスを次に示します。

![](../../mbi/assets/unused_reports.png)

## 手順 3：未使用の指標の削除

ユーザーのリスト、ダッシュボード、レポートを消去した後は、指標のリストの監査に進むことができます。 これにより、古くなっている（例えば、異なる定義で新しい指標が作成された）、または使用されていない ) 可能性があるものを識別できます。

1. 指標の依存レポートのリストを生成するには、に移動します。 **[!DNL Manage Data]**&#x200B;をクリックし、「 **[!UICONTROL Metrics]**.
1. クリック **[!UICONTROL Edit]** 指標の横に表示されます。
1. ページの下部に、「 **[!UICONTROL Dependent Charts]**. リンクをクリックして、この指標の依存レポートリストを生成します。
1. システムがチェックを完了した後、 [!DNL Commerce Intelligence] この指標を使用するダッシュボード、レポート、およびユーザーのリストを表示します。

![](../../mbi/assets/report_dependecies.png)

指標が不要になった場合は、 **[!UICONTROL Metrics]** ページをクリックして **[!UICONTROL Back to Metric List]** をクリックして、削除する指標を見つけます。 クリック **[!UICONTROL Delete]**.

## 手順 4：同期された列を評価する

最後の手順は、現在Data Warehouse内で同期中の列を評価することです。 アカウントの同期を解除できるだけでなく、更新時間が短縮される可能性もあります。

これを追跡したい場合は、 [!DNL Commerce Intelligence] [サポート](../guide-overview.md#Submitting-a-Support-Ticket). サポートチームは、SQL レポートを除く、どのユーザーのダッシュボードでも使用されていないすべての列と、電子メールの概要で使用されていない列を含むレポートを作成できます。 その後、このレポートを使用して、同期を解除する列を選択するためのガイドとして、Data Warehouseマネージャーで使用できます。

>[!NOTE]
>
>これらの列の同期は、今後もいつでも開始できます。 列の同期を解除すると、Data Warehouseーからデータが削除されます。これは、更新サイクル中に、この列で新しい値や更新された値がチェックされないことを意味します。

**列（または列）の同期を解除するには**

1. に移動します。 **[!DNL Manage Data]**&#x200B;を、 **[!UICONTROL Data Warehouse]**.
1. Adobe Analytics の **[!UICONTROL Synced Tables]** リストを開き、列を含むテーブルに移動します。
1. 同期を解除する 1 つ以上の列の横にある 1 つ以上のチェックボックスをオンにします。
   >[!NOTE]
   >
   >テーブル全体を削除せずにプライマリキー列の同期を解除することはできません。

1. クリック **[!UICONTROL Remove]** :1 つ以上の列の同期を解除します。

プロセス全体を以下に示します。

![](../../mbi/assets/drop_column.png)

## 折り返し

お使いの [!DNL Commerce Intelligence] アカウントは今、お客様とチームの間で簡単に移動できるようになります。
