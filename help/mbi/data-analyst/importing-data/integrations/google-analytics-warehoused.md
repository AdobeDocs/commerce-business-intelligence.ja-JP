---
title: 接続Google AnalyticsWarestored
description: 訪問者がサイトをどのように使用しているか、どのコンテンツが魅力的か、訪問者がどこから出て行ったかなどを追跡する方法を説明します。
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# 接続 [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] は、インターネット上で最も広く使用されている web 分析サービスです。 実装 [!DNL Google Analytics] Web サイト上では、訪問者がサイトをどのように使用しているか、どのコンテンツが魅力的か、訪問者がどこから出て行ったかなどを追跡できます。 [!DNL Google Analytics Warehoused] は、既存の [!DNL Google Analytics] 統合とも呼ばれます。 これにより、 [!DNL Google Analytics] Data Warehouse内のデータ（既存のライブフィードとは異なる） [!DNL Google Analytics] 統合とも呼ばれます。 でのこれらの指標の分析 [!DNL Commerce Intelligence]は、他のデータの断片と共に、サイトの全体的な正常性と操作性を向上させます。

## GA Warehoared とライブ統合の違い

主な差別化要因は、1 つの統合が保存されることです ([!DNL Google Analytics Warehoused])、それ以外は ([!DNL Google Analytics Live]) をクリックします。 の場合 [!DNL Google Analytics Warehoused]を使用すると、 [!DNL Google Analytics] データを取得し、 [!DNL Google Analytics] と、洞察に富んだレポートを作成するその他のデータソース。

見る [!DNL Google Analytics] 広告キャンペーンを参照してください。 4 四半期に異なる名前の広告キャンペーンを複数作成したとします。 キャンペーンは、特定のマーケティングイニシアチブの結果でした。 倉庫に格納されたデータを使用して、問題のキャンペーン名を検索し、次の第 4 四半期のイニシアチブ名を返す列を作成できます： `Operation Dumbo`.

組み合わせの側面により、 [!DNL Google Analytics] 分析を行うために他のデータに結合するデータ。 例えば、次のようにします。 `Total Time On Site By Ad Campaign` からのデータ [!DNL Google Analytics] そしてそれを仲間に入れて `Total Spent Per Campaign` からのデータ [!DNL Facebook Ads] エンゲージメントに費やされたコストの全体像を把握するために。

を使用 [!DNL Google Analytics Live] 一方で、 [!DNL Google Analytics] グラフは、Data Warehouseに保存されていない小さなサイロのようなものです。

## 接続中 [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] は `Premium` 統合。 [サポートへの問い合わせ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) この統合をサブスクリプションに追加したい場合。

1. 次に移動： `Connections` 下のページ **[!UICONTROL Admin** > **Integrations]**.
1. クリック **[!UICONTROL Add an Integration]**：右側にあります。
1. 次をクリック： [!DNL Google Analytics Warehoused] アイコン。 これにより、 [!DNL Google Analytics] 認証情報ページ。
1. を入力します。 [!DNL Google Analytics] 認証情報。 認証プロセスが完了すると、にリダイレクトされます。 [!DNL Commerce Intelligence].
1. プロファイル ID のリストが表示されます。 接続先のプロファイルを確認してください [!DNL Commerce Intelligence]. 複数のプロファイルがあり、どれがどれかを特定するのに役立つ情報が必要な場合は、複数のプロファイルの接続を参照してください。 [!DNL Google Analytics] 以下のプロファイルの節を参照してください。

## 複数の接続 [!DNL Google Analytics] プロファイル

1 つのに複数の Web サイトを接続している可能性があります [!DNL Google Analytics] 独自のアカウントで識別 [!DNL Google Analytics] プロファイル ID。 この場合、すべてのプロファイル ID を [!DNL Commerce Intelligence]. プロファイル選択手順で含めるプロファイル ID を確認します。

特定の Web サイトの [!DNL Google Analytics] プロファイル ID :

1. ログイン [!DNL Google Analytics]
1. 特定の Web サイトの [!DNL Google Analytics] dashboard
1. URL を見る — プロファイル ID は次の 8 つの数字に対応します `p` 行末に

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## 切断中 [!DNL Google Analytics Warehoused] から [!DNL Commerce Intelligence] {#disconnect}

1. 次のサイトにアクセスします。 [!DNL Google Analytics] [アカウント設定](https://myaccount.google.com/intro) ページに貼り付けます。
1. の下 `Security` 「 」セクションで、「 **[!UICONTROL edit]** 次の `Authorizing` アプリケーションとサイト。
1. クリック **[!UICONTROL revoke access]** 次の [!DNL Commerce Intelligence].

## 関連ドキュメント

* [統合の再認証](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [接続中 [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Web サイトのアクティビティと顧客コンバージョン率の分析](../../analysis/web-act-cust-conversion.md)
* [を使用したユーザー獲得データの追跡 [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
