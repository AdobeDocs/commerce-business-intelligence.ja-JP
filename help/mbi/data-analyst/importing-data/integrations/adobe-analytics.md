---
title: Adobe Analyticsを接続
description: のエンドツーエンドのカスタマージャーニーの焦点と、 [!DNL Adobe Analytics]  に基づく e コマースの焦点を一つにまとめる方法を説明し  [!DNL Commerce Intelligence] す。
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Connect [!DNL Adobe Analytics]

>[!NOTE]
>
>[ 管理者権限 ](../../../administrator/user-management/user-management.md) が必要です。

![](../../../assets/adobe-analytic-slogo.png)

[!DNL Adobe Analytics] の [!DNL Adobe Commerce Intelligence] 統合により、[!DNL Adobe Analytics] のエンドツーエンドのカスタマージャーニーの焦点と、[!DNL Commerce Intelligence] から依存している e コマースの焦点を統合できます。 これにより、ストアの全体的なパフォーマンスの全体像を把握できます。

より具体的には、[!DNL Adobe Analytics] の [!DNL Commerce Intelligence] 統合は、マーチャントが [!DNL Adobe Commerce] と [!DNL Adobe Analytics] のデータセットの組み合わせを開始するための機能を提供します。

- 既存の [!DNL Adobe Analytics] アカウントから [!DNL Commerce Intelligence] への接続を作成します。

- 1 つのレポートスイートから最大 25 個の指標およびディメンションを選択し、Data Warehouseにレプリケートします。

- レプリケートされた [!DNL Commerce Intelligence] データの変換、結合、レポート作成には、すべての標準 [!DNL Adobe Analytics] 機能を使用します。

## 接続の前提条件

接続するには、次の情報が必要です。

- [!DNL Adobe Analytics] ログイン資格情報

- データのレプリケート元 `Name` レポートスイートの `ID` または [!DNL Adobe Analytics]

- [!DNL Commerce Intelligence] にレプリケートする指標とディメンションのリスト

## [!DNL Adobe Analytics] の [!DNL Commerce Intelligence] 統合の接続

1. `Integrations` の下の **[!DNL Manage Data** > **Integrations]** ページに移動します。

1. 「**[!UICONTROL Add an Integration]**」をクリックします。

1. **[!UICONTROL Adobe Analytics]** アイコンをクリックして、[!DNL Adobe Analytics] アカウントの接続を認証できるページにアクセスします。

1. 「**[!UICONTROL Authorize with Adobe Analytics]**」をクリックします。

1. [!DNL Adobe Analytics] 資格情報を入力します。 認証が成功すると、[!DNL Commerce Intelligence] にリダイレクトされます。

1. 使用可能なレポートスイートのリストが表示されます。 データのインポート元となるレポートスイートを選択し、「**[!UICONTROL Continue]**」をクリックします。

1. 指標およびディメンションの選択画面が表示されます。 少なくとも 1 つの指標と 1 つのディメンション（合計 25 個までの指標およびディメンション）を選択します。 名前で検索するか、スクロールしてコンポーネントを見つけ、チェックボックスをクリックして選択します。 「**[!UICONTROL Continue]**」をクリックします。

1. 選択したレポートスイートがテーブルに表示されます。 「**[!UICONTROL Save]**」をクリックして選択を確定します。

1. [!DNL Commerce Intelligence] サポートチーム [ に統合が許可されていることを通知し、最初の接続プロセスを実行します ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

最初の接続プロセスが実行されると、テーブルは、「Data Warehouse」ページの「`All Tables`」タブで使用できるようになります。 レプリケートする列を選択すると、次回の完全更新後にデータが表示されます。
