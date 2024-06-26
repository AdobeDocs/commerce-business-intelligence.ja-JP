---
title: Commerce Intelligence でのレポートおよび要素の命名
description: でレポートと要素に名前を付けるためのベストプラクティスを説明します [!DNL Commerce Intelligence].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
role: Admin, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# レポートおよび要素に名前を付ける

での構築を開始する前に [!DNL Adobe Commerce Intelligence]、Adobeは成功するためにいくつかの秘密鍵を共有したいと考えています。 指標やフィルターなどの作成方法を知ることは重要ですが、必要なものが見つからない場合や、曖昧さがある場合は、すべての作業が無駄になる可能性があります。

## 命名法が重要な理由 {#why}

計算列、指標およびレポートに名前を付ける方法は、様々なユーザーがフォーム内を簡単に移動できるようにするものです [!DNL Commerce Intelligence] アカウント。 これらの機能に名前を付ける場合は、次の 3 つの点に注意してください。

* **明確さ**  – これにより、レポートの表示内容や指標の機能などを一目で把握できます。
* **整合性** - ユーザー（およびAdobeサポートチーム）が、アカウント内の要素とレポートを簡単に見つけて理解できるようにします。
* **信頼性**  – 他のデータに基づく活動を刺激し、強化するため [!DNL Commerce Intelligence] ユーザーは、データを理解して使用する方法に自信を持たせる必要があります。

実証済みの真の命名法のヒントをお読みください。

## 一般的なベストプラクティス {#general}

### 意味がある {#meaningful}

可能な限り具体的に説明します。 例えば、国の場合、配送先の国か請求先の国かが分かりますか？ これはユーザーの市区町村ですか、それとも取引の市区町村ですか？

**悪い例：**
収益

これは曖昧で、あまり分からない。

**良い例：**
売上高（基本総計+料金） ユーザーの発送国

具体的な例としては、錯乱が起こる可能性を減らします。

### 大文字と一致する {#capitalize}

[!DNL Adobe] では、適切な名詞形式の大文字/小文字の使用を除き、最初の文字を大文字にし、残りの文字を小文字にすることをお勧めします。 例： **ユーザーの注文番号** むしろ **ユーザーの注文番号。**

これは本当に好みの問題ですが、覚えておくべきことは、選択したものに一貫性を持つことです。

### エンティティの一貫性 {#entity}

貴社にはすでに命名が定められているはずです。 配置した指標とディメンションは、他のデータベースやツールで使用されているものと一致するようにします。 例：

* ユーザー対顧客とメンバー対アカウント
* 会社対口座対組織
* 登録と作成

### スペル チェックと文章校正 {#spelling}

スペルを再確認し、これらの厄介な所有物を忘れないでください！

## グラフ {#charts}

の命名時 [グラフ](../tutorials/using-visual-report-builder.md)では、次の式に従うと最も役に立ちます。 **（データのパースペクティブ） + （指標） + （期間） + （時間間隔）**

**悪い例：**
収益

このレポートについて何も伝えていませんが、これは悪いです。

**良い例：**
30 日を経過した月ごとの累積収益

これで分かる **正確に** 素晴らしいレポートに何があります。

## ダッシュボード {#dashboards}

ダッシュボードには、ダッシュボード内に含まれるレポートをテーマによって表す名前を付ける必要があります。 例えば、ダッシュボードに売上高と注文に関する情報のみが含まれている場合は、次のような名前を付けることを検討します **店舗名 – 売上高と注文。**

逆に、ダッシュボードが別のレポートを試す場所である場合は、名前を付けることを検討します **名前のサンドボックス** したがって、内に含まれるレポートはドラフトです。

## Dimension（計算列） {#dimensions}

新規命名時 [寸法](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)では、次の式に従うと最も役に立ちます。 **（エンティティ）+ （N 番目）+ （時間枠）+ （計算）+ （コメント）**. 例：

ユーザーの最初の 30 日間の売上高
* ユーザーの注文番号
* ユーザーの注文番号（監査待ち）

## フィルターセット {#filterset}

[フィルターセット](../data-user/reports/ess-manage-data-filters.md) は通常、含む情報または除外する情報を説明する方法で名前が付けられます。 例えば、フィルターセットに名前を付けます **カウントする項目を注文** を使用すると、任意のユーザーがアクセスし、フィルターセットのロジックを表示し、ビジネス全体でカウントされる内容を決定する注文情報を理解できます。 フィルターセットは、計算列と指標の両方に適用でき、理解しやすいものにする必要があります。

## 指標 {#metrics}

[指標](../data-user/reports/ess-manage-data-metrics.md) は、基本的に、定期的に回答が必要な質問です。 過去 1 か月の注文件数は何件だったか。 顧客の平均生涯価値はどれくらいですか？ ユーザーに与える回答を反映するために、指標に名前を付けることをお勧めします。 また、特定の店舗または部署に対して同じ指標をフィルタリングしている場合は、そのようにラベル付けする必要があります。 例：

平均顧客 LTV （最初の 30 日間）店舗名 – 売上高

最後に、個々のユーザーの計算方法に応じて、同じ指標を異なるタイムスタンプで整理できる場合もあります。 その場合は、名前にタイムスタンプを必ず含めます。

売上高（shipped\_at）売上高（created\_at）

## まとめ {#wrapup}

スタイルおよび命名規則を早期に確立することは、 [!DNL Commerce Intelligence] アカウント。 明確さ、一貫性、信頼性という 3 つの C を覚えておいてください。
