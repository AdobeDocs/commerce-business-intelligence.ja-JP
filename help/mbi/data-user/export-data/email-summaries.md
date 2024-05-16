---
title: 自動メール概要の作成
description: 自動メール概要を作成する方法を説明します。
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 自動メール概要の作成

メールの概要は、ビジネスのステータスやトレンドを主要な関係者と共有するために使用できる、強力なコミュニケーションツールです。 メールの概要を使用すると、次のことができます。

* レポートを含む電子メールのグラフィカルな要約
* 電子メールの概要作成者を電子メールの受信に含めるか除外する
* メールの送信時にスケジュールを設定
* 既存のスケジュール済み電子メール概要の編集、削除、および一時停止

## 新しい電子メールの概要を作成

1. クリック **[!DNL Manage Data]** その後 **[!UICONTROL Email Summary]** サイドバーで。

   メールの概要を初めて作成する場合は、保存された概要はこのページに表示されません。

1. クリック **[!UICONTROL Create New Email Summary]** 右上隅

1. 概要の名前を入力します。

   概要に含まれる内容を伝える名前を選択します。 例： `AOV Comparison`.

1. が含まれる `Choose Content` セクションで、概要に含めるレポートを選択します。

   所有するレポートは最大 10 個まで選択できます。 レポートを選択した後、表示されるアイコンを使用して、そのレポートをテーブルとして送信するかグラフとして送信するかを選択します。 レポートを数値として保存した場合、送信できるのは数値のみです。 古いデータを含むレポートを含むメールサマリーの送信について詳しくは、以下を参照してください。 [アカウント設定の管理](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` レポートは、新しいアーキテクチャを使用している場合にのみ使用できます。

1. （オプション）を選択 `Send Email To Me` メールを受信する場合。

1. 他のユーザーを含めてメールを送信するには、そのユーザーのメールアドレスを `Add Email Recipients` コンマ、スペース、タブ、セミコロンで区切られたフィールド。

## スケジュール メールの概要

が含まれる `Set when to send the Email Summary` フィールドに、メール概要を送信するタイミングを指定できます。 オプションは次のとおりです。

* `Manual`
* `Once`
* `Repeating`

### 後日送信するメールの概要を保存

1. を選択 `Manual` から `Set when to send the Email Summary` フィールド。

1. クリック **[!UICONTROL Save]**.

   これにより、概要がメール概要のリストに保存されます。

1. 概要を送信する準備が整ったら、歯車アイコンをクリックし、以下を選択します。 `Send Now`.

### メールの概要を 1 回送信

1. を選択 `Once` から `Set when to send the Email Summary` フィールド。

1. で開始日を指定 `Select Start Date` カレンダー。

1. でメールを送信する時間を指定 `Select time to send` フィールド。

### 繰り返しスケジュールの作成

1. を選択 `Repeating` から `Set when to send the Email Summary` フィールド。

1. が含まれる `Set Frequency` フィールド、選択 `Daily`, `Weekly`、または `Monthly`.

1. で開始日を指定 `Select Start Date` カレンダー。

1. でメールを送信する時間を指定 `Select time to send` フィールド。

1. （オプション）終了日を指定するには、 `End Date` カレンダーから終了日を選択します。

## 既存の電子メールの概要の変更

メールの概要を作成して保存した後、 `Email Summaries` ページには、すべての保存済みの要約のリストが表示されます。 を展開できます（`+`）を選択します。 このビューの列は次のとおりです。

* `Email Name` - メールの概要の名前
* `Content`  – 報告書名など、概要内の内容のタイプ。 古いデータを含むレポートを含むメールサマリーの送信について詳しくは、以下を参照してください。 [アカウント設定の管理](../../administrator/account-management/managing-account-settings.md).
* `Scheduled` - E メール概要を送信する頻度、日時
* `Recipients` - メールの概要の受信者
* `Created Date` - メールの概要が作成された日付
* `Status` - `Paused` または `Active`

各行の右側にある歯車アイコンをクリックして、次の操作を実行します。

* `Send Now`  – 指定されたすべての受信者にメールの概要をすぐに送信します
* `Edit`  – 電子メールの概要の詳細を変更できます
* `Pause/Active`  – 概要の配信を一時停止したり、設定方法に基づいて概要を有効にしたりできます
* `Delete`  – 電子メールの概要を削除します
