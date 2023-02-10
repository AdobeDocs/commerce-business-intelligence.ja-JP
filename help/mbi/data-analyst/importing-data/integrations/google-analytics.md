---
title: 接続Google Analytics
description: Google Analyticsの接続方法 [!DNL MBI].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 0%

---

# 接続 [!DNL Google Analytics]

>[!NOTE]
>
>必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] は、インターネット上で最も広く使用されている web 分析サービスです。 実装 [!DNL Google Analytics] Web サイト上では、訪問者がサイトをどのように使用しているか、どのコンテンツが魅力的か、訪問者がどこから出て行ったかなどを追跡できます。 でのこれらの指標の分析 [!DNL MBI]は、他のデータと共に、サイトの全体的な正常性と操作性を向上させます。

まず、 [!DNL Google Analytics] ～への認証情報 [!DNL MBI]:

1. 次に移動： **[!UICONTROL Manage Data** > **Integrations]** ページ。
1. クリック **[!UICONTROL Add Integration]**：画面の右側にあります。
1. 次をクリック： [!DNL Google Analytics] アイコン これにより、 [!DNL Google Analytics] 認証情報ページ。
1. を入力します。 [!DNL Google Analytics] 資格情報。 認証プロセスの完了時に、次のページにリダイレクトされます： [!DNL MBI].
1. プロファイル ID のリストが表示されます。 接続先のプロファイルを確認してください [!DNL MBI]. 複数のプロファイルがあり、どれがどれかを特定するのに役立つ情報が必要な場合は、複数のプロファイルの接続を参照してください。 [!DNL Google Analytics] 以下のプロファイルの節を参照してください。

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. 変更は自動的に保存されるので、「 **接続に戻る** 完了したら

## 複数の接続 [!DNL Google Analytics] プロファイル

1 つのに複数の Web サイトを接続している場合があります [!DNL Google Analytics] 独自のアカウントで識別 [!DNL Google Analytics] プロファイル ID。 この場合、すべてのプロファイル ID を [!DNL MBI]. プロファイル選択手順で含めるプロファイル ID を確認します。

特定の Web サイトの [!DNL Google Analytics] プロファイル ID :

1. ログイン [!DNL Google Analytics]
1. 特定の Web サイトの [!DNL Google Analytics] dashboard
1. URL を見る — プロファイル ID は次の 8 つの数に対応します `p` 行末：

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 切断中 [!DNL Google Analytics] から [!DNL MBI] {#disconnect}

1. 次のサイトにアクセス： [!DNL Google Analytics] [アカウント設定](https://www.google.com/accounts/) ページ。
1. 以下 `Security` セクションで、 **[!UICONTROL edit]** 次の `Authorizing` アプリケーションとサイト。
1. クリック **[!UICONTROL revoke access]** 次の [!DNL MBI].

## 関連：

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [接続中 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Web サイトのアクティビティと顧客コンバージョン率の分析](../../analysis/web-act-cust-conversion.md)
* [を使用したユーザー獲得データの追跡 [!DNL Google Analytics] cookie](../../analysis/google-track-user-acq.md)
