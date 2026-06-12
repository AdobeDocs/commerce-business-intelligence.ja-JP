---
title: SSH ホスト キーの検証
description: Commerce IntelligenceがSSH ホストキーを登録する方法、更新する方法、エラーのトラブルシューティング、SSH トンネル接続のサポートへの問い合わせタイミングについて説明します。
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
source-git-commit: b51e9fceba0c62f4ef3dde340d26cd78641ef3a2
workflow-type: tm+mt
source-wordcount: 1130
ht-degree: 0%

---

# SSH ホスト キーの検証 {#ssh-host-keys}

[!DNL Commerce Intelligence]は、[MySQL](mysql-via-ssh-tunnel.md)、[MongoDB](mongodb-via-ssh-tunnel.md)、[PostgreSQL](postgresql.md)などの暗号化（SSH トンネル）データベース接続に対して厳格なSSH ホスト キー検証を使用します。

**[!UICONTROL Save & Test]**&#x200B;の間、システムは接続のSSH バスティョンホストキーを登録し、接続ごとに安全に保存します。 登録後、ライブバスティオンホストキーが登録済みキーと一致した場合にのみ、レプリケーションとトンネリングが成功します。

このモデルは、中間者攻撃や予想外のホスト変更をブロックすることで、セキュリティを向上させます。 また、ホストキーのローテーション、信頼マテリアルの欠落、インフラストラクチャの変更が、一般的なトンネル障害ではなく、接続のSSH ホストキーエラーとして表示される可能性もあります。

>[!NOTE]
>
>**管理者**&#x200B;とは、[!DNL Commerce Intelligence] アカウントの管理者権限を持つユーザーを意味し、特に明記されていない限り、Adobe組織コンソールではありません。 管理者のみが&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;を実行できます。 このコントロールが表示されない場合は、アカウントの管理者に更新を実行するように依頼するか、Adobe サポートにお問い合わせください。

`known_hosts`個のファイルを編集、アップロード、管理することはできません。 アカウントに割り当てられたAdobe インフラストラクチャで登録と更新を実行します。

>[!IMPORTANT]
>
>ホスト キーのローテーションには、管理者が&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;を実行する必要があります。 Bastion ホストキーが変更されたか、Bastion ID （ホスト名、IP、またはポート）が変更された場合、**[!UICONTROL Save & Test]**&#x200B;を再度実行するか、接続を再保存しても、登録済みキーは更新されません。 管理者がホストキーを更新するまで、接続が失敗し続ける可能性があります。

## 保存とテスト {#save-and-test}

**[!UICONTROL Save & Test]**&#x200B;は&#x200B;**初期SSH ホストキー登録のみを実行します**。 設計は保守的であり、接続に既に登録されているキーを回転または上書きすることはありません。

| 登録済みホストキーの状態 | Save &amp; Testの機能 |
| --- | --- |
| ホストキーはまだ登録されていません | **[!UICONTROL Save & Test]**&#x200B;はbastion ホストとポートをスキャンし、ホスト キーを登録し、この接続のために保存します。 |
| ホストキーは既に登録されています | **[!UICONTROL Save & Test]**&#x200B;さんが登録をスキップします。 ライブ踏み台キーが一致しなくなった場合でも、既存の登録済みキーを上書きしたり、回転したり、削除したりしません。 |
| 登録されたキーが見つからないか、空であるか、無効です | **[!UICONTROL Save & Test]**&#x200B;は、無効な信頼材料を単独で修復しません。 管理者は&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;を実行するか、エラーが継続する場合はサポートにお問い合わせください |

最初の登録が成功した後、後で&#x200B;**[!UICONTROL Save & Test]**&#x200B;は資格情報と接続設定の検証を実行しますが、登録済みSSH ホストキーは変更されません。

## SSH ホストキーの更新 {#refresh-ssh-host-keys}

