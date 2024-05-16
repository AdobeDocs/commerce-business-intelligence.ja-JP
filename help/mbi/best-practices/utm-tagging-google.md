---
title: Google Analyticsでの UTM トラッキング
description: Google Analyticsでの UTM トラッキング（タグ付け）のベストプラクティスについて説明します。
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# UTM トラッキング

`UTM` トラッキングは、ユーザーの送信元を分析できる、URL のタグ付け規則です。 ほとんどのマーケティングメールまたはバナー広告からクリックした URL に UTM タグ付けが表示されます。 長いリンクの終わりは、次のようなものです `utm\_source` および `utm\_medium`.

[!DNL Google Analytics] 使用 `UTM` タグ付けにより、トラフィックの発信元を把握します。 この情報の一部は、 [HTTP リファラー](https://en.wikipedia.org/wiki/HTTP_referer) しかし、それ以外の部分は、自分自身を供給する必要があります `UTM` パラメーター。 次の項目が表示されます `google adwords` または `email marketing`。以下を意味します `UTM` 元のリンクから記録されたパラメーターは、クリックしてユーザーの cookie に保存されます。 そこから [!DNL Google Analytics] はそのデータを次の目的で使用します [興味深い行動を引き起こす](../data-analyst/analysis/google-track-user-acq.md) サイトで。 これらのパラメーターの目的を理解すると、UTM タグ付けの最適な設定方法と使用方法を理解するのに役立ちます。

## UTM タグ付けのベストプラクティス

で URL を設定する際に覚えておくべき 5 つの最も重要な事項を以下に示します `UTM` タグ。

### 1. サイトに到達するのを制限できるすべての URL にタグを付けることを目指します

ユーザーにリンクのクリックを求めるたびに、を設定する必要があります `UTM` タグ。 これには、すべてのメールリンク（メールサービスプロバイダーが URL を自動的にタグ付けする方法を備えている場合があります）、広告リンク、報道記事、ブログ投稿が含まれます。

### 2. ツールを使用して URL を作成する

`UTM`でタグ付けされた URL は面倒な場合があります。 長い間、入力するのではなく、ツールを使用します [いいね！](https://support.google.com/analytics/answer/1033867?hl=en) お手伝いします。 これにより、賢明なパラメーターをすべて URL に追加し、そこからコピー&amp;ペーストする URL を取得することができます。 ソーシャルリンクを管理するには、次のようなツール： [!DNL Hootsuite] すべてのリンクにカスタム URL パラメーターを追加するオプションを含めます。

### 3. パラメーター値で大文字と小文字が区別されることを確認します

タグであることを覚えておくことが重要です `utm\_source=adwords` は、とは異なるタグです。 `utm\_source=Adwords`. すべてを小文字にすることを検討してください。

### 4. UTM パラメーター値をデータベースに保存する

トランザクションまたはイベントが発生するたびに、マーケティングアクティビティのパフォーマンスを評価する必要があります。 これを行うには、UTM パラメーター値の値を [[!DNL Google Analytics] データベースへの cookie の取り込み](../data-analyst/analysis/google-track-user-acq.md).

### 5. キャンペーンの命名方法を考える

マーケティング活動が時間の経過と共にどのように改善されているかを追跡するには、命名規則に関する知識が必要です。 シンプルにし、可能な限り最小限に抑えます。 複雑な命名システムは保守が困難です。

このデータをデータベースに取り込むと、次のような高度な分析によってマーケティングと広告のパフォーマンスを評価できます。 [顧客のライフタイムバリュー](../data-analyst/analysis/ess-expected-ltv.md), [リピート購入率](../data-analyst/analysis/repurchase-behavior.md)、および [平均注文額](../data-analyst/analysis/basic-analytics.md).
