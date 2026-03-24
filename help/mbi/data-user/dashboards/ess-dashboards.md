---
title: ダッシュボード
description: ダッシュボードの作成方法と操作方法について説明します。
exl-id: a872344b-ac66-41eb-a471-5a69f8802527
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/Gtb2JIULI8lFIu5uqgN2NlCg-p9Djfy6swWtCkzClUc
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
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 628
ht-degree: 0%

---

# ダッシュボード

[!DNL Adobe Commerce Intelligence] ダッシュボードでは、ストアのパフォーマンスと販売活動を一目で素早く確認できます。 個々のダッシュボードは、ほかのユーザーと共有し、論理グループに整理することができます。 他のユーザーに対して異なるレベルの権限を設定することもできます。

レポートを作成し、ダッシュボードに追加し、データをExcelにエクスポートするのは簡単です。 チャートやレポートは、ダッシュボード上の位置にサイズ変更したりドラッグしたりできます。

![&#x200B; ダッシュボード &#x200B;](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## ダッシュボードの作成 {#createdash}

ダッシュボードは、レポートビルダーで作成した分析用のテーマ別のバケットとして共有できます。 これにより、チームのコラボレーションを促進し、組織全体の信頼できる唯一の情報源を維持できます。

*管理者または標準ユーザー*&#x200B;の場合は、`Dashboard Options` ドロップダウンをクリックして「`Create New dashboard`」を選択すると、ダッシュボードを作成できます。

作成するダッシュボードの外観は完全に自分で決めることができます。 ダッシュボードの要素は、ニーズやワークフローに合わせて、任意の方法で配置したりサイズを変更したりできます。

![&#x200B; サイズ変更ダッシュボード要素を配置](../../assets/arrange_resize_dashboard_element.gif)

### ダッシュボードの作成

1. メニューで、**[!UICONTROL Dashboards]**&#x200B;をクリックします。

1. デフォルトのダッシュボードの名前は、ダッシュボードヘッダーの左上隅に表示されます。 下向き矢印（![下向き矢印アイコン &#x200B;](../../assets/magento-bi-btn-down.png)）をクリックして、使用可能なオプションを表示します。

   ![&#x200B; ダッシュボードの作成](../../assets/magento-bi-dashboard-create.png)

1. **[!UICONTROL Create Dashboard]**&#x200B;をクリックします。 次に、次の操作を行います。

   * ダッシュボードの`Name`を入力します。

   * ダッシュボードの`Group`を作成するには、グループの名前を入力します。

     例えば、Commerceのインストールに複数のストアビューがある場合は、各ストアビューにグループを作成できます。

   * **[!UICONTROL Create]**&#x200B;をクリックします。

   ![&#x200B; ダッシュボード名](../../assets/magento-bi-dashboard-create-name.png)

   * 新しいダッシュボードの名前が左上隅に表示されます。 下向き矢印（![下向き矢印アイコン &#x200B;](../../assets/magento-bi-btn-down.png)）をクリックして、オプションを表示します。 グループを作成した場合、新しいダッシュボードがリストのグループの下に表示されます。

### レポートを追加

1. レポートを追加するには、次のいずれかの操作を行います。

   * ページの&#x200B;**[!UICONTROL Add a report]** プロンプトをクリックします。

   * ダッシュボードヘッダーで、**[!UICONTROL Add Report]**&#x200B;をクリックします。

     ![&#x200B; レポートを追加](../../assets/magento-bi-dashboard-create-add-report.png)

1. **[!UICONTROL Create Report]**&#x200B;をクリックして&#x200B;**[!UICONTROL Report Builder Options]**&#x200B;を表示します。

   ![Report Builder オプション &#x200B;](../../assets/magento-bi-report-builder.png)

## ダッシュボード上のアイテムの配置

* グラフまたはレポートのサイズを変更するには、右下隅を新しいサイズにドラッグします。

* グラフまたはレポートを移動するには、カーソルが十字に変わるまで、タイトルまたはヘッダーにカーソルを合わせます。 次に、位置にドラッグします。

## ダッシュボードの管理 {#managedash}

**[!DNL Manage Data** > **Dashboards]**&#x200B;では、所有しているダッシュボードのユーザー権限を管理したり、不要になったダッシュボードを削除したり、デフォルトのダッシュボードを設定したりできます。

### ダッシュボードの共有 {#sharingdash}

組織全体で[!DNL Commerce Intelligence]を真に拡大し、貴重なインサイトを提供するために、Adobeでは、作成したダッシュボードを他のチームメンバーと共有することを推奨しています。 *ページの上部にある「*」オプションをクリックすると、所有しているダッシュボードを`Share Dashboard`と共有できます。

ダッシュボードを共有する場合、組織全体または個人ごとに権限を割り当てることができます。つまり、レポートを表示および編集できるユーザーを決定できます。

>[!NOTE]
>
>`Read-Only`人のユーザーは、直接共有されたダッシュボードにのみアクセスできます。ダッシュボードを自分で検索して追加することはできません。 ループに入れるのを忘れないでください！

### 共有ダッシュボードへのアクセス {#accessshared}

*管理者または標準ユーザー*&#x200B;で、アカウントに共有ダッシュボードを追加する場合は、**[!UICONTROL Dashboard Options]**&#x200B;をクリックし、ドロップダウンで&#x200B;**[!UICONTROL Find]**&#x200B;をクリックします。

![&#x200B; ダッシュボードを検索](../../assets/find_dashboard.png)<!--{: width="1000" height="535"}-->

### ダッシュボード設定の管理

1. メニューで、**[!DNL Manage Data** > **Dashboards]**&#x200B;をクリックします。

1. 該当する場合は、新しい`Dashboard Name`を入力します。

1. ダッシュボードを特定の`Dashboard Group`に割り当てるには、グループのリストから選択します。

   **`Permissions`**

   すべてのユーザーにダッシュボードへの同じレベルのアクセス権を付与するには、次の操作を行います。

   1. **`Shared with`**&#x200B;で、次のいずれかのオプションを選択します。

      * `View`
      * `Edit`
      * `None`

   1. 確認を求められたら、**[!UICONTROL OK]**&#x200B;をクリックして、各ユーザーの権限レベルを更新します。

   1. 個人の権限レベルを変更するには、リスト内のユーザーが権限レベルを変更します。 変更は自動的に保存されます。

   **`Default`**

   1. このダッシュボードを[!DNL Commerce Intelligence] アカウントのデフォルトにするには、**[!UICONTROL Make Default]**&#x200B;をクリックします。

   **`Remove`**

   1. ダッシュボードを削除するには、**[!UICONTROL Delete Dashboard]**&#x200B;をクリックします。
