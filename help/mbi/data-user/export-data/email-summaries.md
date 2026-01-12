---
title: 自動メール概要の作成
description: 自動メール概要を作成する方法を説明します。
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: a65ededb203b7551fdfcb31cff130ef85b01fbe3
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# 自動メール概要の作成

メールの概要は、ビジネスのステータスやトレンドを主要な関係者と共有するために使用できる、強力なコミュニケーションツールです。 メールの概要を使用すると、次のことができます。

* レポートを含む電子メールのグラフィカルな要約
* 電子メールの概要作成者を電子メールの受信に含めるか除外する
* メールの送信時にスケジュールを設定
* 既存のスケジュール済み電子メール概要の編集、削除、および一時停止

## 新しい電子メールの概要を作成

1. サイドバ **[!DNL Manage Data]** の「**[!UICONTROL Email Summary]**」をクリックします。

   メールの概要を初めて作成する場合は、保存された概要はこのページに表示されません。

1. 右上隅の「**[!UICONTROL Create New Email Summary]**」をクリックします。

1. 概要の名前を入力します。

   概要に含まれる内容を伝える名前を選択します。 例：`AOV Comparison`。

1. [`Choose Content`] セクションで、概要に含めるレポートを選択します。

   コンテンツを追加する方法は 2 つあります。

   * **個々のレポートを選択** - ダッシュボードから特定のレポートを選択します
   * **ダッシュボード全体を選択** - ダッシュボードのレイアウトに表示されるすべてのレポートを含めます

   所有するレポートは最大 10 個まで選択できます。 レポートを選択した後、表示されるアイコンを使用して、そのレポートをテーブルとして送信するかグラフとして送信するかを選択します。 レポートを数値として保存した場合、送信できるのは数値のみです。 古いデータを含むレポートを含むメールの概要の送信について詳しくは、[ アカウント設定の管理 ](../../administrator/account-management/managing-account-settings.md) を参照してください。

   ダッシュボード全体を追加する場合、次の形式および削除オプションがあります。

   * レポートの形式をグラフまたはテーブルに変更する
   * レポートを E メールに含めない
   * 表形式レポートに CSV ファイルを含める場合に選択します。これにより、受信者は、インボックスから直接、エクスポート可能な生のデータにアクセスできます。

   >[!NOTE]
   >
   >`Cohort` のレポートは、新しいアーキテクチャを使用している場合にのみ使用できます。

   >[!NOTE]
   >
   >大きな CSV 添付ファイルは、1 つのメールにつき合計 25 MB までサポートされます。

1. （オプション）メールを受信する場合は、「`Send Email To Me`」を選択します。

1. メールに他のユーザーを含めるには、`Add Email Recipients` フィールドにメールアドレスをコンマ、スペース、タブ、セミコロンで区切って入力します。

## スケジュールのメールの概要

「`Set when to send the Email Summary`」フィールドでは、メールの概要を送信するタイミングを指定できます。 オプションは次のとおりです。

* `Manual`
* `Once`
* `Repeating`

### 後日送信するメールの概要を保存

1. 「`Manual`」フィールドから「`Set when to send the Email Summary`」を選択します。

1. 「**[!UICONTROL Save]**」をクリックします。

   これにより、概要がメール概要のリストに保存されます。

1. 概要を送信する準備が整ったら、歯車アイコンをクリックし、「`Send Now`」を選択します。

### メールの概要を 1 回送信

1. 「`Once`」フィールドから「`Set when to send the Email Summary`」を選択します。

1. `Select Start Date` カレンダーで開始日を指定します。

1. メールを送信する時間を「`Select time to send`」フィールドに指定します。

### 繰り返しスケジュールの作成

1. 「`Repeating`」フィールドから「`Set when to send the Email Summary`」を選択します。

1. 「`Set Frequency`」フィールドで、「`Daily`」、「`Weekly`」または「`Monthly`」を選択します。

1. `Select Start Date` カレンダーで開始日を指定します。

1. メールを送信する時間を「`Select time to send`」フィールドに指定します。

1. （オプション）終了日を指定するには、「`End Date`」を選択し、カレンダーから終了日を選択します。

## 既存の電子メールの概要の変更

メールの概要を作成して保存すると、`Email Summaries` のページに保存されたすべての概要のリストが表示されます。 詳細については、各行の（`+`）を展開してください。 このビューの列は次のとおりです。

* `Email Name` - メールの概要の名前
* `Content` - レポート名など、概要内のコンテンツのタイプ
* `Scheduled` - メールの概要を送信する頻度、日付、時刻
* `Recipients` - メールの概要の受信者
* `Created Date` - メールの概要が作成された日付
* `Status` - `Paused` または `Active`

>[!NOTE]
>
>古いデータを含むレポートを含むメールの概要の送信について詳しくは、[ アカウント設定の管理 ](../../administrator/account-management/managing-account-settings.md) を参照してください。

各行の右側にある歯車アイコンをクリックして、次の操作を実行します。

* `Send Now` – 指定したすべての受信者にメールの概要をすぐに送信します
* `Edit` - メール概要の詳細を変更します
* `Pause/Active` - メールの概要配信を一時停止または有効化します
* `Delete` - メールの概要を削除します
