---
title: Adobe Analyticsを接続
description: のエンドツーエンドのカスタマージャーニーの焦点をまとめる方法を学ぶ [!DNL Adobe Analytics] さらに、お客様が頼りにしている e コマースの焦点 [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 接続 [!DNL Adobe Analytics]

>[!NOTE]
>
>が必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

この [!DNL Adobe Analytics] の統合 [!DNL Adobe Commerce Intelligence] を使用すると、のエンドツーエンドのカスタマージャーニーの焦点をまとめることができます [!DNL Adobe Analytics] さらに、お客様が頼りにしている e コマースの焦点 [!DNL Commerce Intelligence]. これにより、ストアの全体的なパフォーマンスの全体像を把握できます。

具体的には、 [!DNL Adobe Analytics] の統合 [!DNL Commerce Intelligence] マーチャントがサービスの組み合わせを開始するための機能を提供 [!DNL Adobe Commerce] および [!DNL Adobe Analytics] データセット。

- 既存のから接続を作成 [!DNL Adobe Analytics] 説明する [!DNL Commerce Intelligence].

- 1 つのレポートスイートから最大 25 個の指標およびディメンションを選択し、Data Warehouseにレプリケートします。

- すべての規格を使用 [!DNL Commerce Intelligence] レプリケートされたものを変換、結合、レポートする機能 [!DNL Adobe Analytics] データ。

## 接続の前提条件

接続するには、次の情報が必要です。

- [!DNL Adobe Analytics] ログイン資格情報

- `Name` および/または `ID` 件中 [!DNL Adobe Analytics] データのレプリケート元のレポートスイート

- レプリケート先の指標およびディメンションのリスト [!DNL Commerce Intelligence]

## の接続 [!DNL Adobe Analytics] の統合 [!DNL Commerce Intelligence]

1. に移動します `Integrations` ページの下 **[!DNL Manage Data** > **Integrations]**.

1. クリック **[!UICONTROL Add an Integration]**.

1. 「」をクリックします **[!UICONTROL Adobe Analytics]** アイコンをクリックして、 [!DNL Adobe Analytics] アカウント接続。

1. クリック **[!UICONTROL Authorize with Adobe Analytics]**.

1. を入力 [!DNL Adobe Analytics] 資格情報。 認証が成功すると、にリダイレクトされます。 [!DNL Commerce Intelligence].

1. 使用可能なレポートスイートのリストが表示されます。 データのインポート元となるレポートスイートを選択し、 **[!UICONTROL Continue]**.

1. 指標およびディメンションの選択画面が表示されます。 少なくとも 1 つの指標と 1 つのディメンション（合計 25 個までの指標およびディメンション）を選択します。 名前で検索するか、スクロールしてコンポーネントを見つけ、チェックボックスをクリックして選択します。 クリック **[!UICONTROL Continue]**.

1. 選択したレポートスイートがテーブルに表示されます。 クリック **[!UICONTROL Save]** をクリックして選択を確定します。

1. に通知 [!DNL Commerce Intelligence] [サポートチーム](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 統合が承認され、最初の接続プロセスが実行されることを確認します。

最初の接続プロセスが実行されると、テーブルは、Data Warehouseページの下の `All Tables` タブ。 レプリケートする列を選択すると、次回の完全更新後にデータが表示されます。
