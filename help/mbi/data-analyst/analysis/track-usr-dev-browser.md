---
title: Google Analytics — データベース内のユーザーデバイスとブラウザーデータを追跡します。
description: モバイルデバイスを介して実際にログインしているユーザーの数と、それがユーザーのライフタイム値に与える影響について説明します。
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
role: Admin, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# [!UICONTROL Google Analytics] トラッキング

を使用 [!UICONTROL Google Analytics] 以下が可能です。 [リファラルソース情報を保存する](../analysis/google-track-user-acq.md) 最も価値の高いユーザーがどこから来たのかを把握するために このトピックでは、ユーザーが作業しているプラットフォーム（デバイスやブラウザーなど）について説明します。 これにより、モバイルデバイスを介して実際にログインしているユーザーの数と、それがユーザーのライフタイム値に与える影響を把握できます。

## ユーザーデバイスとブラウザーデータの保存

Web サイトでリクエストがおこなわれるたびに、ユーザーのブラウザーは、リクエストをおこなうプラットフォームに関する情報を含む User-Agent 文字列を送信します。 User-Agent 文字列の例を次に示します。

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

よく見ると、文字列にユーザーのオペレーティングシステム、ブラウザー、および使用しているデバイスの名前（名前がある場合）に関する情報が含まれていることがわかります。 User-Agent 文字列は、プラットフォームと同じプラットフォームのバージョンで大きく異なりますが、通常、プラットフォーム名が内のどこかに存在するというのは事実です。 例えば、上記の#1は Chrome ブラウザーを搭載したMac、上記の#2は Firefox ブラウザーを搭載した Windows マシン、#3はiPhone、#4はiPad、#5は Android デバイスです。

この情報は、リクエストがおこなわれるたびに、サーバーからアクセスできます。 PHP では、User-Agent 文字列は `$_SERVER['HTTP_USER_AGENT']`. Ruby on Rails では、に格納されます。 `request.env['HTTP_USER_AGENT']`. 他の言語や環境も同様の方法でアクセスできます。

### このデータはいつ記録する必要がありますか？

[!DNL Adobe] では、 `Platform` または `User-Agent` を `Customers` および `Orders` ユーザーが作成されたり、注文がおこなわれたりするたびに、この情報を保存するデータベーステーブル。 SQL データベースを使用している場合、このフィールドは `VARCHAR(255)`. 

>[!NOTE]
>
>The `User-Agent` 文字列の長さはこれよりも大幅に長くすることができますが、実際にはこの長さを超えることはほとんどありません。

### 有用なセグメントを解析する方法を教えてください。

ここには、 `User-Agent` 文字列をオペレーティングシステム、デバイスなどのコンポーネントに組み込みます。 詳しくは、 [ua-parser プロジェクト](https://github.com/tobie/ua-parser) を参照してください。

この新しい情報を使用して、ユーザーがサイトにアクセスする方法をより深く理解できます。 その後、エクスペリエンスを調整したり、特定のグループ向けにマーケティングキャンペーンを作成したりできます。

## 関連

* [経由で注文のリファラルソースを追跡する [!DNL Google Anaytics] E コマース](../importing-data/integrations/google-ecommerce.md)
* [データベース内のユーザーのリファラルソースを追跡する](../analysis/google-track-user-acq.md)
* [最も価値のある獲得ソースとチャネルを見つける](../analysis/most-value-source-channel.md)
* [接続する [!DNL Google Adwords] アカウント](../importing-data/integrations/google-adwords.md)
* [広告キャンペーンの ROI の向上](../analysis/roi-ad-camp.md)
* [方法 [!DNL Google Analytics] UTM 属性は機能しますか？](../analysis/utm-attributes.md)
