---
title: Connect Adobe Analytics
description: のエンドツーエンドのカスタマージャーニーの焦点をまとめる方法を学ぶ [!DNL Adobe Analytics] e コマースの焦点は、 [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# 接続 [!DNL Adobe Analytics]

>[!NOTE]
>
>必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

この [!DNL Adobe Analytics] の統合 [!DNL Adobe Commerce Intelligence] を使用すれば、カスタマージャーニーをエンドツーエンドで集中させることができます。 [!DNL Adobe Analytics] e コマースの焦点は、 [!DNL Commerce Intelligence]. これにより、ストアの全体的なパフォーマンスの全体像が得られます。

具体的には、 [!DNL Adobe Analytics] の統合 [!DNL Commerce Intelligence] 商人が組み合わせを開始する機能を提供 [!DNL Adobe Commerce] および [!DNL Adobe Analytics] データセット。

- 既存のから接続を作成 [!DNL Adobe Analytics] ～を説明する [!DNL Commerce Intelligence].

- Data Warehouseにレプリケートする 1 つのレポートスイートから最大 25 個の指標およびディメンションを選択します。

- すべての標準を使用 [!DNL Commerce Intelligence] レプリケートされたの変換、結合、およびレポートする機能 [!DNL Adobe Analytics] データ。

## 接続の前提条件

接続するには、次の情報が必要です。

- [!DNL Adobe Analytics] ログイン資格情報

- `Name` および/または `ID` / [!DNL Adobe Analytics] データのレプリケート元のレポートスイート

- レプリケート先の指標およびディメンションのリスト [!DNL Commerce Intelligence]

## 接続 [!DNL Adobe Analytics] の統合 [!DNL Commerce Intelligence]

1. 次に移動： `Integrations` 下のページ **[!DNL Manage Data** > **Integrations]**.

1. クリック **[!UICONTROL Add an Integration]**.

1. 次をクリック： **[!UICONTROL Adobe Analytics]** アイコンをクリックして、 [!DNL Adobe Analytics] アカウント接続。

1. クリック **[!UICONTROL Authorize with Adobe Analytics]**.

1. を入力します。 [!DNL Adobe Analytics] 資格情報。 認証が成功すると、にリダイレクトされます。 [!DNL Commerce Intelligence].

1. 使用可能なレポートスイートのリストが表示されます。 データのインポート元のレポートスイートを選択し、 **[!UICONTROL Continue]**.

1. 指標およびディメンションの選択画面が表示されます。 1 つ以上の指標と 1 つ以上のディメンションを選択し、合計 25 個の指標とディメンションを組み合わせます。 名前で検索するか、スクロールしてコンポーネントを探し、チェックボックスをクリックして選択します。 クリック **[!UICONTROL Continue]**.

1. 選択したレポートスイートがテーブルに表示されます。 クリック **[!UICONTROL Save]** をクリックして選択を確定します。

1. 次の情報を [!DNL Commerce Intelligence] [サポートチーム](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) 統合が承認され、統合が初期接続プロセスを実行することを確認します。

最初の接続プロセスが実行されると、テーブルがData Warehouseページの `All Tables` タブをクリックします。 レプリケートする列を選択すると、次の完全更新の後にデータが表示されます。
