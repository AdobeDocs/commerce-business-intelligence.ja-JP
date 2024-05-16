---
title: の除外 [!DNL Commerce Intelligence] アカウント
description: のクリーンアップ方法を説明します [!DNL Commerce Intelligence] アカウント。
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 0%

---

# のクリーンアップ [!DNL Adobe Commerce Intelligence] アカウント

今まで一緒にいたかどうか [!DNL Commerce Intelligence] 6 か月または 6 年間、きちんとアカウントを維持することは、プラットフォームを最大限に活用する組織にとって最も重要です。 時間の経過と共に、不要になったユーザー、ダッシュボード、レポート、指標および列が存在するのは当然です。 1 回限りのレポートを作成してそれを忘れた場合や、会社を離れたときにアカウントを非アクティブ化しなかったユーザーの場合があります。

（を使用） [すべての要素に標準化された明確な名前を付ける](../best-practices/naming-elements.md)） [!DNL Commerce Intelligence] アカウント、以下のアカウント監査手順は、ユーザーにとって煩雑で不要な分析を減らすのに役立ちます。 その他のメリットとして、次のものがあります [更新サイクルの高速化が可能](../best-practices/reduce-update-cycle-time.md).

## 手順 1：非アクティブユーザーの特定

アカウントを整理する最初の手順は、会社を退社したユーザーや使用しなくなったユーザーなど、非アクティブなユーザーのアカウントをディアクティベートすることです [!DNL Commerce Intelligence] 現在の役割

これを行うには – 右上のナビゲーションバーで会社名をクリックし、次のいずれかを選択します。 **[!UICONTROL Manage Users]**. 次に、ディアクティベートするユーザーを選択し、 **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>必要です [管理者権限](../administrator/user-management/user-management.md) をクリックします。

>[!WARNING]
>
>ユーザーをディアクティベートすると、そのユーザーが作成したグラフ、ダッシュボード、その他のアセットが削除されます。 これらのアセットを保持する場合は、 [!DNL Commerce Intelligence] [サポート](../guide-overview.md#Submitting-a-Support-Ticket) ユーザーを非アクティブ化する前にチーム化します。 サポートは、これらのアセットを別のユーザーに転送する際に役立ちます。

### ユーザーの再アクティブ化

ユーザーを再アクティブ化するには、非アクティブ化されたのと同じメールアドレスでアカウントを再作成して、ユーザーを再び招待します。ユーザーのアクセスと所有していたデータは、ログイン時に復元されます。

## 手順 2：未使用のダッシュボードとレポートの削除

アカウントを監査する次の手順では、未使用のダッシュボードとレポートを削除します。

>[!NOTE]
>
>必要です `Admin` または `Standard` [ユーザー権限](../administrator/user-management/user-management.md) をクリックします。

を使用するすべてのユーザー `Admin` または `Standard` access では、レポートとダッシュボードを作成できます。 そのため、これらの権限を持つユーザーは全員、次の手順に従って未使用のレポートを特定し、削除する必要があります。

### ダッシュボードとレポートのレビュー

何かを削除する前に、レポートとダッシュボードで使用状況を評価する必要があります。 を使用できます **[!UICONTROL find unused reports]** 機能について以下で説明します。最初のレビューを行うと、クリーンアップ作業の生産性がはるかに高まります。

### ダッシュボードと報告書の削除

ダッシュボードとレポートにアクセスしたら、アカウントのクリーンアップを開始できます。

**ダッシュボードからレポートを削除するには**

1. ダッシュボードで、削除するレポートを見つけます。
1. を選択 **[!UICONTROL Options]** レポートの右上隅
1. クリック **[!UICONTROL Remove From Dashboard]**.

**ダッシュボード全体を削除するには**

1. を選択 **[!UICONTROL Manage Data]**、次に**[!UICONTROL Dashboards**].
1. 削除するダッシュボードをクリックします。
1. クリック **[!UICONTROL Delete Dashboard]**.

以下を選択することもできます。 **[!UICONTROL Dashboard Options]**、次に **[!UICONTROL Delete]** ダッシュボード自体から。

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>ダッシュボードを削除しても、その中のレポートは削除されないので、レポートを削除するには、もう 1 つの手順を実行する必要があります。

**未使用のレポートを削除するには**

1. を選択 **[!UICONTROL Manage Data]**、次に **[!UICONTROL Reports]**.
1. を確認します **未使用のレポートのみを表示** 指標リストの下にあるボックス。 これにより、ダッシュボードやメールの概要で使用されないレポートのリストが作成されます。
1. 削除するレポートを選択します。 レポートリストの上にあるチェックボックスをクリックして、すべてを選択できます。
1. クリック **[!UICONTROL Delete Selected]**.

未使用のレポート削除プロセスを次に示します。

![](../../mbi/assets/unused_reports.png)

## 手順 3：未使用の指標の削除

ユーザーリスト、ダッシュボードおよびレポートをクリーンアップしたら、指標のリストの監査に進むことができます。 これにより、古くなっている可能性のあるもの（例えば、新しい指標が別の定義で作成された、使用されていないなど）を識別できます。

1. 指標の依存レポートのリストを生成するには、次に移動します **[!DNL Manage Data]**&#x200B;を選択し、「クリック」を選択します **[!UICONTROL Metrics]**.
1. クリック **[!UICONTROL Edit]** 指標の横。
1. ページの下部に、というセクションが表示されます。 **[!UICONTROL Dependent Charts]**. リンクをクリックして、この指標の依存レポートリストを生成します。
1. システムがチェックを完了したら、 [!DNL Commerce Intelligence] この指標を使用しているダッシュボード、レポートおよびユーザーのリストを表示します。

![](../../mbi/assets/report_dependecies.png)

指標が不要になった場合は、に戻ります **[!UICONTROL Metrics]** をクリックしたページ **[!UICONTROL Back to Metric List]** 削除する指標を見つけます。 クリック **[!UICONTROL Delete]**.

## 手順 4：同期された列を評価

最後の手順は、Data Warehouseで現在同期されている列を評価することです。 列の同期を解除すると、アカウントの表示を減らすだけでなく、更新時間を短縮する可能性もあります。

これを追求する場合は、次のアドレスに連絡してください： [!DNL Commerce Intelligence] [サポート](../guide-overview.md#Submitting-a-Support-Ticket). サポートチームは、どのユーザーのダッシュボードでも使用されておらず、電子メールの概要でも使用されていないすべての列を含むレポート（SQL レポートを除く）を作成できます。 その後、このレポートをガイドとして使用し、Data Warehouseマネージャーで同期を解除する列を選択できます。

>[!NOTE]
>
>これらの列の同期は、今後いつでも再開できます。 列の同期を解除すると、Data Warehouseからデータが削除されます。つまり、更新サイクル中にこの列の新しい値や更新された値はチェックされません。

**列の同期を解除するには、次の手順に従います**

1. に移動 **[!DNL Manage Data]**、次に **[!UICONTROL Data Warehouse]**.
1. が含まれる **[!UICONTROL Synced Tables]** リストで、列を含むテーブルに移動します。
1. 同期を解除する 1 つ以上の列の横にある 1 つ以上のチェックボックスをオンにします。
   >[!NOTE]
   >
   >テーブル全体を削除しないと、プライマリキー列の同期を解除できません。

1. クリック **[!UICONTROL Remove]** :1 つ以上の列の同期を解除します。

プロセス全体を見ると、次のようになります。

![](../../mbi/assets/drop_column.png)

## まとめ

あなたの [!DNL Commerce Intelligence] アカウントは、ユーザーとチームにとって今までよりも整理され、ナビゲーションが容易になっているはずです。
