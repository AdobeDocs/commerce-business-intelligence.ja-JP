---
title: 自動電子メールの概要の作成
description: 自動電子メールの概要を作成する方法を説明します。
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# 自動電子メールの概要の作成

E メールの概要は、主要な関係者とビジネスの現在の状況や傾向を共有するために使用できる強力なコミュニケーションツールです。 E メールの概要を使用すると、次のことができます。

* レポートを含むグラフィカルな概要を電子メールで送信
* 電子メールの概要作成者を電子メールの受信に含めるか除外します
* E メールの送信スケジュール
* スケジュール済みの既存の電子メールの概要を編集、削除、一時停止します

## 新しいメールサマリの作成

1. クリック **[!DNL Manage Data]** その後 **[!UICONTROL Email Summary]** サイドバーに表示されます。

   電子メールの概要を初めて作成する場合、このページには保存された概要は表示されません。

1. クリック **[!UICONTROL Create New Email Summary]** をクリックします。

1. 要約の名前を入力します。

   概要に含まれる内容を表す名前を選択します。 例： `AOV Comparison`.

1. 内 `Choose Content` セクションで、サマリに含めるレポートを選択します。

   所有するレポートは最大 10 個選択できます。 レポートを選択した後、表示されるアイコンを使用して、そのレポートを表またはグラフとして送信するかどうかを選択します。 レポートを数値として保存した場合は、数値としてのみ送信できます。 古いデータを含むレポートを含む電子メールの概要を送信する方法については、 [アカウント設定の管理](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` レポートは、新しいアーキテクチャを使用している場合にのみ使用できます。

1. （オプション）「 」を選択します。 `Send Email To Me` 電子メールを受信する場合。

1. 電子メールに他のユーザーを含めるには、「 `Add Email Recipients` コンマ、スペース、タブまたはセミコロンで区切られたフィールド。

## スケジュールメールの概要

内 `Set when to send the Email Summary` 「 」フィールドでは、電子メールの概要を送信するタイミングを指定できます。 オプションは次のとおりです。

* `Manual`
* `Once`
* `Repeating`

### 後日送信する電子メールの概要を保存

1. 選択 `Manual` から `Set when to send the Email Summary` フィールドに入力します。

1. クリック **[!UICONTROL Save]**.

   これにより、概要が E メールの概要のリストに保存されます。

1. 概要を送信する準備が整ったら、歯車アイコンをクリックし、「 `Send Now`.

### メールサマリを 1 回送信

1. 選択 `Once` から `Set when to send the Email Summary` フィールドに入力します。

1. 開始日を `Select Start Date` カレンダー。

1. 電子メールを送信する時間を `Select time to send` フィールドに入力します。

### 繰り返しスケジュールを作成

1. 選択 `Repeating` から `Set when to send the Email Summary` フィールドに入力します。

1. 内 `Set Frequency` フィールド、選択 `Daily`, `Weekly`または `Monthly`.

1. 開始日を `Select Start Date` カレンダー。

1. 電子メールを送信する時間を `Select time to send` フィールドに入力します。

1. （オプション）終了日を指定するには、 `End Date` カレンダーから終了日を選択します。

## 既存のメールの概要の変更

電子メールの概要を作成して保存すると、 `Email Summaries` ページには、保存されたすべての概要のリストが表示されます。 を展開できます (`+`) をクリックして、詳細を確認します。 このビューの列は次のとおりです。

* `Email Name`  — 電子メールの概要の名前
* `Content`  — レポート名など、概要内のコンテンツのタイプ。 古いデータを含むレポートを含む電子メールの概要を送信する方法については、 [アカウント設定の管理](../../administrator/account-management/managing-account-settings.md).
* `Scheduled`  — 電子メールの概要が送信される頻度、日付、時刻
* `Recipients` - E メールサマリの受信者
* `Created Date`  — 電子メールの概要が作成された日付
* `Status` - `Paused` または `Active`

各行の右側の歯車アイコンをクリックして、次の操作を実行します。

* `Send Now`  — 指定したすべての受信者に電子メールの概要を直ちに送信します
* `Edit` - E メールの概要の詳細を変更できます
* `Pause/Active`  — 電子メールの概要が配信されるのを一時停止したり、設定に基づいて概要を有効にしたりできます
* `Delete`  — 電子メールの概要を削除します
