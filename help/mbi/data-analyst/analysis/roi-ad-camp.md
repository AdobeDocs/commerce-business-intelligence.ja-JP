---
title: 広告キャンペーンの ROI の向上
description: キャンペーンのパフォーマンスを評価する様々な方法について説明します。
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Data Warehouse Manager, Reports, Campaigns
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 0%

---

# 広告キャンペーンと ROI

[!DNL Adobe Commerce Intelligence] を使用すると、次のことが簡単にできます [広告コストデータと収益データの結合](../../data-analyst/importing-data/integrations/google-adwords.md) データベースから。 これにより、投資回収率（ROI）が最も高いキャンペーンを特定できます。 このトピックでは、キャンペーンのパフォーマンスを評価する様々な方法について説明します。

## 前提条件

* 広告コストデータを読み込みます。
   * [を接続 [!DNL Google AdWords] 対象： [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md)：これはと同期されます [!DNL Adwords] ～で過ごす [!DNL Commerce Intelligence]
   * [その他の広告コストデータのアップロード](../importing-data/connecting-data/import-offline-ad-data.md)：への直接コネクタがないチャネルの場合は、この方法をお勧めします [!DNL Commerce Intelligence]
   * 複数のソースからコストデータをインポートすると、次のことができます [統合](../../best-practices/consolidating-your-tables.md) のデータ [!DNL Commerce Intelligence]. 簡単に [サポートチケットを送信](../../guide-overview.md#Submitting-a-Support-Ticket).
* [ユーザー獲得チャネルデータの追跡](../analysis/google-track-user-acq.md)

## ユーザー獲得キャンペーン

ユーザー獲得をターゲットとしたキャンペーンは、次のような多くの観点から測定できます。

1. キャンペーンで獲得した新規ユーザー数
1. キャンペーンの登録から購入へのコンバージョン率
1. 平均ユーザー生涯値（LTV）に基づくキャンペーンの ROI

上記の分析（1）と（2）は、に関する別のチュートリアルで説明しています。 [上位のマーケティングチャネルの特定](../analysis/most-value-source-channel.md). ここでは、分析（3）を調べて、キャンペーンの ROI の推移を測定します。 これにより、特定のキャンペーンから取得したユーザーが、取得コストをカバーするのに十分な生涯収益を生み出したかどうかに回答できます。

>[!NOTE]
>
>この例では、すべてのキャンペーンコストが新しいユーザーの取得にのみ使用されたと想定しています。 実際には、キャンペーンコストは、コンバージョンされていない訪問の取得やリピート購入者とも共有されます。 新規登録ユーザーの獲得にすべてのコストを使用すると仮定すると、結果として生じる ROI は最悪のケースのシナリオ（獲得あたりの最高コスト）を占めます。 実際の ROI が計算よりも高いことを確認できます。
>
>例：10 人の新規ユーザーと 10 人のリピート購入者を生成したキャンペーンに$20 を費やしたとすると、新規ユーザーあたりの実際のコストは$1 になります。 しかし、すべてのコストが新しいユーザーを獲得するために行ったと仮定すると、獲得あたりのコストは 2 ドルです。

**1.まず、キャンペーン別に広告コストをセグメント化するグラフを作成します。**

1. を作成 [!UICONTROL Metric] それはあなたの時間の経過を合計する
1. に移動 [!UICONTROL Data > Metrics]
1. を選択 `Add New Metric` を選択し、 [!DNL `Adwords...`] を記録しているテーブル [!DNL AdWords] コストデータ。
1. 指標エディターで、指標に名前を付けます（例：） [!UICONTROL AdWord Cost]）
1. ドロップダウンを使用して、を実行します。 **合計** 日 `adCost` 列： [!DNL Adwords...] による並べ替え済みテーブル（変更） `date` 列。
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. クリック `Back to Metric List` 上部で、任意のダッシュボードに移動します。

1. キャンペーン別の支出をセグメント化するレポートの作成
1. 任意のダッシュボードで、 [!UICONTROL Add Report > Create report]
1. 「」を選択します [!UICONTROL Adword Cost] 作成したばかりの指標
1. を [!UICONTROL Time period] 対象： `All-time`、および [!UICONTROL Interval] 対象： `None`
1. の下 `Group by` タブ、追加 `campaign` as [!UICONTROL grouping field]を選択し、 `Add All` ボックス内。
1. このレポートには、すべての時間が表示されます [!DNL AdWords] キャンペーン別コスト

**2. キャンペーン別に新規ユーザーをカウントするレポートを作成します。**

1. 任意のダッシュボードで、 **[!UICONTROL Add Report > Create report]**
1. 「」を選択します `New users` 新規登録ユーザー数の推移をカウントする指標
1. を [!UICONTROL Time period] 対象： `All-time`、および [!UICONTROL Interval] 対象： `None`
1. の下 `Group by` タブ、追加 `campaign` as `grouping field`を選択し、 **`Add All`** その場で
1. このレポートは、すべての登録済みユーザーをキャンペーンごとに表示します

**3. キャンペーン別の平均ユーザー LTV をセグメント化するレポートを作成します。**

1. 任意のダッシュボードで、 **[!UICONTROL Add Report > Create report]**
1. 「」を選択します `Average lifetime revenue` 平均ユーザーの生涯売上高を計算する指標
1. を [!UICONTROL Time period] 対象： `All-time`、および [!UICONTROL Interval] 対象： `None`
1. の下 `Group by` タブ、追加 `campaign` または `utm\_campaign` as [!UICONTROL grouping field]を選択し、 `Add All` その場で
1. このレポートは、キャンペーン別の平均ユーザー生涯売上高を表示します

**最後に、次の 3 つの分析を 1 つのレポートにまとめて、キャンペーンの ROI を計算します。**

1. 任意のダッシュボードで、 **[!UICONTROL Add Report > Create new report]**
1. 入力として追加し、上記で使用している 3 つの指標を使用します。 各フィールドには 1 文字が割り当てられます（例：\[`A`\], \[`B`\]、\[`C`\]）
1. [!UICONTROL Cost]:AdWords コスト指標を追加します – これは変数\[A\] です。 これにより、キャンペーン別のコストが返されます。
1. [!UICONTROL Users]：指標「新規ユーザー – これは変数\[B\] です」を追加します。 これは、キャンペーン別のユーザー数を返します。
1. [!UICONTROL LTV]：指標「Average Lifetime Revenue」を追加します。これは可変です\[`C`\]。 これにより、キャンペーン別の LTV が返されます。

1. グラフという単語の横にある非表示アイコンをクリックして、テーブルに焦点を当てます
1. 使用する `Add Formula` これらの指標を組み合わせるには、次の手順を実行します。
1. [!UICONTROL ROI]：式を入力します `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`\[[`A`\] は `Ad Cost by Campaigns`, \[`B`\] は `New users by campaigns`、および\[`C`\] `LTV by campaigns`. これは、（平均ユーザー LTV – 取得あたりの平均コスト） / （取得あたりの平均コスト）の比率を返します
1. [!UICONTROL Avg Return per User]：式を入力します **\[`C`\] – （\[`A`\]/\[`B`\]）**. これは、（平均ユーザー LTV） – （獲得あたりの平均コスト）を計算することによって、ユーザーに対して行われた平均利益を返します。
1. [!UICONTROL CPA]：式を入力します **`\[A\]/\[B\]`**. これは、獲得あたりの実際のキャンペーンのコストを返します。
1. 含めるその他の潜在的な指標： [!DNL AdWords] データには、次の合計が含まれます  `Impressions` および `adClicks` （送信元： [!DNL AdWords] data）、および合計 `number of orders` 特定のキャンペーンを通じて作成されます。
1. ユーザーが登録または初回購入してから 30 日後と 90 日後の LTV に基づいて ROI を計算するのも興味深いかもしれません。

1. 指標と式をクリックおよびドラッグして、レポートの列を並べ替えることができます
1. レポートに名前を付け、必ずテーブルとして保存します。

## 製品キャンペーン

製品固有の広告を実行していますか？ その場合は、特定の製品の売上高/コストを計算することで、これらのキャンペーンの ROI を測定できます。

>[!NOTE]
>
>この例では、すべてのキャンペーンコストが特定の製品の購入の生成にのみ使用されたと想定しています。 購入の生成にすべてのコストが費やされたと仮定すると、結果の ROI は最悪のケースシナリオ（購入あたりの最高コスト）を占めます。 実際の ROI はこの計算よりも高いと確信できます。 例：新規ユーザー 10 人と購入 10 件を生成したキャンペーンに$20 を費やしたとすると、購入あたりの実際のコストは$1 です。 新規ユーザーの獲得にはすべてのコストがかかるという前提の下では、1 回の購入あたりのコストは 2 ドルです。

始める前に、 [サポートチケットを送信](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 次のディメンションを行項目テーブルに結合するには、次の手順に従います（`sales\_flat\_order\_item, order\_item`）:

* 注文のソース（ユーザーレベルでリファラルソースのみを追跡する場合は、ユーザーのソースを結合します）
* 注文のキャンペーン（ユーザーレベルでのリファラルソースの追跡のみ行う場合は、ユーザーのキャンペーンに参加します）
* 注文のメディア（ユーザーレベルでのリファラルソースのみを追跡する場合は、ユーザーのメディアを結合します）

**1.次に、特定の製品についてキャンペーンあたりの売上高を返すグラフを作成することから始めます。**

1. 任意のダッシュボードで、 **[!UICONTROL Add Report > Create new report]**
1. 「」を選択します `Revenue by items` ライン項目レベルで売上高を計算する指標
1. を [!UICONTROL Time period] 対象： `All-time`、および [!UICONTROL Interval] 対象： `None`
1. の下 `Filter by` タブ、追加 `product name 'IN'` 製品 `A`、製品 `B`、製品 `C`、...」を選択し、キャンペーンのターゲットとなるすべての製品名をコンマで区切って含めます（例： `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`）
1. の下 `Group by` タブ、追加 `order's campaign` または `order's utm\_campaign` as `grouping` フィールドをクリックし、 **[!UICONTROL Add All]** その場で
1. このレポートは、特定の製品の売上高をキャンペーン別に表示します

**2. ROI を計算するには、指標を 1 つのレポートに再度組み合わせます。**

1. 任意のダッシュボードで、 **[!UICONTROL Add Report > Create new report]**
1. を追加 `Revenue by items` 指標。上記の「特定の製品のキャンペーン」レポートの指示に従って、フィルターおよびグループ化し、クリックします。 **[!UICONTROL Hide]** 指標のスカラー値の下
1. 次に、 [!DNL AdWords Cost] 指標。からの指示によってフィルターおよびグループ化に従います `Ad cost by campaigns` で確認したレポート `User acquisition campaigns` 上のセクションをクリックしてから、 **[!UICONTROL Hide]** 指標のスカラー値の下
1. これらの指標を設定した状態で、数式を追加します。
1. [!UICONTROL ROI]：式を入力します `\[A\]/\[B\]`の場合 `\[A\]` を表す `Revenue per campaign for specific product(s)` および `\[B\]` を表す `Ad cost by campaigns`. これは、（特定の製品の売上高） / （キャンペーンコスト）の比率を返します
1. [!UICONTROL Return]：式を入力します `\[A\]-\[B\]`. これは、（平均ユーザー LTV） – （獲得あたりの平均コスト）を計算して、ユーザーに対する平均利益を返します
1. （オプション） [!UICONTROL Revenue]：を表示します `Revenue by items` キャンペーンごとに特定の製品の売上高を表示するための指標
1. （オプション） [!UICONTROL Cost]：を表示します `AdWords Cost` キャンペーンのコストを確認するための指標

1. レポートに名前を付け、必ずテーブルとして保存します

**3. アドバタイズした各製品または製品グループについて、上記の手順 1 と 2 を繰り返します。**

## 関連ドキュメント

* [以下を介した注文参照ソースの追跡 [!DNL Google Analytics] 電子Commerce](../importing-data/integrations/google-ecommerce.md)
* [データベース内のユーザー紹介ソースを追跡](../analysis/google-track-user-acq.md)
* [データベース内のユーザーデバイス、ブラウザー、OS データの追跡](../analysis/track-usr-dev-browser.md)
* [最も価値のある獲得ソースとチャネルを見つける](../analysis/most-value-source-channel.md)
* [を接続 [!DNL Google Adwords] アカウント](../importing-data/integrations/google-adwords.md)
* [方法 [!DNL Google Analytics] UTM アトリビューションの仕組み](../analysis/utm-attributes.md)
* [での UTM タグ付けの 5 つのベストプラクティス [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
