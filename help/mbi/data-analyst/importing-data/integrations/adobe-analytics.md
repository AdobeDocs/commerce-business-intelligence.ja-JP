---
title: Adobe Analyticsとの連携
description: ' [!DNL Adobe Analytics] のエンドツーエンドのカスタマージャーニーに焦点を当て、 [!DNL Commerce Intelligence]から利用するe コマースに焦点を当てる方法について説明します。'
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/KkiKySM2q8ewqhQ1kdUjLuTM4iOpzrZb5Ok-UvBBpJE
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 312
ht-degree: 0%

---

# [!DNL Adobe Analytics]を接続

>[!NOTE]
>
>[管理者権限](../../../administrator/user-management/user-management.md)が必要です。

![Adobe Analyticsのロゴ &#x200B;](../../../assets/adobe-analytic-slogo.png)

[!DNL Adobe Analytics]の[!DNL Adobe Commerce Intelligence]統合により、[!DNL Adobe Analytics]のエンドツーエンドのカスタマージャーニーの焦点と、[!DNL Commerce Intelligence]から利用するe コマースの焦点を合わせることができます。 これにより、ストアの全体的なパフォーマンスを把握できます。

具体的には、[!DNL Adobe Analytics]の[!DNL Commerce Intelligence]統合は、マーチャントが[!DNL Adobe Commerce]と[!DNL Adobe Analytics]のデータセットの組み合わせを開始するための機能を提供します。

- 既存の[!DNL Adobe Analytics] アカウントから[!DNL Commerce Intelligence]への接続を作成します。

- 1つのレポートスイートから最大25個の指標とディメンションを選択して、Data Warehouseにレプリケートします。

- すべての標準[!DNL Commerce Intelligence]機能を使用して、レプリケートされた[!DNL Adobe Analytics] データの変換、結合、レポートを行います。

## 接続の前提条件

接続するには、次の情報が必要です。

- [!DNL Adobe Analytics]個のログイン資格情報

- `Name`個のレポートスイートのうち`ID`個および/または[!DNL Adobe Analytics]個からデータをレプリケートする

- [!DNL Commerce Intelligence]にレプリケートする指標とディメンションのリスト

## [!DNL Adobe Analytics]の[!DNL Commerce Intelligence]統合を接続しています

1. `Integrations`の下の&#x200B;**[!DNL Manage Data** > **Integrations]** ページに移動します。

1. **[!UICONTROL Add an Integration]**&#x200B;をクリックします。

1. **[!UICONTROL Adobe Analytics]** アイコンをクリックして、[!DNL Adobe Analytics] アカウント接続を認証できるページにアクセスします。

1. **[!UICONTROL Authorize with Adobe Analytics]**&#x200B;をクリックします。

1. [!DNL Adobe Analytics]資格情報を入力してください。 認証が成功すると、[!DNL Commerce Intelligence]にリダイレクトされます。

1. 使用可能なレポートスイートのリストが表示されます。 データのインポート元となるレポートスイートを選択し、**[!UICONTROL Continue]**&#x200B;をクリックします。

1. 指標とディメンションの選択画面が表示されます。 1つ以上の指標と1つ以上のディメンションを選択し、合計25個までの指標とディメンションを選択します。 名前で検索するか、スクロールしてコンポーネントを見つけ、チェックボックスをクリックして選択します。 **[!UICONTROL Continue]**&#x200B;をクリックします。

1. 選択したレポートスイートがテーブルに表示されます。 **[!UICONTROL Save]**&#x200B;をクリックして選択を確定します。

1. [!DNL Commerce Intelligence] [&#x200B; サポートチーム &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=ja)に、統合が承認され、最初の接続プロセスが実行されていることを通知します。

最初の接続プロセスが実行されると、テーブルはData Warehouse ページの「`All Tables`」タブで利用できるようになります。 複製する列を選択すると、データは次の完全な更新後に表示されます。
