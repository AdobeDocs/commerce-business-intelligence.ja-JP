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
>が必要 [管理者権限。](../../administrator/user-management/user-management.md)

あなたの [!DNL Commerce Intelligence] アカウント :Data Warehouseに合わせてアカウント設定をカスタマイズできます。 これらのフィールドにアクセスするには、画面の右上隅にある組織名を選択し、次のいずれかを選択します **[!UICONTROL Account Settings]** ドロップダウンから。

* **[!UICONTROL Client Name:]** この設定は、アカウント全体のすべてのダッシュボードおよび他の場所の右上隅に表示されます。 変更する場合 **[!UICONTROL "Vandelay Industries Co., Ltd]** ジャストへ **[!UICONTROL "Vandelay]**、ここで行います。

* **[!UICONTROL Currency:]** これはです *既定の通貨* （アカウント内のすべての金額について）。 10 進数または通貨の値がData Warehouseに同期されるたびに、この設定によってレポート内のその値の前に配置される記号が決まります。

* **[!UICONTROL Blackout Hours:]** この設定により、選択した時間帯は、接続されたデータベースにData Warehouseがアクセスできなくなります。 すべての時間は 0 時間で東部標準時（EST）で表されます。 例えば、EST の午前 9 時から午後 1 時の間に実稼動データベースにアクセスしないようにするには、次の数字の配列を入力する必要があります。 **9、10、11、12**.

* **[!UICONTROL Forced update hours:]** この設定により、Data Warehouseの更新がアカウントで自動的に開始されます *時間内* が指定されました。 ブラックアウト時と同様に、これらは ET にも含まれます。 例えば、Data Warehouseの更新を次の時間から自動的に開始するとします **真夜中** および **正午** EST には、次の数字の配列を入力する必要があります。 **0、12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** このオプションでは、電子メールの概要の送信がスケジュールされている場合の状況を管理します *いずれかのレポートのデータの前* が更新されました。 次を選択した場合： **不可**&#x200B;の場合、アカウントはスケジュールされた時刻にメールを送信しません。 代わりに、データが更新されると、アカウントによって送信されます。 次を選択した場合： **[!UICONTROL Yes]**&#x200B;を入力すると、アカウントがメールを送信し、データが古いことを説明するメッセージが含まれ、データが更新されたら別のメールを送信します。

* **[!UICONTROL Enable data updates:]** このオプションを選択すると、データ更新がアカウント上で実行されます。 設定をに変更した場合 **[!UICONTROL No]**&#x200B;の場合、データ同期と列の計算はアカウントで停止します。

>[!NOTE]
>
>必ずを選択してください。 **[!UICONTROL Save Customizations]** 変更を加えた後。
