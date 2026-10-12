---
title: Google ECommerceに接続
description: Adobe Googleのe コマースデータをCommerce Intelligenceに接続することで、最も価値のある紹介チャネルを追跡し、他のデータソースとともに売上を分析できます。
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: 'https://experienceleague.adobe.com/iBVf-dkbm1NbELZUYjLp1TzypO7Cu55tIzd93lQ1zo0'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: 4d217dbe-2c9a-5839-94d7-471fd31623b7
    internal-label: Data Integration
  - id: 601e4abe-d9bf-58de-a779-32ed6794dcbe
    internal-label: Data Import/Export
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%
---
# [!DNL Google ECommerce]を接続

>[!NOTE]
>
>[管理者権限](../../../administrator/user-management/user-management.md)が必要です。

![Google e コマース ロゴ ](../../../assets/google-ecommerce-logo.png)

トラフィックと注文が常に発生しているため、顧客に効果的にリーチし、獲得することができます。 しかし、最も価値のある紹介チャネルは何でしょうか？ あるソースから取得した顧客と別のソースから取得した顧客の平均生涯価値は何ですか？ [!DNL Google ECommerce]から[!DNL Commerce Intelligence]までの注文紹介ソースデータを接続することで、[最も価値のあるマーケティングチャネル ](../../../data-analyst/analysis/most-value-source-channel.md)を特定するのに役立つ分析を作成できます。

[!DNL Google ECommerce]資格情報を[!DNL Commerce Intelligence]に入力して開始します。

1. **[!UICONTROL Admin** > **Connections]**&#x200B;の下の`Connections` ページに移動します。

1. `Data Sources` テーブルの上の画面の右側にある「**[!UICONTROL Add a New Source]**」をクリックします。

1. [!DNL Google ECommerce] アイコンをクリックします。 これにより、[!DNL Google ECommerce]資格情報ページが開きます。

1. [!DNL Google Analytics]資格情報を入力してください。 認証プロセスが完了すると、次の場所にリダイレクトされます：[!DNL Commerce Intelligence]。

1. プロファイル IDのリストが表示されます。 [!DNL Commerce Intelligence]に接続するプロファイルを確認してください。

   複数のプロファイルがあり、そのプロファイルを特定するヘルプが必要な場合は、以下の「[!DNL Google Analytics] プロファイルを複数**接続」セクションを参照してください。

   ![複数のGoogle Analytics プロファイルを接続するオプションを示すフォーム ](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. 変更は自動的に保存されるので、完了したら&#x200B;**[!UICONTROL Back to Connections]**&#x200B;をクリックします。

## 複数の[!DNL Google Analytics] プロファイルを[!DNL Commerce Intelligence]に接続しています

1つの[!DNL Google Analytics] アカウントに複数のWeb サイトを接続している可能性があります。各Web サイトは、独自の[!DNL Google Analytics] プロファイル IDで識別されます。 この場合、すべてのプロファイル IDを[!DNL Commerce Intelligence]に含めるオプションがあります。 プロファイル選択手順に含めるプロファイル IDを確認します。

特定のweb サイトの[!DNL Google Analytics] プロファイル IDを識別するには：

1. [!DNL Google Analytics]にログインします。
1. 特定のweb サイトの[!DNL Google Analytics] ダッシュボードに移動します。
1. URLを見てください – プロファイル IDは、行の末尾にある`p`に続く8つの数字に対応しています。

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## [!DNL Google ECommerce]を[!DNL Commerce Intelligence]から切断しています {#disconnect}

1. [!DNL Google Analytics] [ アカウント設定](https://www.google.com/account/about/?hl=en) ページにアクセスします。
1. `Security` セクションで、`Authorizing`個のアプリケーションとサイトの横にある&#x200B;**[!UICONTROL edit]**&#x200B;をクリックします。
1. [!DNL Commerce Intelligence]の横にある&#x200B;**[!UICONTROL revoke access]**&#x200B;をクリックします。

## 関連：

* [期待される [!DNL Google ECommerce]  データ](../integrations/google-ecommerce-data.md)
* [統合の再認証](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations)
* [ [!DNL Google ECommerce]  トラッキングを設定しています](https://support.google.com/analytics/answer/1009612?hl=en)
* [最も価値のある獲得ソースとチャネルの発見](../../analysis/most-value-source-channel.md)
* [広告キャンペーンのROIを高める](../../analysis/roi-ad-camp.md)
