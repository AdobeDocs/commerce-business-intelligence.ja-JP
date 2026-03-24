---
title: Google Analytics - データベース内のユーザーデバイスとブラウザーデータを追跡します
description: 実際にモバイルデバイスを介してログインしているユーザーの数と、それがユーザーの生涯価値にどのように影響するかをご覧ください。
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
role: Admin, User
feature: Reports, Dashboards
TQID: https://experienceleague.adobe.com/-j-LqjbuqLjdmDWNGxAERaDJNMapTMn7uDar1HsshSc
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 432
ht-degree: 0%

---

# [!UICONTROL Google Analytics]件のトラッキング

[!UICONTROL Google Analytics]を使用すると、[紹介ソース情報を保存](../analysis/google-track-user-acq.md)して、最も価値のあるユーザーがどこから来ているのかを把握できます。 このトピックでは、ユーザーが使用しているプラットフォーム（デバイスやブラウザーなど）について説明します。 これにより、モバイルデバイスを介して実際にログインしているユーザーの数と、それがユーザーの生涯価値にどのように影響するのかを把握できます。

## ユーザーデバイスとブラウザーデータの保存

web サイトにリクエストが送信されるたびに、ユーザーのブラウザーは、リクエストを行うプラットフォームに関する情報を含むUser-Agent文字列を送信します。 User-Agent文字列の例を次に示します。

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

よく見ると、文字列には、ユーザーのオペレーティングシステム、ブラウザー、使用しているデバイスの名前（名前がある場合）に関する情報が含まれています。 User-Agentの文字列は、プラットフォームや同じプラットフォームのバージョンによって大きく異なりますが、プラットフォーム名が同じプラットフォーム内のどこかに存在することは一般的に真実です。 例えば、上#1はChromeを搭載したMac、上#2はFirefoxを搭載したWindows マシン、#3はiPhone、#4はiPad、#5はAndroidデバイスです。

この情報は、リクエストが行われるたびにサーバーからアクセスできます。 PHPでは、User-Agent文字列は`$_SERVER['HTTP_USER_AGENT']`に格納されます。 Ruby on Railsでは、`request.env['HTTP_USER_AGENT']`に格納されています。 他の言語や環境では、同様の方法でアクセスできます。

### このデータをいつ記録すべきか。

[!DNL Adobe]では、ユーザーが作成されるか注文が行われるたびに、この情報を保存するために、`Platform`および`User-Agent`のデータベーステーブルに`Customers`または`Orders`という新しいフィールドを追加することをお勧めします。 SQL データベースを使用している場合、このフィールドは`VARCHAR(255)`である必要があります。 

>[!NOTE]
>
>`User-Agent`文字列はこれよりはるかに長くすることが許可されていますが、実際にはこの長さを超えることはほとんどありません。

### 有益なセグメントを解析するにはどうすればよいですか？

`User-Agent`文字列を解析して、オペレーティングシステムやデバイスなどのコンポーネントにするのに役立つライブラリがいくつかあります。 詳しくは、[ua-parser プロジェクト &#x200B;](https://github.com/tobie/ua-parser)を参照してください。

この新しい情報を使用すると、ユーザーがサイトにアクセスする方法をより深く理解できます。 その後、エクスペリエンスを調整したり、特定のグループに合わせたマーケティング施策を構築したりできます。

## 関連

* [&#x200B; [!DNL Google Anaytics] E-Commerce経由で注文の紹介ソースを追跡](../importing-data/integrations/google-ecommerce.md)
* [データベース内のユーザー紹介ソースの追跡](../analysis/google-track-user-acq.md)
* [最も価値のある獲得ソースとチャネルの発見](../analysis/most-value-source-channel.md)
* [&#x200B; [!DNL Google Adwords]  アカウントを接続](../importing-data/integrations/google-adwords.md)
* [広告キャンペーンのROIを高める](../analysis/roi-ad-camp.md)
* [&#x200B; [!DNL Google Analytics] UTM アトリビューションの仕組み](../analysis/utm-attributes.md)
