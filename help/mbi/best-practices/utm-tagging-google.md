---
title: GOOGLE ANALYTICSでのUTM トラッキング
description: Google AnalyticsでのUTM トラッキング（タグ付け）のベストプラクティスについて説明します。
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/IX5oaIr8tbUUeA3ZrIQNUMnG8ApXMBS1hcpecqFW8kg
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: beb7a3c1-66ab-4786-b879-7621375b3c40
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 450
ht-degree: 0%

---

# UTM トラッキング

`UTM` トラッキングは、ユーザーがどこから来たのかを分析できるURLのタグ付け規則です。 ほとんどのマーケティングメールまたはバナー広告からクリックしたURLを見ると、UTM タグが表示されます。 `utm\_source`や`utm\_medium`などで終わる長いリンクです。

[!DNL Google Analytics]では、`UTM`のタグ付けを使用して、トラフィックの送信元を把握しています。 この情報の一部は[HTTP リファラー](https://en.wikipedia.org/wiki/HTTP_referer)から取得されますが、残りの部分は`UTM`個のパラメーターを入力する必要があります。 `google adwords`または`email marketing`が表示された場合、元のリンクから記録された`UTM` パラメーターがクリックされ、ユーザーのCookieに保存されることを意味します。 そこから、[!DNL Google Analytics]はそのデータを使用して、サイトで[興味深い行動](../data-analyst/analysis/google-track-user-acq.md)を特定します。 これらのパラメーターの目的を理解すると、UTM タグを設定して使用する最適な方法を理解できます。

## UTM タグ付けのベストプラクティス

次に、`UTM` タグ付きでURLを設定する際に覚えておくべき5つの最も重要な点を示します。

### &#x200B;1. サイトへのアクセスを制御できるURLをすべてタグ付けすること

リンクをクリックするようにユーザーに依頼するたびに、`UTM` タグ付けを設定する必要があります。 これには、すべてのメールリンク（メールサービスプロバイダーがURLを自動的にタグ付けする方法を持っている可能性があります）、広告リンク、プレス記事、ブログ記事が含まれます。

### &#x200B;2. ツールを使用したURLの作成

タグ付けされた`UTM`個のURLは面倒になる可能性があります。 長く入力する代わりに、[のような](https://support.google.com/analytics/answer/1033867?hl=en) ツールを使ってください。 これにより、URLに適切なパラメーターを追加し、URLを取得してコピー&amp;ペーストできます。 ソーシャルリンクを管理するには、[!DNL Hootsuite]などのツールに、すべてのリンクにカスタム URL パラメーターを追加するオプションが含まれています。

### &#x200B;3. パラメーター値で大文字と小文字を区別するようにしてください

タグ `utm\_source=adwords`が`utm\_source=Adwords`とは異なるタグであることを覚えておくことが重要です。 すべてを小文字にすることを検討してください。

### &#x200B;4. UTM パラメータ値をデータベースに格納する

トランザクションやイベントが発生するたびに、マーケティング活動のパフォーマンスを評価します。 これは、[[!DNL Google Analytics] cookieからUTM パラメーター値をデータベース &#x200B;](../data-analyst/analysis/google-track-user-acq.md)に読み込むことで実現できます。

### &#x200B;5. キャンペーンの名前を考える

マーケティング活動が時間の経過とともにどのように改善しているかを追跡するには、命名規則について賢明である必要があります。 できるだけシンプルにして、最小限に抑えましょう。 複雑な命名システムは、維持が困難です。

このデータをデータベースに取り込むと、[顧客生涯価値](../data-analyst/analysis/ess-expected-ltv.md)、[再購入率](../data-analyst/analysis/repurchase-behavior.md)、[平均注文額](../data-analyst/analysis/basic-analytics.md)など、より高度な分析によって、マーケティングと広告のパフォーマンスを評価できます。
