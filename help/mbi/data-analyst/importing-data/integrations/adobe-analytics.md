---
title: Connect Adobe Analytics
description: のエンドツーエンドのカスタマージャーニーの焦点をまとめる方法を学ぶ [!DNL Adobe Analytics] e コマースの焦点は、 [!DNL MBI].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# 接続 [!DNL Adobe Analytics]

>[!NOTE]
>
>必要 [管理者権限](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

この [!DNL Adobe Analytics] の統合 [!DNL MBI] を使用すれば、カスタマージャーニーをエンドツーエンドで集中させることができます。 [!DNL Adobe Analytics] e コマースの焦点は、 [!DNL MBI]を使用して、ストアの全体的なパフォーマンスをより完全に把握できます。

具体的には、 [!DNL Adobe Analytics] の統合 [!DNL MBI] には、マーチャントが Commerce と Analytics のデータセットの組み合わせを開始する機能が用意されています。
- 既存のから接続を作成 [!DNL Adobe Analytics] ～を説明する [!DNL MBI].
- 1 つのレポートスイートから最大 25 個の指標およびディメンションを選択し、にレプリケートします。 [!DNL MBI] data warehouse を使用します。
- すべての標準を使用 [!DNL MBI] レプリケートされたの変換、結合、およびレポートする機能 [!DNL Adobe Analytics] データ。

## 接続の前提条件

接続するには、次の情報が必要です。
- [!DNL Adobe Analytics] ログイン資格情報
- `Name` および/または `ID` / [!DNL Adobe Analytics] データのレプリケート元のレポートスイート
- レプリケート先の指標およびディメンションのリスト [!DNL MBI]

## 接続 [!DNL Adobe Analytics] MBI の統合

1. 次に移動： `Integrations` 下のページ **[!DNL Manage Data** > **Integrations]**.
1. クリック **[!UICONTROL Add an Integration]**：画面の右側にあります。
1. 次をクリック： **[!UICONTROL Adobe Analytics]** アイコンをクリックして、 [!DNL Adobe Analytics] アカウント接続。
1. クリック **[!UICONTROL Authorize with Adobe Analytics]**.
1. を入力します。 [!DNL Adobe Analytics] 資格情報。 認証が成功すると、にリダイレクトされます。 [!DNL MBI].
1. 使用可能なレポートスイートのリストが表示されます。 データのインポート元のレポートスイートを選択し、 **[!UICONTROL Continue]**.
1. 指標およびディメンションの選択画面が表示されます。 1 つ以上の指標と 1 つ以上のディメンションを選択し、合計 25 個の指標とディメンションを組み合わせます。 名前で検索するか、スクロールしてコンポーネントを探し、チェックボックスをクリックして選択します。 クリック **[!UICONTROL Continue]**.
1. 選択したレポートスイートがテーブルに表示されます。 クリック **[!UICONTROL Save]** をクリックして選択を確定します。
1. 次の情報を [!DNL MBI] 統合が承認され、初期接続プロセスが実行されるサポートチーム。

最初の接続プロセスが実行されると、テーブルがData Warehouseページの `All Tables` タブをクリックします。 レプリケートする列を選択すると、次の完全更新の後にデータが表示されます。