**[!UICONTROL Refresh SSH Host Keys]**&#x200B;は、バスティオンが変更された場合、または信頼材料を修復する必要がある場合に、登録済みSSH ホストキーを更新します。 管理者は、**[!UICONTROL Data]** > **[!UICONTROL Connections]**&#x200B;の接続から更新を開始します。

更新は、アカウントに割り当てられたAdobe インフラストラクチャで非同期的に実行されます。 [!DNL Commerce Intelligence]は、更新がキューに入れられた後に返されます。 ワークステーションでスキャンを実行しません。

次のいずれかの条件に該当する場合にのみ、更新&#x200B;**書き換え**&#x200B;が登録したホストキーのみを更新します。

* 登録済みホストキーがありません
* 登録済みホストキーが空です
* 登録されたホストキーを読み取れません
* 登録済みホストキーが検証に失敗する
* 新しいスキャンは、登録されたキーとは異なるホストキー行を返します
* スキャンと登録キーの指紋が一致しません

登録されたキーが最新で有効な場合、更新は変更されずに完了します。

>[!TIP]
>
>チームがバスティオンでSSH ホスト キーをローテーションした後、バスティオンのホスト名またはIPを変更するか、SSH エンドポイントを置き換えた後に&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;を実行します。 数分待ってから、**[!UICONTROL Save & Test]**&#x200B;を実行して接続を確認します。

## アカウントの移行 {#migration}

アカウントの移行はトリガーにしないでください。 Adobeは、メンテナンスまたはスケーリング中にデータサーバーの移動を実行し、登録されたSSH ホストキーをコピーするので、移動後も厳密な検証が引き続き機能します。

移行が完了したことをAdobeが通知すると、次の操作が行われます。

1. **[!UICONTROL Save & Test]**&#x200B;を実行して接続を確認します。 キーが正常にコピーされた場合、登録をスキップする必要があります。
1. SSH ホストのキーエラーが引き続き発生する場合は、管理者に&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;の実行を依頼し、数分待ってから、もう一度&#x200B;**[!UICONTROL Save & Test]**&#x200B;を実行します。
1. エラーが&#x200B;**[!UICONTROL Save & Test]**&#x200B;回以上発生し、最大2回の&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;回まで発生する場合は、Adobe サポートにお問い合わせください。

## SSH ホストキーエラーメッセージ {#ssh-host-key-errors}

接続ステータスは、単一のユーザーフレンドリーなSSH ホストキーメッセージを示します。 生のOpenSSH エラーはダッシュボードに表示されません。

次の表は、一般的なメッセージを、可能性のある原因と一般的な次のステップにマッピングしたものです。

