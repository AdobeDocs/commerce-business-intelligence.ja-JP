---
title: アカウント設定の管理
description: Data Warehouse の多数のアカウント設定をカスタマイズする方法を説明します。
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# アカウント設定のカスタマイズ

>[!NOTE]
>
>必要 [管理者権限。](../../administrator/user-management/user-management.md)

を [!DNL MBI] アカウントを使用すると、Data Warehouse の様々なアカウント設定をカスタマイズできます。 これらにアクセスするには、任意の画面の右上隅で組織名を選択し、「 」を選択します。 **[!UICONTROL Account Settings]** をドロップダウンから選択します。

* **[!UICONTROL Client Name:]** この設定は、すべてのダッシュボードとアカウント全体の他の場所の右上隅に表示されます。 変更する場合 **[!UICONTROL "Vandelay Industries Co., Ltd]** ただの **[!UICONTROL "Vandelay]**&#x200B;の場合は、ここで設定を行います。

* **[!UICONTROL Currency:]** これは *デフォルト通貨* アカウント内のすべての金額の 小数値または通貨値が Data Warehouse に同期されるたびに、この設定によってレポート内でその値の前に配置される記号が決まります。

* **[!UICONTROL Blackout Hours:]** この設定により、1 日の選択した時間帯に、Data Warehouse が接続されたデータベースにアクセスしなくなります。 すべての時間は、0 時間で、東部標準時 (EST) で表されます。 例えば、実稼動データベースに米国東部標準時間の午前 9 時から米国東部標準時間の午後 1 時の間にアクセスしたくない場合は、次の数字の配列を入力する必要があります。 **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** この設定により、お使いのアカウントで Data Warehouse の更新が自動的に開始されます *時間に* 指定しました。 ブラックアウト時間と同様に、これらは ET にもあります。 例えば、Data Warehouse の更新を **真夜中** および **正午** EST では、次の桁の配列を入力する必要があります。 **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** このオプションは、E メールの概要が送信されるスケジュールが設定されている状況で、システムに対して何を実行するかを指定します *レポートのデータの前* は現在まで更新されます。 次を選択した場合： **いいえ**&#x200B;アカウントでは、スケジュールされた時刻に E メールの送信をスキップし、データが更新されると送信します。 次を選択した場合： **[!UICONTROL Yes]**&#x200B;に設定すると、アカウントが E メールを送信し、データが古いことを説明するメッセージを含め、データが更新されると別の E メールを送信します。

* **[!UICONTROL Enable data updates:]** このオプションを使用すると、アカウントでデータの更新が確実に実行されます。 設定を **[!UICONTROL No]**&#x200B;の場合、データ同期と列の計算は完全に停止します。

>[!NOTE]
>
>必ず **[!UICONTROL Save Customizations]** 変更を加えた後。
