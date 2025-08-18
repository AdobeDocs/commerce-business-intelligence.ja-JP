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

`UTM` トラッキングは、ユーザーの送信元を分析できる、URL のタグ付け規則です。 ほとんどのマーケティングメールまたはバナー広告からクリックした URL に UTM タグ付けが表示されます。 `utm\_source` や `utm\_medium` のような物で終わるのは、それらの長いリンクです。

[!DNL Google Analytics] は `UTM` タグ付けを使用して、トラフィックの発信元を把握します。 この情報の一部は [HTTP リファラー ](https://en.wikipedia.org/wiki/HTTP_referer) から得られますが、残りの部分は `UTM` のパラメーターを自分で指定する必要があります。 `google adwords` または `email marketing` が表示される場合、元のリンククリックから記録され、ユーザーの Cookie に保存されるこれらの `UTM` パラメーターを意味します。 そこから、[!DNL Google Analytics] はそのデータを使用して、サイト上の [ 興味深い行動の属性 ](../data-analyst/analysis/google-track-user-acq.md) を決定します。 これらのパラメーターの目的を理解すると、UTM タグ付けの最適な設定方法と使用方法を理解するのに役立ちます。

## UTM タグ付けのベストプラクティス

次のリストは、`UTM` タグを使用して URL を設定する際に覚えておくべき 5 つの最も重要な事項です。

### &#x200B;1. サイトに到達するのを制限できるすべての URL にタグを付けることを目指します

リンクのクリックをユーザーに求めるたびに、`UTM` のタグ付けを設定する必要があります。 これには、すべてのメールリンク（メールサービスプロバイダーが URL を自動的にタグ付けする方法を備えている場合があります）、広告リンク、報道記事、ブログ投稿が含まれます。

### &#x200B;2. ツールを使用して URL を作成する

タグ付け `UTM`URL は面倒な場合があります。 長い間それらを入力しようとする代わりに、[ このような ](https://support.google.com/analytics/answer/1033867?hl=en) ツールを使用して支援します。 これにより、賢明なパラメーターをすべて URL に追加し、そこからコピー&amp;ペーストする URL を取得することができます。 [!DNL Hootsuite] などのツールには、ソーシャルリンクを管理するために、すべてのリンクにカスタム URL パラメーターを追加するオプションが含まれています。

### &#x200B;3. パラメーター値で大文字と小文字が区別されることを確認します

タグ `utm\_source=adwords` は `utm\_source=Adwords` とは異なるタグであることを覚えておくことが重要です。 すべてを小文字にすることを検討してください。

### &#x200B;4. UTM パラメーター値をデータベースに保存する

トランザクションまたはイベントが発生するたびに、マーケティングアクティビティのパフォーマンスを評価する必要があります。 これを行うには、UTM パラメーター値の値を [[!DNL Google Analytics] cookie からデータベース ](../data-analyst/analysis/google-track-user-acq.md) に読み取ります。

### &#x200B;5. キャンペーンの命名方法を考える

マーケティング活動が時間の経過と共にどのように改善されているかを追跡するには、命名規則に関する知識が必要です。 シンプルにし、可能な限り最小限に抑えます。 複雑な命名システムは保守が困難です。

このデータをデータベースに取り込むと、[ 顧客のライフタイム値 ](../data-analyst/analysis/ess-expected-ltv.md)、[ リピート購入率 ](../data-analyst/analysis/repurchase-behavior.md)、[ 平均注文額 ](../data-analyst/analysis/basic-analytics.md) などのより高度な分析によって、マーケティングや広告のパフォーマンスを評価できます。
