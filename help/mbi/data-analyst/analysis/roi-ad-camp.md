---
title: 広告キャンペーンの ROI の向上
description: キャンペーンのパフォーマンスを評価する様々な方法について説明します。
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1284'
ht-degree: 0%

---

# 広告キャンペーンと ROI

MBI を使用すると、 [広告コストデータと売上高データの結婚](../../data-analyst/importing-data/integrations/google-adwords.md) をデータベースから削除します。 これにより、ROI が最も高いキャンペーンを特定できます。 この記事では、キャンペーンのパフォーマンスを評価する様々な方法を紹介します。

## 前提条件

* 広告コストデータを読み込む：
   * [接続 [!DNL Google AdWords] から [!DNL MBI]](../importing-data/integrations/google-adwords.md):これにより、 [!DNL Adwords] ～に費やす [!DNL MBI]
   * [他の広告コストデータをアップロード](../importing-data/connecting-data/import-offline-ad-data.md):これは、への直接コネクタのないチャネルの場合に推奨されます。 [!DNL MBI]
   * 複数のソースからコストデータをインポートする場合、 [統合](../../best-practices/consolidating-your-tables.md) のデータ [!DNL MBI]. 簡単に [サポートチケットを提出する](../../guide-overview.md).
* [ユーザー獲得チャネルデータの追跡](../analysis/google-track-user-acq.md)

## ユーザー獲得キャンペーン

ユーザーの獲得をターゲットにしたキャンペーンは、以下を含む様々な観点から測定できます。

1. 獲得したキャンペーンの新規ユーザー数
1. キャンペーンの登録から購入へのコンバージョン率
1. 平均ユーザーライフタイム値 (LTV) に基づくキャンペーンの ROI

上記の分析 (1) と (2) については、 [上位のマーケティングチャネルの特定](../analysis/most-value-source-channel.md). ここでは、分析 (3) を検討し、時間の経過と共にキャンペーンの ROI を測定します。 これにより、特定のキャンペーンからユーザーが獲得した場合に、獲得コストを賄うのに十分なライフタイム売上高が生じたかどうかがわかります。

>[!NOTE]
>
>すべてのキャンペーンコストは、新規ユーザーの獲得にのみ使用されたと仮定します。 実際には、キャンペーンのコストは、コンバージョンされていない訪問、リピート購入者の獲得とも共有されます。 しかし、すべてのコストが新規登録ユーザーの獲得に使用されると仮定すると、結果の ROI は最悪のケースシナリオ（獲得あたりの最高コスト）を考慮するので、実際の ROI が当社の計算よりも高いことを確認できます。
>
>例：新規ユーザー 10 人とリピート購入者 10 人を生み出したキャンペーンに$20 を費やしたと仮定すると、新規ユーザー 1 人あたりの実際のコストは$1 ですが、すべてのコストで新規ユーザーを獲得したと仮定すると、獲得あたりのコストは$2 です )。

**1. まず、広告コストをキャンペーン別にセグメント化するグラフを作成します。**

1. の作成 [!UICONTROL Metric] あなたの時間の中での過ごし方を示す
1. に移動します。 [!UICONTROL Data > Metrics]
1. 選択 `Add New Metric` をクリックし、 [!DNL `Adwords...`] 記録しているテーブル [!DNL AdWords] コストデータ。
1. 指標エディターで、指標に名前を付けます ( 例： [!UICONTROL AdWord Cost])
1. ドロップダウンを使用し、 **合計** の `adCost` 列 [!DNL Adwords...] 次の項目で並べ替えられたテーブル（変更） `date` 列。
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. これで完了です。 クリック `Back to Metric List` をクリックし、任意のダッシュボードに移動します。

1. キャンペーン別のセグメント支出のレポートを作成する
1. 任意のダッシュボードで、 [!UICONTROL Add Report > Create new report]
1. を選択します。 [!UICONTROL Adword Cost] 先ほど作成した指標
1. を [!UICONTROL Time period] から `All-time`、および [!UICONTROL Interval] から `None`
1. 以下 `Group by` タブ、追加 `campaign` as [!UICONTROL grouping field]をクリックし、 `Add All` をクリックします。
1. このレポートには常時表示されます [!DNL AdWords] キャンペーン別コスト

