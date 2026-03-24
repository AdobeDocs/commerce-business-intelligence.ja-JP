---
title: Commerce Intelligence ユーザーガイド
description: Commerce Intelligence のデータ管理者向けの包括的な情報。
breadcrumb-title: ガイドの概要
seo-title: Commerce Intelligence User Guide
seo-description: Describes how to use Adobe Commerce Intelligence features used to gain insights from Adobe Commerce or Magento Open Source data, along with other third-party data sources.
exl-id: f62c7a98-1b4c-4abb-9692-50ce0f3ee1fb
TQID: https://experienceleague.adobe.com/VOTO62g3Z13NyaT1T-QK98eHc9EVuIBt7OsW8ssEaNI
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 424
ht-degree: 2%

---

# [!DNL Adobe Commerce Intelligence] ユーザーガイド

>[!NOTE]
>
>[!DNL Adobe Commerce Intelligence]は以前[!DNL Magento Business Intelligence]と呼ばれていました。 現在、このガイドで変更をキャプチャするための一連の更新が進行中です。

データ管理者には、次の2つの領域があります。

- 管理者：この領域を使用して、設定UIとレポートにアクセスします。
- コマンドラインインターフェイス（CLI）：このツールを使用して、インストールタスクとバックエンド設定タスクを実行します。

## このガイドの使用方法

このガイドでは、組織内でどのような役割を担っているかに基づいて、次のセクションを整理しています。

- [&#x200B; データ ユーザー](data-user.md): データを使用してビジネス上の意思決定を支援しています。 チームのデータアナリストからレポートやダッシュボードを受け取る可能性がありますが、それらのレポートやダッシュボードの作成方法も知る必要があります。
- [&#x200B; データ アナリスト &#x200B;](data-analyst.md): クエリを設計し、データ分析の頼りになる人物であることに慣れています。 データに関する質問に対する具体的な回答を見つけ出し、同僚へのセルフサービス体験を促進する方法を身に付けています。
- 管理者：ライセンス、ユーザーの追加と削除、重要な管理タスクの処理など、[!DNL Commerce Intelligence] アカウントを管理します。

このガイドには、上記の役割ベースのワークフローに加えて、次の内容も含まれています。

- ベストプラクティス：[!UICONTROL Commerce Intelligence]は堅牢で柔軟なプラットフォームです。つまり、類似したタスクを実行する方法は様々です。 このセクションでは、[!DNL Commerce Intelligence]がデータのキャプチャ、分析、表示に推奨する方法をまとめています。
- チュートリアル：次のセルフガイド付きチュートリアルに従って、[!DNL Commerce Intelligence]の力を学びましょう。

## ヘルプの利用方法

ご不明な点がある場合や、お客様のアカウントで問題が発生した場合は、[&#x200B; サポートチーム &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)にお問い合わせください。

### サービスポリシー

カスタマーサポートチームが提供するサービスの[&#x200B; リストを参照してください](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)。

### サポートチケットの提出

高度な計算列の作成に関するサポートが必要ですか？ 欠陥または接続の問題が発生しましたか？ サポートチームに連絡する必要がある場合は、Adobeから[&#x200B; サポートチケットガイドライン &#x200B;](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html)を使用するよう求められます。 このガイドラインは、Adobeがこの問題を解決するために必要な情報の概要を示しています。

## 使用可能なドキュメント

| 関連文書 | 説明 |
|----------------------- | ----------- |
| [Adobe Commerce 2.4 Merchant Documentation](https://experienceleague.adobe.com/en/docs/commerce-admin/user-guides/home) | Adobe CommerceとMagento Open Sourceの両方のマーチャントに焦点を当てたドキュメント |
| [Adobe Commerce ドキュメント向けサービス &#x200B;](https://experienceleague.adobe.com/en/docs/commerce/user-guides/home) | マーチャントがストアとビジネスの主要コンポーネントを統合するのに役立つサービスのコレクションをサポートするドキュメント。 |
| [Adobe Commerce 2.4運用ガイド &#x200B;](https://experienceleague.adobe.com/en/docs/commerce-operations/operational-guides/home) | Adobe CommerceおよびMagento Open Source プラットフォームにデプロイされたプロジェクトを開発、デプロイ、保守するためのコンセプト、プロセス、ツール、ベストプラクティスに関するシステムドキュメント。 |
| [Adobe Commerce 2.4開発者向けドキュメント &#x200B;](https://developer.adobe.com/commerce/) | Adobe CommerceまたはMagento Open Sourceの構築とカスタマイズに使用する開発者向けのドキュメント |

{{$include /help/_includes/templated/whats-new.md}}

<!-- Last updated from includes: 2026-01-07 10:11:29 -->
