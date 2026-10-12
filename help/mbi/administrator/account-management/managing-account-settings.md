---
title: アカウント設定の管理
description: Data Warehouseのアカウント設定をカスタマイズする方法について説明します。
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b6935462-7263-4ced-a703-60de6a5aeb2d
    internal-label: Administration
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: 9e444628-408e-5d74-8cd4-c552f0d5d47f
    internal-label: Accounts
subfeature_v2:
  - id: a763c1a2-1d0a-40d7-9617-8139636fd12e
    internal-label: Access management
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%
---
# アカウント設定のカスタマイズ

>[!NOTE]
>
>[管理者権限が必要です。](../../administrator/user-management/user-management.md)

[!DNL Commerce Intelligence] アカウントでは、Data Warehouseのアカウント設定をカスタマイズできます。 これらは、任意の画面の右上隅にある組織名を選択し、ドロップダウンから「**[!UICONTROL Account Settings]**」を選択することでアクセスできます。

* **[!UICONTROL Client Name:]**&#x200B;この設定は、アカウント内のすべてのダッシュボードの右上隅および他の場所に表示されます。 **[!UICONTROL "Vandelay Industries Co., Ltd]**&#x200B;を&#x200B;**[!UICONTROL "Vandelay]**&#x200B;に変更する場合は、ここで行います。

* **[!UICONTROL Currency:]**&#x200B;これは、アカウント内のすべての金銭的価値に対する&#x200B;*デフォルト通貨*&#x200B;です。 小数点以下桁または通貨単位の値がData Warehouseに同期されるたびに、この設定によって、レポート内でその値の前に配置される記号が決まります。

* **[!UICONTROL Blackout Hours:]**&#x200B;この設定により、選択した時間内に、Data Warehouseが接続されたデータベースにアクセスできなくなります。 すべての時間は、ゼロ時間および東部標準時（EST）で表されます。 例えば、ESTの午前9時から午後1時までの間に実稼動データベースにアクセスしない場合は、**9、10、11、12**&#x200B;という数字の配列を入力する必要があります。

* **[!UICONTROL Forced update hours:]**&#x200B;この設定により、指定した時間&#x200B;*の間に、アカウント*&#x200B;でData Warehouseの更新が自動的に開始されます。 ブラックアウト時間と同様に、これらはETにも含まれています。 例えば、**午前0時**&#x200B;および&#x200B;**正午** ESTにData Warehouseの更新を自動的に開始する場合は、次の数字の配列&#x200B;**0、12**&#x200B;を入力する必要があります。

* **[!UICONTROL Send email summaries if the data has not updated yet:]**&#x200B;このオプションは、メールの概要が&#x200B;*を送信するようにスケジュールされている場合に、レポート*&#x200B;のデータが更新されるまでの状況を管理します。 **No**&#x200B;を選択した場合、アカウントはスケジュールされた時間に電子メールの送信をスキップします。 データが更新されると、代わりにアカウントから送信されます。 **[!UICONTROL Yes]**&#x200B;を選択すると、アカウントは電子メールを送信し、データが古いことを説明するメッセージを含め、データが更新されると別の電子メールを送信します。

* **[!UICONTROL Enable data updates:]**&#x200B;このオプションを使用すると、アカウントでデータ更新が実行されます。 設定を&#x200B;**[!UICONTROL No]**&#x200B;に変更すると、データの同期と列の計算がアカウントで停止します。

>[!NOTE]
>
>変更を加えた後は、必ず&#x200B;**[!UICONTROL Save Customizations]**&#x200B;を選択してください。
