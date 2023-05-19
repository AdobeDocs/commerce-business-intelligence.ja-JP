---
title: アカウント設定の管理
description: Data Warehouseのアカウント設定をカスタマイズする方法を説明します。
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 8d4e71363edad0613cc0ab277c2a43aad000965e
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# アカウント設定のカスタマイズ

>[!NOTE]
>
>必要 [管理者権限。](../../administrator/user-management/user-management.md)

を [!DNL Commerce Intelligence] アカウントを使用すると、Data Warehouseのアカウント設定をカスタマイズできます。 これらにアクセスするには、任意の画面の右上隅で組織名を選択し、「 」を選択します。 **[!UICONTROL Account Settings]** をドロップダウンから選択します。

* **[!UICONTROL Client Name:]** この設定は、すべてのダッシュボードとアカウント全体の他の場所の右上隅に表示されます。 変更する場合 **[!UICONTROL "Vandelay Industries Co., Ltd]** ただの **[!UICONTROL "Vandelay]**&#x200B;の場合は、ここで設定を行います。

* **[!UICONTROL Currency:]** これは *デフォルト通貨* アカウント内のすべての金額の 小数値または通貨値がData Warehouseに同期されるたびに、この設定によってレポート内でその値の前に配置される記号が決まります。

* **[!UICONTROL Blackout Hours:]** この設定により、1 日の選択した時間内に、Data Warehouseが接続されたデータベースにアクセスできなくなります。 すべての時間は、0 時間で、東部標準時 (EST) で表されます。 例えば、実稼動データベースに米国東部標準時間の午前 9 時から米国東部標準時間の午後 1 時の間にアクセスしたくない場合は、次の数字の配列を入力する必要があります。 **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** この設定により、アカウントでData Warehouseの更新が自動的に開始されます *時間の間* 指定しました。 ブラックアウト時間と同様に、これらは ET にもあります。 例えば、Data Warehouseの更新を **真夜中** および **正午** EST では、次の桁の配列を入力する必要があります。 **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** このオプションは、E メールの概要が送信するようにスケジュールされている状況を管理します *レポートのデータの前* が更新されました。 次を選択した場合： **いいえ**&#x200B;アカウントでは、E メールの送信がスケジュールされた時刻にスキップされます。 代わりに、データが更新されると、アカウントはこれを送信します。 次を選択した場合： **[!UICONTROL Yes]**&#x200B;を使用すると、アカウントは電子メールを送信し、データが古いことを説明するメッセージを含み、データが更新されると別の電子メールを送信します。

* **[!UICONTROL Enable data updates:]** このオプションを使用すると、アカウントでデータの更新が確実に実行されます。 設定を **[!UICONTROL No]**、データ同期と列の計算がアカウントで停止します。

>[!NOTE]
>
>必ず **[!UICONTROL Save Customizations]** 変更を加えた後。
