---
title: アカウント設定の管理
description: Data Warehouse用にアカウント設定をカスタマイズする方法を説明します。
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# アカウント設定のカスタマイズ

>[!NOTE]
>
>[ 管理者権限 ](../../administrator/user-management/user-management.md) が必要です。

[!DNL Commerce Intelligence] アカウントでは、Data Warehouse用にアカウント設定をカスタマイズできます。 これらのフィールドにアクセスするには、画面の右上隅にある組織名を選択し、ドロップダウンから「**[!UICONTROL Account Settings]**」を選択します。

* **[!UICONTROL Client Name:]** この設定は、アカウント全体のすべてのダッシュボードおよび他の場所の右上隅に表示されます。 **[!UICONTROL "Vandelay Industries Co., Ltd]** を **[!UICONTROL "Vandelay]** のみに変更する場合は、ここで行います。

* **[!UICONTROL Currency:]** これは、アカウント内のすべての金額の *デフォルト通貨* です。 10 進数の値または通貨の値がData Warehouseに同期されるたびに、この設定によってレポート内のその値の前に配置される記号が決まります。

* **[!UICONTROL Blackout Hours:]** この設定により、選択した時間帯は、Data Warehouseが接続されたデータベースにアクセスしなくなります。 すべての時間は 0 時間で東部標準時（EST）で表されます。 例えば、EST の午前 9 時から午後 1 時の間に実稼動データベースにアクセスし :00 い場合は :00**9、10、11、12** という数字の配列を入力する必要があります。

* **[!UICONTROL Forced update hours:]** この設定により、Data Warehouseの更新が指定したアカウント *時間* で自動的に開始されます。 ブラックアウト時と同様に、これらは ET にも含まれます。 たとえば、Data Warehouseの更新を **午前 0 時** と **正午** EST に自動的に開始するには、**0, 12** という数字の配列を入力します。

* **[!UICONTROL Send email summaries if the data has not updated yet:]** このオプションは、メールの概要の送信がスケジュールされている *いずれかのレポートのデータが更新される前* 状況を管理します。 「**いいえ** を選択した場合、アカウントはスケジュールされた時刻にメールを送信しません。 代わりに、データが更新されると、アカウントによって送信されます。 **[!UICONTROL Yes]** を選択した場合、アカウントはメールを送信し、データが古いことを説明するメッセージを含め、データが更新されると別のメールを送信します。

* **[!UICONTROL Enable data updates:]** このオプションを選択すると、データ更新がアカウント上で実行されます。 設定を **[!UICONTROL No]** に変更すると、アカウントでデータ同期と列の計算が停止します。

>[!NOTE]
>
>変更を加えた後は、必ず **[!UICONTROL Save Customizations]** を選択してください。
