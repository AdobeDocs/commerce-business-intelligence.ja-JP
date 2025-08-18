---
title: Google Analytics - データベース内のユーザーデバイスとブラウザーデータを追跡します。
description: モバイルデバイスを介して実際にログインしているユーザーの数と、そのユーザーのライフタイム値への影響について説明します。
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
role: Admin, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# [!UICONTROL Google Analytics] トラッキング

[!UICONTROL Google Analytics] を使用すると [ リファラルソース情報を保存 ](../analysis/google-track-user-acq.md) して、最も価値のあるユーザーの出所を把握できます。 このトピックでは、ユーザーが作業しているプラットフォーム（デバイス、ブラウザーなど）について説明します。 これにより、モバイルデバイスで実際にログインしているユーザーの数と、そのユーザーのライフタイム値への影響を把握できます。

## ユーザーデバイスとブラウザーデータの保存

Web サイトに対してリクエストが行われるたびに、ユーザーのブラウザーは、リクエストを行ったプラットフォームに関する情報を含む User-Agent 文字列を送信します。 User-Agent 文字列の例を次に示します。

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

詳しく見ると、文字列にユーザーのオペレーティングシステム、ブラウザー、使用しているデバイスの名前（名前がある場合）に関する情報が含まれていることがわかります。 User-Agent 文字列は、プラットフォーム間および同じプラットフォームのバージョン間で大きく異なりますが、通常、プラットフォーム名は内のどこかに存在します。 例えば、上記の#1 はChrome ブラウザーを使用したMac#2、上記は Firefox ブラウザーを使用した Windows マシン、#3 はiPhone、#4 はiPad、#5 はAndroid デバイスです。

この情報には、リクエストが行われるたびにサーバーからアクセスできます。 PHP では、User-Agent 文字列は `$_SERVER['HTTP_USER_AGENT']` に格納されます。 Ruby on Rails では、`request.env['HTTP_USER_AGENT']` に保存されます。 他の言語や環境でも、同様の方法でアクセスできます。

### このデータはいつ記録する必要がありますか？

[!DNL Adobe] では、`Platform` または `User-Agent` という新しいフィールドを `Customers` および `Orders` データベーステーブルに追加して、ユーザーの作成や注文のたびに、この情報を保存することをお勧めします。 SQL データベースを使用している場合、このフィールドは `VARCHAR(255)` にする必要があります。 

>[!NOTE]
>
>`User-Agent` の文字列は、これよりはるかに長くなることができますが、実際にはこの長さを超えることはほとんどありません。

### 役に立つセグメントを解析するにはどうすればよいですか？

`User-Agent` の文字列を解析してオペレーティングシステムやデバイスなどのコンポーネントを生成するのに役立つライブラリが多数用意されています。 詳しくは、[ua-parser プロジェクト ](https://github.com/tobie/ua-parser) を参照してください。

この新しい情報により、ユーザーがサイトにアクセスする方法をより深く理解できます。 その後、エクスペリエンスをカスタマイズしたり、特定のグループ向けのマーケティングキャンペーンを作成したりできます。

## 関連

* [E-Commerce経由  [!DNL Google Anaytics]  注文リファラルソースを追跡](../importing-data/integrations/google-ecommerce.md)
* [データベース内のユーザー紹介ソースを追跡](../analysis/google-track-user-acq.md)
* [最も価値のある獲得ソースとチャネルを見つける](../analysis/most-value-source-channel.md)
* [アカウント  [!DNL Google Adwords]  接続](../importing-data/integrations/google-adwords.md)
* [広告キャンペーンの ROI の向上](../analysis/roi-ad-camp.md)
* [ [!DNL Google Analytics] UTM アトリビューションの仕組み](../analysis/utm-attributes.md)
