---
source-git-commit: aa7acd0d863a3cd48ff83675b72c2a96eae02b4d
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---
# Adobe Commerce Intelligenceのユーザーガイド

私たちは、コミュニティやAdobeの職員によるドキュメント部門以外からの貢献を歓迎します。

## AdobeオープンSource行動規範

このプロジェクトでは、[Adobe Open Source Code of Conduct](code-of-conduct.md)または[.NET Foundation Code of Conduct](https://dotnetfoundation.org/code-of-conduct)を採用しています。 詳しくは、[寄付](contributing.md)の記事を参照してください。

## Adobe コンテンツへのコントリビューションについて

[Adobe Docs Contributor Guide](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html)を参照してください。

貢献の方法は、貢献するユーザーと変更の種類によって異なります。

### 軽微な変更

マイナーアップデートを投稿する場合は、記事にアクセスし、記事の下部に表示されるフィードバック領域をクリックし、**詳細なフィードバックオプション**&#x200B;をクリックしてから、**編集を提案**&#x200B;をクリックして、GitHubのマークダウンソースファイルに移動します。 GitHub UIを使用して更新します。 詳しくは、[Adobe Docs コントリビューターガイド ](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html)を参照してください。

このリポジトリのドキュメントやコード例に対して提出する軽微な修正や明確化は、Adobe利用条件の対象となります。

### コミュニティメンバーからの主な変更点や新しい記事

Adobe コミュニティに参加していて、新しい記事を作成したり、大きな変更を送信したりしたい場合は、Git リポジトリの「イシュー」タブを使用してイシューを送信し、ドキュメントチームとの会話を開始してください。 計画に同意したら、公開リポジトリと非公開リポジトリの作業を組み合わせて、新しいコンテンツを取り込むために従業員と協力する必要があります。

### Adobe社員の主な変化

Adobe Experience Cloud ソリューションの製品チームのテクニカルライター、プログラムマネージャー、開発者であり、技術記事の投稿や作成を担当する仕事がある場合は、GHECのプライベートリポジトリを使用する必要があります。

## ツールと設定

コミュニティのコントリビューターは、GitHub UIを使用して基本的な編集をおこなったり、リポジトリをフォークして主要なコントリビューションを作成したりできます。

詳しくは、[Adobe Docs Contributor Guide](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html)を参照してください。

## Markdownを使用してトピックを書式設定する方法

このリポジトリ内のすべての記事では、GitHubのマークダウンを使用しています。 Markdownに詳しくない場合は、以下を参照してください。

- [Markdown構文ガイド](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax)
- [Markdown構文チートシート](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/cheatsheet)

## 画像の最適化のためのプリコミットフック

このリポジトリには、コミット前に画像を最適化する自動のプリコミットフックが含まれています。 **すべてのコントリビューターは、一貫した画像の最適化とリポジトリサイズの削減を確実にするために、これらのフック**&#x200B;を有効にする必要があります。

### クイック設定

リポジトリのクローンを作成したら、次を実行します。

```bash
.githooks/setup-hooks.sh
```

### フックの機能

- ステージングされた画像ファイルを自動的に検出（`.png`、`.jpeg`、`.jpg`、`.gif`、`.svg`）
- `image_optim`を実行してラスター画像（`.png`、`.jpeg`、`.jpg`、`.gif`）を圧縮および最適化します
- 最適化された画像を自動的にリステージ
- コミットされたすべてのラスター画像が適切に最適化されていることを確認します
- ステージングされたSVGをサイズ制限に照らし合わせてチェックし、サイズが大きすぎるSVGが`help/`から参照されている場合はコミットを中止します（そうでない場合は警告するだけです）

### Adobe Workfrontの利点

- リポジトリサイズの削減
- ドキュメントのページ読み込みを高速化
- あらゆる貢献者で一貫した画質
- 手作業による最適化は不要です

セットアップ手順、トラブルシューティング、設定の詳細については、[`.githooks/README.md`](.githooks/README.md)を参照してください。

## Experience League オーサリングガイド

### Adobe Experience Managerの導入方法

- [Adobe Experience Managerの概要](https://experienceleague.adobe.com/en/docs/authoring-guide/using/getting-started/getting-started)
- [Git設定](https://experienceleague.adobe.com/en/docs/authoring-guide/using/setup/tools/git-setup)
- [GitおよびGitHub documentation essentials](https://experienceleague.adobe.com/en/docs/authoring-guide/using/setup/tools/git-fundamentals)
- [クイックスタートのビデオ](https://experienceleague.adobe.com/en/docs/authoring-guide/using/getting-started/quick-start-guides/quick-start-overview)

### ワークフロー

- [利用頻度の低いコントリビューター向けのワークフロー](https://experienceleague.adobe.com/en/docs/authoring-guide/using/editing/git-workflow-infrequent-user)
- [GitHub プルリクエスト](https://experienceleague.adobe.com/en/docs/authoring-guide/using/editing/public-github)

### 編集

- [オーサリングのベストプラクティス](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/authoring-best-practices)
- [Markdown構文ガイド](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/markdown-syntax)
- [Markdown構文チートシート](https://experienceleague.adobe.com/en/docs/authoring-guide/using/markdown/cheatsheet)
- [テーブルの操作](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/tables)
- [リンクの追加](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/linking)
- [コンテンツの移行と再構築](https://experienceleague.adobe.com/en/docs/authoring-guide/using/authoring/restructure-new)