**2. 次に、キャンペーン別に新規ユーザー数をカウントするレポートを作成します。**

1. 任意のダッシュボードで、 **[!UICONTROL Add Report > Create new report]**
1. を選択します。 `New users` 新規登録ユーザー数を経時的にカウントする指標
1. を [!UICONTROL Time period] から `All-time`、および [!UICONTROL Interval] から `None`
1. 以下 `Group by` タブ、追加 `campaign` as `grouping field`をクリックし、 **`Add All`** 箱の中に
1. このレポートには、キャンペーン別に過去に登録されたユーザーが表示されます

**3. また、平均的なユーザー LTV をキャンペーン別にセグメント化するレポートも作成します。**

1. 任意のダッシュボードで、 **[!UICONTROL Add Report > Create new report]**
1. を選択します。 `Average lifetime revenue` 平均ユーザーのライフタイム売上高を計算する指標
1. を [!UICONTROL Time period] から `All-time`、および [!UICONTROL Interval] から `None`
1. 以下 `Group by` タブ、追加 `campaign` または `utm\_campaign` as [!UICONTROL grouping field]をクリックし、 `Add All` 箱の中に
1. このレポートには、キャンペーン別の平均ユーザーライフタイム売上高が表示されます

**最後に、次の 3 つの分析を 1 つのレポートにまとめて、キャンペーンの ROI を計算します。**

1. 任意のダッシュボードで、 **[!UICONTROL Add Report > Create new report]**
1. を入力として追加する場合、上記で使用した 3 つの指標を使用します。 それぞれにレターが割り当てられます ( 例：\[`A`\], \[`B`\] および\[`C`\])
1. [!UICONTROL Cost]:AdWords のコスト指標を追加します。これは変数\[A\] になります。 これにより、単にキャンペーンごとにコストが返されます。
1. [!UICONTROL Users]:指標「新規ユーザー」を追加します。これは変数「[B\]」になります。 これにより、単にキャンペーン別にユーザー数が返されます。
1. [!UICONTROL LTV]:平均全期間売上高指標を追加します — これは変数\[ です`C`\]. これは、単にキャンペーンで LTV を返します。

1. 「グラフ」という単語の横にある非表示アイコンをクリックして、テーブルにフォーカスできるようにします。
1. 次に、 `Add Formula` これらの指標を組み合わせるには、次のようにします。
1. [!UICONTROL ROI]:数式を入力 `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`\[`A`\] は `Ad Cost by Campaigns`, \[`B`\] は `New users by campaigns`，および\[`C`\] `LTV by campaigns`. これにより、（平均ユーザー LTV — 獲得あたりの平均コスト） / （獲得あたりの平均コスト）の比率が返されます
1. [!UICONTROL Avg Return per User]:数式を入力 **\[`C`\]-(\[`A`\]/\[`B`\])**. これにより、（平均ユーザー LTV） — （獲得あたりの平均コスト）を計算して、ユーザーに対しておこなわれた平均利益が返されます。
1. [!UICONTROL CPA]:数式を入力 **`\[A\]/\[B\]`**. これにより、獲得あたりの実際のキャンペーンのコストが返されます。
1. 含める他の潜在的な指標 [!DNL AdWords] データには～の合計が含まれる  `Impressions` および `adClicks` （から） [!DNL AdWords] データ ) と合計 `number of orders` 特定のキャンペーンを通じて作成されます。
1. また、ユーザーが登録または初回購入してから 30 日と 90 日後の LTV に基づいて ROI を計算するのも興味深い場合があります。

1. 自由にクリックし、指標と数式をドラッグして、レポートの列を並べ替えることができます
1. レポートに名前を付けて、必ずテーブルとして保存してください。

## 製品キャンペーン

製品固有の広告を実行しているか。 その場合は、特定の製品の売上高/コストを計算することで、これらのキャンペーンの ROI を測定できます。

>[!NOTE]
>
>特定の製品の購入を生み出すために、すべてのキャンペーンコストが排他的に使用されたと仮定します。 すべてのコストが購入の生成に費やされたと仮定すると、結果の ROI は最悪のケースシナリオ（購入あたりの最大コスト）を考慮するので、実際の ROI がこの計算よりも高いことを確認できます。 例：新規ユーザー 10 人と購入 10 人を生み出したキャンペーンに$20 を費やした場合、実際の購入あたりのコストは$1 ですが、すべてのコストで新規ユーザーを獲得したと仮定すると、購入あたりのコストは$2 です。)*

