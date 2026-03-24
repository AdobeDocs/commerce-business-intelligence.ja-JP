---
title: Google ECommerceに接続
description: 最も価値のある紹介チャネルの詳細。
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/iBVf-dkbm1NbELZUYjLp1TzypO7Cu55tIzd93lQ1zo0
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: d095671a-1355-40aa-8b5f-06c33c68080bid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 305
ht-degree: 0%

---

# [!DNL Google ECommerce]を接続

>[!NOTE]
>
>[管理者権限](../../../administrator/user-management/user-management.md)が必要です。

![Google e コマース ロゴ ](../../../assets/google-ecommerce-logo.png)

トラフィックと注文が常に発生しているため、顧客に効果的にリーチし、獲得することができます。 しかし、最も価値のある紹介チャネルは何でしょうか？ あるソースから取得した顧客と別のソースから取得した顧客の平均生涯価値は何ですか？ [!DNL Google ECommerce]から[!DNL Commerce Intelligence]までの注文紹介ソースデータを接続することで、[最も価値のあるマーケティングチャネル ](../../../data-analyst/analysis/most-value-source-channel.md)を特定するのに役立つ分析を作成できます。

[!DNL Google ECommerce]資格情報を[!DNL Commerce Intelligence]に入力して開始します。

1. `Connections`の下の&#x200B;**[!UICONTROL Admin** > **Connections]** ページに移動します。

1. **[!UICONTROL Add a New Source]** テーブルの上の画面の右側にある「`Data Sources`」をクリックします。

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
1. `Security` セクションで、**[!UICONTROL edit]**&#x200B;個のアプリケーションとサイトの横にある`Authorizing`をクリックします。
1. **[!UICONTROL revoke access]**&#x200B;の横にある[!DNL Commerce Intelligence]をクリックします。

## 関連：

* [期待される [!DNL Google ECommerce]  データ](../integrations/google-ecommerce-data.md)
* [統合を再認証しています](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [ セットアップ  [!DNL Google ECommerce]  トラッキング ](https://support.google.com/analytics/answer/1009612?hl=en)
* [最も価値のある獲得ソースとチャネルの発見](../../analysis/most-value-source-channel.md)
* [広告キャンペーンのROIを高める](../../analysis/roi-ad-camp.md)