| メッセージまたはステータス | テクノロジーの意味 | 考えられる原因 | 典型的な次のステップ |
| --- | --- | --- | --- |
| SSH ホスト キーの検証に失敗しました | Bastion ホスト キーが登録済みキーと一致しないか、信頼材料が使用できません | SSH ホストキーがバスティオンで回転しました。バスティオンのホスト名、IP、またはポートが変更されました。登録済みキーが見つからないか、空であるか、無効であるか、または読み取れません | **リモートアドレス**&#x200B;および&#x200B;**SSH ポート**&#x200B;を確認してください。 インフラストラクチャのチームに、バスティオンのホストキーが変更されたかどうかを尋ねます。 管理者に&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;の実行を依頼し、数分待ってから&#x200B;**[!UICONTROL Save & Test]**&#x200B;を実行します。 |
| SSH ホストキーを登録できませんでした | **[!UICONTROL Save & Test]**&#x200B;は、バスティオンのホスト キーをスキャンまたは保存できませんでした | Adobe インフラストラクチャからBastionにアクセスできません。DNS エラー、ファイアウォール ブロック [!DNL Commerce Intelligence] IP アドレス、間違った&#x200B;**リモート アドレス**&#x200B;または&#x200B;**SSH ポート**、Bastionのホスト キーのスキャン エラー | データベース資格情報ページの[!DNL Commerce Intelligence] IP アドレスを使用して、ファイアウォールの許可リストに加えるを確認します。 設定されたポートでSSHを受け入れることをバスティオンが確認します。 接続フィールドを修正して、**[!UICONTROL Save & Test]**&#x200B;を再実行してください。 |
| SSH ホストキーがないか、無効です | 登録された信頼情報が存在しないか破損しているため、厳密な検証でトンネルがブロックされました | 最初の接続で登録が完了しませんでした。前の更新に失敗しました。移行でキーがコピーされませんでした。Adobe インフラストラクチャで問題が発生しました | 管理者に&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;を実行してから&#x200B;**[!UICONTROL Save & Test]**&#x200B;を実行するように依頼します。 エラーが解決しない場合は、サポートにお問い合わせください。 |
| SSH ホストキーを更新できませんでした | 更新で登録キーが更新されませんでした | 更新中のネットワーク、DNS、またはスキャンの失敗。Adobe インフラストラクチャの問題 | 数分待ってください。 管理者に&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;を再度実行するように依頼します（最初の試行が失敗した場合は2回目の試行）。 踏み込みの到達可能性と許可リストに加える性を確認する。 2回の更新試行と&#x200B;**[!UICONTROL Save & Test]**&#x200B;後も接続が失敗する場合は、サポートにお問い合わせください。 |

## チェックリストのトラブルシューティング {#troubleshooting}

1. **リモートアドレス**、**SSH ポート**、およびLinux ユーザー設定がバスティオン設定と一致することを確認します。
1. ファイアウォールで、データベース資格情報ページに表示される[!DNL Commerce Intelligence] IP アドレスが許可されていることを確認します。
1. インフラストラクチャのチームに、バスティオンのSSH ホストキーが最近変更されたかどうかを尋ねます。
1. **[!UICONTROL Save & Test]**&#x200B;を実行して設定を検証し、まだ存在しない場合はキーを登録します。
1. 管理者に&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;の実行を依頼し、数分待ってから、もう一度&#x200B;**[!UICONTROL Save & Test]**&#x200B;を実行します。 最初の更新でエラーが解決しない場合は、この手順を繰り返します。
1. 2回の更新試行を行っても接続にSSH ホストキーエラーが表示される場合は、接続ページ（またはアカウントサポートチャネル）で「**[!UICONTROL Contact Support]**」をクリックします。

## Adobe サポートへの問い合わせ {#contact-support}

サポートへの問い合わせ：

* 管理者が&#x200B;**[!UICONTROL Refresh SSH Host Keys]**&#x200B;を2回実行しても&#x200B;**[!UICONTROL Save & Test]**&#x200B;が失敗した後も、SSH ホストキーエラーが継続します
* **[!UICONTROL Refresh SSH Host Keys]**&#x200B;が完了しないか、15 ～ 30分後に接続ステータスが変更されない
* エラーが発生したのは、Adobeからアカウントの移行またはデータサーバーのメンテナンスに関する通知があった直後です
* Bastionの設定とファイアウォールの許可リストに加えるが正しく、チームはホストキーを回転しておらず、接続できません
* **[!UICONTROL Refresh SSH Host Keys]**&#x200B;を実行するには管理者が必要ですが、アカウントに管理者がいません

接続名、最後の&#x200B;**[!UICONTROL Save & Test]**&#x200B;回または更新試行の概算の時間、およびバスティオン ホスト キーが最近変更されたかどうかが含まれます。 秘密鍵やパスフレーズは送信しないでください。

## 関連 {#related}

* [SSH トンネル経由でMySQLを接続する](mysql-via-ssh-tunnel.md)
* [SSH トンネルを介したMongoDBの接続](mongodb-via-ssh-tunnel.md)
* [SSH トンネル経由でPostgreSQLを接続する](postgresql.md)
* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
