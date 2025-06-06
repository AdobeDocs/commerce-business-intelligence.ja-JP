---
title: クーポンの影響の分析
description: 顧客の獲得と維持に対するクーポンの影響を分析する方法を説明します。
exl-id: b0619365-fa75-49b5-a393-87f3364a390f
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 1%

---

# クーポンの影響

顧客によるクーポンの利用方法を分析すると、ビジネスに関する重要なインサイトを得ることができます。 具体的には、クーポンを使用して顧客を取得および保持する方法を分析します。 このトピックでは、次のタイプの質問に答えるのに役立つ分析について説明します。

* クーポンで取得している顧客の数
* クーポンを取得した顧客は、クーポンを取得していない顧客よりもリピート購入する可能性が高いですか？
* クーポンを取得した顧客と、クーポンを取得していない顧客では、平均生涯売上高はどのように異なりますか？
* クーポンから獲得した顧客は、クーポンを使用して繰り返し購入していますか？

これらの質問に対しては、[ クーポン取得顧客と非クーポン取得顧客の比較 ](#compare)、[ クーポン取得からの初回注文詳細の分析 ](#firstorder)、および [ クーポンを初回注文で使用する顧客の属性の調査 ](#attributes) に焦点を当てて回答してください。

始めましょう。

## クーポン取得顧客と非クーポン取得顧客の比較 {#compare}

クーポンの取得と保持を調べる分析を作成する場合は、次の指標の使用を検討します。

### 新規顧客の数

この指標は、クーポンで取得された顧客の数と、クーポンで取得されなかった顧客の数の推移を示します。 これにより、クーポンを使用して顧客の獲得率を判断できます。

### 平均生涯売上高

この指標は、クーポンおよびクーポン以外で取得した顧客からの平均ライフタイム収益を示します。 これは、顧客のライフタイム値が購入タイプによって異なるかどうかを判断するのに役立ちます。

### リピート注文数

この指標は、両方のタイプの顧客獲得によって行われたリピート注文数を示します。 これは、クーポン取得済み顧客とクーポン取得済み以外の顧客のどちらにフォローアップオーダーが行われるかを判断するのに役立ちます。

### クーポン付きリピート注文の数と割合

これにより、クーポンが適用されたリピート注文の数と、クーポンが適用されたリピート注文の割合が表示されます。 これにより、クーポンを取得した顧客がクーポンを使用してリピート注文を行う傾向が、クーポンを取得していない顧客よりも高いかどうか、また、クーポンを取得した顧客がフォローアップ注文でクーポンを不釣り合いに使用しているかどうかを判断できます。

クーポン取得指標と非クーポン取得指標のサンプルデータを見てみましょう。

| **顧客獲得** | **新規顧客の数** | **平均生涯売上高** | **リピート注文数** | **クーポン付きのリピート注文数** | リピート注文の **% （クーポン付き）** |
|-----|-----|-----|-----|-----|-----|
| クーポン | 1,206 | 356.91 ドル | 2,570 | 1,248 | 48.56% |
| 非クーポン | 11,561 | 498.30 ドル | 20,145 | 3,251 | 16.14% |

{style="table-layout:auto"}

この機能から何を引き出すことができるかをご覧ください。

### 新規顧客の数

上記の例では、クーポン以外の取得の数が、クーポンの取得よりはるかに多くなっています。 ただし、クーポンで取得したお客様の数はまだ 1,206 人で、それ以外はお客様にならなかった可能性があります。

### 平均生涯売上高

この例では、クーポン以外の取得の平均生涯売上高は、クーポン取得の平均生涯売上高よりも高くなります。 つまり、クーポン以外の購入では、リピート購入や高価値購入が増えていることを意味します。

### リピート注文数

非クーポン取得のリピート注文数は、クーポン取得よりはるかに多くなっています。 クーポン以外の獲得顧客が多数あるため、この傾向が予測されます。

### クーポン付きのリピート注文数

同様に、クーポンを使用して行われた繰り返し注文の数は、非クーポン取得の場合より多くなります。

## クーポン付きリピート注文の割合

非クーポン取得顧客は、クーポン取得顧客よりもクーポンが適用されたリピート注文の割合がはるかに低くなります。 したがって、クーポンを取得した顧客の場合、リピート注文のほぼ半分にクーポンが適用されています。 この例では、クーポンを取得した顧客は、クーポンで繰り返し購入する傾向があります。

## クーポン取得からの最初の注文の詳細の分析 {#firstorder}

この節では、クーポンでセグメント化された、クーポン獲得からの **最初の注文にのみ焦点を当てています。** 分析でこれらの指標を使用する：

### 注文/顧客の数

この指標は、各クーポンの初回注文数、または初回注文でそのクーポンを使用した顧客の数を示します。 これは、特定のクーポンが他のクーポンよりも初回購入を推奨しているかどうかを判断するのに役立ちます。

### 総収益

この指標は、顧客の初回注文で使用された特定のクーポンから得られた売上高を示します。 この売上高は、割引が適用される前に販売された品目の計算です。

### クーポンからの割引

この指標は、クーポンから適用された合計割引額を示します。

### 純売上高

この指標は、顧客の初回注文で使用された特定のクーポンから得られた売上高を示します。 この売上高は、すべての割引が適用された後に販売された項目の計算です。 クーポンがないと純売上高が発生しない可能性があることに注意することが重要です。

### 平均注文値

この指標は、特定のクーポンの平均注文額を表示します。

### 注文の平均ライフタイム数

この指標は、特定のクーポンを使用する顧客が生成したロイヤルティと平均注文数を評価するのに役立ちます。

### 平均生涯売上高

この指標は、特定のクーポンを使用する顧客が生成したロイヤルティと平均売上高を評価するのに役立ちます。 クーポンを使用するお客様が他のお客様よりも高い価値があるかどうかを評価する場合は、有意なサンプルサイズを確保するために、各クーポンが使用された注文数を考慮してください。

次に、顧客の初回注文に使用される 3 つの異なるクーポンが含まれる例を見てみましょう。

| **クーポン** | **初回注文（FTO）** | **FTO からの総収入金額** | **FTO に適用される割引** | **FTO の純収益** | **FTO の平均注文額** |
|-----|-----|-----|-----|-----|-----|
| **100 ドル以上は 25% 割引** | 56 | $8,531.04 | $2,132.76 | $6,398.28 | 152.34 ドル |
| **10 ドル割引** | 87 | $3,707.07 | 426.100 ドル | $3,280.97 | 42.61 ドル |
| **20% オフ** | 145 | $10,975.05 | 2,195.01 ドル | $8,780.04 | 75.69 ドル |

{style="table-layout:auto"}

これからは何が取れますか？ まず、「20% オフ」クーポンは、最初の注文の数が最も多かった。 ただし、各クーポンに関連付けられている注文数は、次のようないくつかの要因によって異なる可能性があります。

* 各クーポンの広告金額。
* クーポンが提供された時間の長さ。
* クーポンが提供された日/週/月/年の時間。
* ビジネスによってクーポンが提供されたシーズン。

  **例：** 夏期に「20% オフ」のクーポンをオファーしたが、ビジネスは冬物服を販売している。
* クーポンに関する制限。

  **例：** 「10% オフ」クーポンは、冬物のコートを同じ順序で購入したお客様にのみ提供されます。

**100 ドル以上に対して 25% 割引」クーポンの「総収益** は、「$10 割引」クーポンの総収益よりはるかに高い。 ただし、「$10 オフ」クーポンにははるかに大きい **注文数** があります。 **平均注文額** を分析すると、これらの違いに関するインサイトを得ることができます。 「100 ドル以上 25% オフ」クーポンは注文数が少ないにもかかわらず、平均注文額は「10 ドルオフ」クーポンの 3 倍以上です。 したがって、総売上高が大きいのは、「100 ドル以上の 25% オフ」クーポンに起因します。

「100 ドル以上で 25% オフ **と** 20% オフ **クーポンの** 割引」と「純売上高」は、ほぼ同じ価値があります。 「100 ドル以上で 25% オフ」の平均注文額は「20% オフ」の平均注文額の 2 倍に近いですが、後者のクーポンは注文数の 3 倍未満です。

## クーポンを最初の注文で使用する顧客の属性 {#attributes}

注文自体を見てみましょう。最初の注文でクーポンを使用している顧客を見てみましょう。

| **顧客の最初の注文クーポン** | **顧客数** | **注文の平均ライフタイム数** | **平均生涯売上高** |
|-----|-----|-----|-----|
| **100 ドル以上は 25% 割引** | 56 | 2.8 | 554.54 ドル |
| **10 ドル割引** | 87 | 1.9 | 115.50 ドル |
| **20% オフ** | 145 | 1.3 | 103.75 ドル |

{style="table-layout:auto"}

初回注文数は、各クーポンの顧客数と同じであることに注意してください。 各顧客が最初の注文を 1 つしか持てないので、これは理にかなっています。

最も多かったのは、「20% オフ」クーポンを通じて獲得された顧客です。 ただし、これらの顧客は **平均生涯注文数** および **平均生涯売上高** が最も少なく、通常、ほとんどのクーポン取得顧客はリピート注文を行いません。 さらに、「100 ドル以上の 25% オフ」クーポンを通じて獲得した顧客は、より高い **平均ライフタイム注文数**、次いで高い **平均ライフタイム収益** を推進しています。 一般的に、このクーポンを介して取得されたユーザーは通常戻ってきて、より多くの繰り返し購入をします。

## まとめ {#wrapup}

顧客によるクーポンの使用方法をより深く理解するために作成できる分析は多数あります。 顧客がクーポンをどのように使用するか、またはクーポンの使用にかかる時間を分析することを考えたことはありますか？ 最適な割引額を見つけることはどうですか – リピート購入者を促す金額、平均注文額の増加、生涯売上高の増加はどうなりますか？ これらのタイプの質問に関するヘルプについては、[ サポートにお問い合わせください ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)。
