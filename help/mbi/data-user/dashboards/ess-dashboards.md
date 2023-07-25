---
title: ダッシュボード
description: ダッシュボードを作成し、使用する方法を説明します。
exl-id: a872344b-ac66-41eb-a471-5a69f8802527
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# ダッシュボード

[!DNL Adobe Commerce Intelligence] ダッシュボードでは、ストアのパフォーマンスと販売活動を一目で簡単に確認できます。 個々のダッシュボードは、他のユーザーと共有し、論理グループに整理できます。 また、他のユーザーに対して異なるレベルの権限を設定することもできます。

レポートの作成、ダッシュボードへの追加、Excel へのデータのエクスポートは簡単におこなえます。 グラフやレポートは、サイズを変更したり、ダッシュボード上の位置にドラッグしたりすることができます。

![ダッシュボード](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## ダッシュボードの作成 {#createdash}

ダッシュボードは、ダッシュボードで作成する分析のテーマを持つ共有可能なReport Builderです。 この方法を使用して、チームに対して、組織全体でコラボレーションを行い、単一の真実の源を維持するよう促すことができます。

*管理者または Standard ユーザーの場合*&#x200B;をクリックすると、 `Dashboard Options` ドロップダウンと選択 `Create New dashboard`.

作成するダッシュボードの外観はユーザー次第です。 ダッシュボード内の要素の配置やサイズ変更は、ニーズやワークフローに合わせて自由におこなうことができます。

![ダッシュボード要素のサイズ変更を行う](../../assets/arrange_resize_dashboard_element.gif)

### ダッシュボードの作成

1. メニューで、 **[!UICONTROL Dashboards]**.

1. デフォルトのダッシュボードの名前が、ダッシュボードヘッダーの左上隅に表示されます。 下向き矢印 (![](../../assets/magento-bi-btn-down.png)) をクリックして、使用可能なオプションを表示します。

   ![ダッシュボードを作成](../../assets/magento-bi-dashboard-create.png)

1. クリック **[!UICONTROL Create Dashboard]**. 次に、以下の手順を実行します。

   * を入力します。 `Name` をダッシュボードに追加します。

   * を作成するには、以下を実行します。 `Group` 「ダッシュボード」に、グループの名前を入力します。

     例えば、コマースのインストールに複数のストア表示がある場合、各ストア表示に対してグループを作成できます。

   * クリック **[!UICONTROL Create]**.

   ![ダッシュボード名](../../assets/magento-bi-dashboard-create-name.png)

   * 新しいダッシュボードの名前が左上隅に表示されます。 下向き矢印 (![](../../assets/magento-bi-btn-down.png)) をクリックしてオプションを表示します。 グループを作成した場合は、リスト内のグループの下に新しいダッシュボードが表示されます。

### レポートの追加

1. レポートを追加するには、次のいずれかの操作を行います。

   * 次をクリック： **[!UICONTROL Add a report]** プロンプトが表示されます。

   * ダッシュボードのヘッダーで、 **[!UICONTROL Add Report]**.

     ![レポートの追加](../../assets/magento-bi-dashboard-create-add-report.png)

1. クリック **[!UICONTROL Create Report]** 見せる **[!UICONTROL Report Builder Options]**.

   ![Report Builderオプション](../../assets/magento-bi-report-builder.png)

## ダッシュボードでの項目の配置

* グラフまたはレポートのサイズを変更するには、右下隅を新しいサイズにドラッグします。

* グラフまたはレポートを移動するには、タイトルまたはヘッダーの上にマウスポインターを置き、カーソルが十字に変わるまでマウスを移動します。 次に、それを位置にドラッグします。

## ダッシュボードの管理 {#managedash}

In **[!DNL Manage Data** > **Dashboards]**&#x200B;を使用すると、自分が所有するダッシュボードのユーザー権限を管理したり、不要になったダッシュボードを削除したり、デフォルトのダッシュボードを設定したりできます。

### ダッシュボードの共有 {#sharingdash}

真のスケールを設定するには [!DNL Commerce Intelligence] 組織全体を通じて、貴重なインサイトを提供するAdobeは、作成したダッシュボードを他のチームメンバーと共有することを推奨します。 *自分が所有するダッシュボードを共有できます* クリックして `Share Dashboard` 」オプションを使用して、製品内で利用できます。

ダッシュボードを共有する場合、組織全体または複数の権限を個別に割り当てることができます。つまり、レポートを表示および編集できるユーザーを決定できます。

>[!NOTE]
>
>`Read-Only` ユーザーは、直接共有されるダッシュボードに対するアクセス権のみを持ち、ダッシュボードを検索したり追加したりすることはできません。 彼らをループ内に置いておくのを忘れないでください！

### 共有ダッシュボードへのアクセス {#accessshared}

*管理者または標準ユーザーの場合* 共有ダッシュボードをアカウントに追加する場合は、 **[!UICONTROL Dashboard Options]** をクリックし、 **[!UICONTROL Find]** 」と入力します。

![ダッシュボードを検索](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### ダッシュボード設定の管理

1. メニューで、 **[!DNL Manage Data** > **Dashboards]**.

1. 必要に応じて、新しい `Dashboard Name`.

1. ダッシュボードを特定の `Dashboard Group`、グループのリストから「 」を選択します。

   **`Permissions`**

   すべてのユーザーに同じレベルのダッシュボードへのアクセス権を与えるには、次の手順を実行します。

   1. の下 **`Shared with`**、次のいずれかのオプションを選択します。

      * `View`
      * `Edit`
      * `None`

   1. 確認メッセージが表示されたら、「 **[!UICONTROL OK]** をクリックして、各ユーザーの権限レベルを更新します。

   1. 個人の権限レベルを変更するには、リスト内のユーザーを探して、権限レベルを変更します。 変更は自動的に保存されます。

   **`Default`**

   1. このダッシュボードを [!DNL Commerce Intelligence] アカウントをクリックします。 **[!UICONTROL Make Default]**.

   **`Remove`**

   1. ダッシュボードを削除するには、 **[!UICONTROL Delete Dashboard]**.
