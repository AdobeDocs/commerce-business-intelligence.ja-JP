---
title: 自動メール要約の作成
description: 電子メールの自動要約の作成方法。
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/e6PatGqkzOXmxOYhzvDEkNrXCktjz3rIVWkxhleG4mI
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 604
ht-degree: 0%

---

# 自動メール要約の作成

メールによる要約は、ビジネスの状況と傾向を主要な関係者と共有するための強力なコミュニケーションツールです。 メール要約を活用すると、次のことが可能になります。

* レポートを含む電子メールのグラフィック概要
* メールの概要の作成者をメールの受信に含めるか除外する
* メールの送信日をスケジュール
* 既存のスケジュール済みメールの要約の編集、削除、一時停止

## 新しいメール概要の作成

1. サイドバーで「**[!DNL Manage Data]**」、「**[!UICONTROL Email Summary]**」の順にクリックします。

   メールの要約を初めて作成する場合、このページには保存された要約は表示されません。

1. 右上隅の&#x200B;**[!UICONTROL Create New Email Summary]**&#x200B;をクリックします。

1. 概要の名前を入力します。

   要約に含まれる内容を表す名前を選択します。 例：`AOV Comparison`。

1. `Choose Content` セクションで、概要に含めるレポートを選択します。

   コンテンツを追加するには、次の2つのオプションがあります。

   * **個別レポートの選択** - ダッシュボードから特定のレポートを選択します
   * **ダッシュボード全体を選択** - ダッシュボードのレイアウトに表示されるダッシュボードのすべてのレポートを含める

   所有しているレポートは最大10個まで選択できます。 レポートを選択したら、表示されるアイコンを使用して、そのレポートを表またはグラフとして送信するかどうかを選択します。 レポートを数値として保存した場合は、数値としてのみ送信できます。 古いデータを含むレポートを含むメール概要の送信について詳しくは、[ アカウント設定の管理](../../administrator/account-management/managing-account-settings.md)を参照してください。

   ダッシュボード全体を追加するには、次の形式および削除オプションがあります。

   * レポートの形式をグラフまたは表に変更する
   * レポートをメールに含めることから削除
   * 表形式のレポート用にCSV ファイルを含める場合に選択します。これにより、受信者は受信トレイから生のエクスポート可能なデータに直接アクセスできます。

   >[!NOTE]
   >
   >`Cohort`件のレポートは、新しいアーキテクチャを使用している場合にのみ使用できます。

   >[!NOTE]
   >
   >CSVの大きな添付ファイルは、メールごとに合計25 MBまでサポートされます。

1. （オプション）電子メールを受信する場合は、`Send Email To Me`を選択します。

1. メールに他のユーザーを含めるには、コンマ、スペース、タブ、またはセミコロンで区切った`Add Email Recipients` フィールドにメールアドレスを入力します。

## メール概要のスケジュール

「`Set when to send the Email Summary`」フィールドで、メールの要約を送信するタイミングを指定できます。 オプションは次のとおりです。

* `Manual`
* `Once`
* `Repeating`

### 後日に送信するメールの概要を保存

1. `Manual` フィールドから`Set when to send the Email Summary`を選択します。

1. **[!UICONTROL Save]**&#x200B;をクリックします。

   これにより、要約がメール要約のリストに保存されます。

1. 概要を送信する準備ができたら、歯車アイコンをクリックし、`Send Now`を選択します。

### メール概要を1回送信

1. `Once` フィールドから`Set when to send the Email Summary`を選択します。

1. `Select Start Date` カレンダーで開始日を指定します。

1. `Select time to send` フィールドでメールを送信する時間を指定します。

### リピートスケジュールの作成

1. `Repeating` フィールドから`Set when to send the Email Summary`を選択します。

1. `Set Frequency` フィールドで、`Daily`、`Weekly`または`Monthly`を選択します。

1. `Select Start Date` カレンダーで開始日を指定します。

1. `Select time to send` フィールドでメールを送信する時間を指定します。

1. （オプション）終了日を指定するには、`End Date`を選択し、カレンダーから終了日を選択します。

## 既存のメール概要の変更

電子メールの概要を作成して保存すると、`Email Summaries` ページに保存されたすべての概要のリストが表示されます。 詳細については、各行の（`+`）を展開できます。 このビューの列は次のとおりです。

* `Email Name` - メールの概要の名前
* `Content` - サマリー内のコンテンツの種類（任意のレポートの名前など）
* `Scheduled` - メールの概要が送信される頻度、日付、時間
* `Recipients` - メール概要の受信者
* `Created Date` - メールの概要が作成された日付
* `Status` - `Paused`または`Active`

>[!NOTE]
>
>古いデータを含むレポートを含むメール概要の送信について詳しくは、[ アカウント設定の管理](../../administrator/account-management/managing-account-settings.md)を参照してください。

各行の右側にある歯車アイコンをクリックして、次の操作を行います。

* `Send Now` – 指定されたすべての受信者にメールの概要を即座に送信します
* `Edit` - メールの概要の詳細を変更します
* `Pause/Active` - メールの概要の配信を一時停止またはアクティブ化します
* `Delete` - メールの概要を削除します