始める前に [サポートチケットを提出する](../../guide-overview.md) 次のディメンションを行項目テーブルに結合するには (`sales\_flat\_order\_item, order\_item`):

* 注文のソース（ユーザーレベルで紹介ソースのみを追跡し、ユーザーのソースに参加する場合）
* 注文のキャンペーン（ユーザーレベルで紹介ソースのみを追跡し、ユーザーのキャンペーンに参加する場合）
* 注文のメディア（ユーザーレベルで紹介ソースのみを追跡し、ユーザーのメディアに参加する場合）

**1. 次に、特定の製品に関するキャンペーンごとの売上高を返すグラフを作成します。**

1. 任意のダッシュボードで、 **[!UICONTROL Add Report > Create new report]**
1. を選択します。 `Revenue by items` 行項目レベルの売上高を計算する指標
1. を [!UICONTROL Time period] から `All-time`、および [!UICONTROL Interval] から `None`
1. 以下 `Filter by` タブ、追加 `product name 'IN'` 製品 `A`，製品 `B`，製品 `C`, ...&quot; キャンペーンでターゲットとされるすべての製品名をコンマで区切って含めます ( 例： `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. 以下 `Group by` タブ、追加 `order's campaign` または `order's utm\_campaign` as `grouping` 「 」フィールドで「 」をクリックし、 **[!UICONTROL Add All]** 箱の中に
1. このレポートには、キャンペーン別の特定の製品の売上高が表示されます

**2. ROI を計算するために、指標を 1 つのレポートに再度組み合わせます。**

1. 任意のダッシュボードで、 **[!UICONTROL Add Report > Create new report]**
1. を `Revenue by items` 指標を使用する場合は、上の特定の製品に関するキャンペーンレポートの指示に従い、フィルターおよびグループ化を使用して、 **[!UICONTROL Hide]** 指標のスカラー値の下に
1. 次に、 [!DNL AdWords Cost] 指標 ( フィルターに従い、 `Ad cost by campaigns` 調査したレポート `User acquisition campaigns` セクション上次に、 **[!UICONTROL Hide]** 指標のスカラー値の下に
1. これらの指標を設定し、数式を追加します。
1. [!UICONTROL ROI]:数式を入力 `\[A\]/\[B\]`、 `\[A\]` 表 `Revenue per campaign for specific product(s)` および `\[B\]` 表 `Ad cost by campaigns`. これにより、（特定の製品の売上高）/（キャンペーンコスト）の比率が返されます
1. [!UICONTROL Return]:数式を入力 `\[A\]-\[B\]`. これにより、（平均ユーザー LTV） — （獲得あたりの平均コスト）を計算して、ユーザーに対して行われた平均利益が返されます
1. （オプション） [!UICONTROL Revenue]:次を表示： `Revenue by items` キャンペーンごとの特定の製品の売上高を表示する指標
1. （オプション） [!UICONTROL Cost]:次を表示： `AdWords Cost` キャンペーンのコストを表示する指標

1. レポートに名前を付け、必ずテーブルとして保存してください

**3. アドバタイズした製品または製品グループごとに、上記の手順 1 と 2 を繰り返します。**

## 関連ドキュメント

* [経由で注文のリファラルソースを追跡 [!DNL Google Analytics] E コマース](../importing-data/integrations/google-ecommerce.md)
* [データベース内のユーザー参照元を追跡する](../analysis/google-track-user-acq.md)
* [データベース内のユーザーデバイス、ブラウザー、OS データを追跡する](../analysis/track-usr-dev-browser.md)
* [最も価値のある獲得ソースとチャネルを見つける](../analysis/most-value-source-channel.md)
* [接続 [!DNL Google Adwords] アカウント](../importing-data/integrations/google-adwords.md)
* [方法 [!DNL Google Analytics] UTM 属性は機能しますか？](../analysis/utm-attributes.md)
* [での UTM タグ付けの 5 つのベストプラクティス [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
