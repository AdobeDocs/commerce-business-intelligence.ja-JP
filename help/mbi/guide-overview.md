---
title: Commerce Intelligence ユーザーガイド
description: Commerce Intelligence のデータ管理者向けの包括的な情報。
breadcrumb-title: ガイドの概要
seo-title: Commerce Intelligence User Guide
seo-description: Describes how to use Adobe Commerce Intelligence features used to gain insights from Adobe Commerce or Magento Open Source data, along with other third-party data sources.
exl-id: f62c7a98-1b4c-4abb-9692-50ce0f3ee1fb
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 2%

---


# [!DNL Adobe Commerce Intelligence] ユーザーガイド

>[!NOTE]
>
>[!DNL Adobe Commerce Intelligence] は以前は [!DNL Magento Business Intelligence] と呼ばれていました。 このガイドで変更内容を取り込むために、現在、一連のアップデートが進行中です。

データ管理者には、次の 2 つの領域があります。

- 管理者：この領域を使用して、設定 UI およびレポートにアクセスします。
- コマンドラインインターフェイス（CLI）：このツールを使用して、インストールタスクとバックエンド設定タスクを実行します。

## 使用方法

このガイドには、組織内でどのような役割を担っているかに基づいて、以下の節が編成されています。

- [ データユーザー ](data-user.md)：ビジネス上の意思決定に役立つデータを使用します。 チームのデータアナリストからレポートやダッシュボードを受け取る場合もありますが、これらのレポートやダッシュボードの作成方法の詳細も必要になります。
- [ データアナリスト ](data-analyst.md)：クエリを適切に設計し、データ分析の頼りになる人物です。 データに関する質問に対する特定の回答を見つける方法を理解しており、同僚のセルフサービスエクスペリエンスを促進したいと考えています。
- 管理者：ライセンス、ユーザーの追加と削除、重要な管理タスクの処理など、[!DNL Commerce Intelligence] アカウントを管理します。

上記の役割ベースのワークフローに加えて、このガイドには次の内容も含まれます。

- ベストプラクティス：[!UICONTROL Commerce Intelligence] は堅牢で柔軟なプラットフォームであり、同様のタスクを実行する方法は多数あります。 このセクションでは、データのキャプチャ、分析、表示に [!DNL Commerce Intelligence] に推奨される方法をまとめます。
- Tutorials：これらのセルフガイド型チュートリアルに従って、[!DNL Commerce Intelligence] の機能を学習します。

## お問い合わせ

ご不明な点やプロフェッショナルサービスを利用したい場合、またはアカウントで問題が発生した場合は、[ サポートチーム ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) にお問い合わせください。

### サービスポリシー

[ カスタマーサポートチームが提供するサービスのリスト ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) を参照してください。

### サポートチケットの送信

高度な計算列の作成に関するサポートが必要な場合は、 欠陥または接続の問題が発生しましたか？ サポートチームに連絡する必要がある場合、Adobeは、[ サポートチケットガイドライン ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) を使用するように求めます。 このガイドラインでは、Adobeがこの問題を解決するために必要な情報の概要を説明します。

## 使用可能なドキュメント

| ドキュメントリソース | 説明 |
|----------------------- | ----------- |
| [Adobe Commerce 2.4 マーチャントドキュメント ](https://experienceleague.adobe.com/docs/commerce-admin/user-guides/home.html) | Adobe CommerceとMagento Open Sourceの両方に関するマーチャント向けドキュメント |
| [Adobe Commerce向けサービスのドキュメント ](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/home.html) | マーチャントがビジネスの主要なコンポーネントをストアと統合するのに役立つ、サービスのコレクションをサポートするドキュメント。 |
| [Adobe Commerce 2.4 運用ガイド ](https://experienceleague.adobe.com/docs/commerce-operations/operational-guides/home.html) | Adobe CommerceおよびMagento Open Sourceプラットフォームにデプロイされたプロジェクトを開発、デプロイ、管理するためのコンセプト、プロセス、ツールおよびベストプラクティスに関するシステムドキュメント。 |
| [Adobe Commerce 2.4 開発者向けドキュメント ](https://developer.adobe.com/commerce/) | Adobe CommerceまたはMagento Open Sourceの構築とカスタマイズに使用される、開発者向けドキュメント |

{style="table-layout:auto"}
