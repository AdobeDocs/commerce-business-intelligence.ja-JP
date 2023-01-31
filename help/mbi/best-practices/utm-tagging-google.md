---
title: Google Analyticsでの UTM トラッキング
description: Google Analyticsでの UTM トラッキング（タグ付け）のベストプラクティスについて説明します。
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# UTM トラッキング

`UTM` トラッキングは、ユーザーの来訪元を分析できる URL のタグ付け規則です。 ほとんどのマーケティング用電子メールまたはバナー広告からクリックした URL を見ると、UTM タグが表示されます。 その長いリンクは、次のようなもので終わる `utm\_source` および `utm\_medium`.

[!DNL Google Analytics] uses `UTM` タグを使用して、トラフィックの送信元を確認します。 この情報の一部は、 [HTTP リファラー](https://en.wikipedia.org/wiki/HTTP_referer) しかし残りの部分は自分で提供しなければなりません `UTM` パラメーター。 見た時 `google adwords` または `email marketing` これが意味する `UTM` 元のリンクから記録されるパラメーターをクリックして、ユーザーの cookie に保存します。 そこから [!DNL Google Analytics] はそのデータを使用して [興味のある行動を引き起こす](../data-analyst/analysis/google-track-user-acq.md) を選択します。 これらのパラメーターの内容を理解すると、UTM タグの設定と使用の最善の方法を理解できます。

## UTM タグ付けのベストプラクティス

以下に、で URL を設定する際に最も重要な 5 つの事項を示します。 `UTM` タグ付け。

### 1.サイトへの訪問を制御できるすべての URL にタグ付けすることを目的とする

担当者にリンクをクリックするように求めるたびに、次の設定を行う必要があります： `UTM` タグ付け。 これには、すべての電子メールリンク（電子メールサービスプロバイダーが URL を自動的にタグ付けする方法を持つ可能性が高い）、広告リンク、プレス記事、ブログ投稿が含まれます。

### 2.ツールを使用して URL を作成する

`UTM`タグ付き URL は非常に面倒な場合があります。 長く入力する代わりに、ツールを使用してください [この](https://support.google.com/analytics/answer/1033867?hl=en) 助けになります。 これにより、URL にすべての賢明なパラメーターを追加することで考慮を深め、その URL からコピー&amp;ペーストする URL を取得できます。 ソーシャルリンクを管理するには、 [!DNL Hootsuite] すべてのリンクにカスタム URL パラメーターを追加するオプションを含めます。

### 3.パラメーターの値で、大文字と小文字が区別されることを確認してください

このタグを覚えておくことが重要です。 `utm\_source=adwords` は次とは異なるタグです： `utm\_source=Adwords`. すべてを小文字にすることを検討します。

### 4. UTM パラメーターの値をデータベースに格納します

トランザクションまたはイベントが発生するたびに、マーケティングアクティビティのパフォーマンスを評価する必要があります。 これを行うには、UTM パラメーターの値を [[!DNL Google Analytics] cookie をデータベースに追加](../data-analyst/analysis/google-track-user-acq.md).

### 5.キャンペーンに名前を付ける方法を考えてみましょう

マーケティング活動が時間の経過と共にどのように改善されているかを追跡するには、命名規則に関する知識が必要です。 シンプルにし、できるだけ最小限に抑えます。 複雑な命名システムは維持が困難です。

このデータをデータベースに取り込むと、以下を含むより高度な分析によって、マーケティングや広告のパフォーマンスを評価できます。 [顧客のライフタイム値](../data-analyst/analysis/ess-expected-ltv.md), [再購入率](../data-analyst/analysis/repurchase-behavior.md)、および [平均注文額](../data-analyst/analysis/basic-analytics.md).
