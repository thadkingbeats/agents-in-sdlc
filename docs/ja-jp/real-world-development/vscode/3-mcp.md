---
title: "演習 3 - Playwright MCP サーバーで機能をテストする"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: Agent mode][previous-lesson] · [次のレッスン: カスタム エージェント →][next-lesson]

Agent mode で絞り込み機能を作成しました。プルリクエスト (PR) を開く前に、ブラウザーで実際に動作することを確認します。アプリを手動で操作する代わりに、**Playwright Model Context Protocol (MCP) サーバー**を接続し、Copilot に実際のブラウザーを操作させて機能をテストします。その後、ブランチを公開して PR を作成します。

この演習では、次のことを行います。

- Model Context Protocol (MCP) と MCP サーバーが Copilot にツールを追加する仕組みを学びます。
- Playwright MCP サーバーをワークスペースに追加します。
- ブラウザーで絞り込み機能を手動テストするよう Copilot に依頼します。
- ブランチを公開して、絞り込み機能のプルリクエストを作成します。

## Model Context Protocol (MCP) とは

Agent mode は、エディターの外部にあるツールを利用できると、さらに強力になります。Model Context Protocol (MCP) は Copilot が外部ツールやサービスと通信するための標準的な方法です。

![コンテキスト、LLM、ツール (MCP サーバーと VS Code 拡張機能が提供するツールを含む) と agent mode の連携を示す図](../../../_images/ex1-mcp-diagram.png)

[Model Context Protocol (MCP)](https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/) を使うと、AI エージェントは外部ツールやサービスと通信できます。MCP によって、リソースを使って最新情報にアクセスしたり、ツールを使って開発者に代わって操作を行ったりできます。

MCP サーバーは AI エージェントと外部ツールやサービスをつなぎます。既存の API や npm パッケージなどのローカル ツールとの通信を管理します。各 MCP サーバーは、エージェントが利用できる一連のツールとリソースを提供します。

よく使われている MCP サーバーの例を示します。

- **[GitHub MCP Server](https://github.com/github/github-mcp-server)**: GitHub リポジトリを管理する API にアクセスし、リポジトリの作成・更新、issue やプルリクエストの管理などを行います。
- **[Playwright MCP Server](https://github.com/microsoft/playwright-mcp)**: Playwright によるブラウザー自動化を提供し、Web ページの移動、フォームの入力、ボタンの選択などを行います。

さまざまなツールやリソースにアクセスできる MCP サーバーがほかにもあります。GitHub は、見つけやすさとエコシステムへの貢献を促進するために [MCP レジストリ](https://github.com/mcp)をホストしています。

> [!CAUTION]
> セキュリティの観点から、MCP サーバーはほかの依存関係と同様に扱ってください。使用前にソース コードを慎重に確認し、発行元を検証して、セキュリティへの影響を検討します。信頼できる MCP サーバーのみを使い、機密リソースや操作へのアクセス許可には注意してください。

## MCP の設定を確認する

`.vscode/mcp.json` ファイルで、この VS Code ワークスペースで利用する MCP サーバーを設定します。

1. Codespace で `.vscode/mcp.json` を開きます。
2. 次のように `github` サーバーが設定済みであることを確認します。

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       }
     }
   }
   ```

この `github` エントリはプロジェクト テンプレートに含まれているため、前の演習で Copilot が issue のバックログを読み取れました。[リモート GitHub MCP サーバー][remote-github-mcp-server]を使っているため、ローカルへのインストールは不要です。VS Code は HTTP で接続し、Copilot がツールを初めて使うときに GitHub で認証します。

## Playwright MCP サーバーを追加する

次に 2 つ目のサーバーを追加します。[Playwright MCP サーバー][playwright-mcp-server]を使うと Copilot がブラウザーを操作できるため、機能のテストに適しています。

1. `.vscode/mcp.json` で `github` の隣に `playwright` エントリを追加し、ファイルを次のようにします。

   ```json
   {
     "servers": {
       "github": {
         "type": "http",
         "url": "https://api.githubcopilot.com/mcp/"
       },
       "playwright": {
         "command": "npx",
         "args": ["@playwright/mcp@latest", "--headless"]
       }
     }
   }
   ```

2. ファイルを保存します。

リモートの `github` サーバーとは異なり、`playwright` は**ローカル** サーバーです。VS Code は `npx @playwright/mcp@latest` を実行して起動します。`--headless` フラグを指定すると、ブラウザーを画面に表示せずに実行できます。デスクトップ環境がない Codespace では、この設定が必要です。

> [!NOTE]
> Tailspin Toys ではすでにエンドツーエンド テストに Playwright を使っているため、通常はブラウザーがインストール済みです。後で Copilot がブラウザーがないと報告した場合は、`npx playwright install chromium` を実行するよう依頼して、もう一度試します。

## サーバーを起動して信頼する

VS Code は MCP サーバーを**必要に応じて起動**します。Copilot がサーバーのツールを初めて使うとき、VS Code が起動し、サーバーを信頼するか確認します。

1. `.vscode/mcp.json` の `playwright` エントリの上に **Start** が表示されます。選択してサーバーを起動し、設定が正しいことを確認します。
2. サーバーを信頼するか確認されたら、設定を確認して信頼することを選び、サーバーを起動します。

手動での起動は任意です。ここで起動しなくても、次の手順で Copilot がツールを使うときに、VS Code がサーバーを起動して信頼を確認します。

## 絞り込み機能をテストする

[Playwright MCP サーバー][playwright-mcp-server]を使うと、Copilot が実際のブラウザーを操作できます。開発者がアプリを手動で操作する代わりに、エージェントがページを開き、移動し、絞り込みを適用して結果を読み取り、観察した内容を要約できます。会話を離れずに機能を確認できます。

Playwright MCP サーバーは、スクリーンショットではなくページの[アクセシビリティ ツリー][playwright-mcp-server]を使います。エージェントはボタン、リンク、リスト項目などのラベル付き要素を扱います。これは支援技術と同じように構造化された情報を使うため、簡単な機能確認がアクセシビリティの簡易チェックにもなります。

サーバーを接続してアプリを実行した状態で、作成した絞り込み機能をテストするよう Copilot に依頼します。

1. Copilot Chat に次のプロンプトを送信します。

   ```text
   Using the Playwright MCP server, open a browser to the running app at http://localhost:4321 and verify the new game filtering feature:

   1. Go to the games page and note how many games are listed.
   2. Apply a category filter and confirm the list updates to only show games in that category.
   3. Clear it, then apply a publisher filter and confirm the list updates to that publisher.
   4. Combine a category and a publisher filter and confirm the results respect both.

   Report what you observe at each step, and call out anything that does not behave as expected.
   ```

Copilot は Playwright MCP サーバーを通じてブラウザーを起動し、手順に沿って操作した結果を報告します。issue の受け入れ条件に照らして要約を読みます。問題があれば、プルリクエストを開く前に追加の質問をするか、コード修正を依頼します。

> [!NOTE]
> テストするには、アプリが `http://localhost:4321` で実行されている必要があります。開発サーバーを停止した場合は、プロンプトを送信する前に起動します。Copilot が Playwright MCP サーバーを初めて使うとき、ブラウザーのダウンロードが必要な場合があります。ブラウザーがないと報告されたら、`npx playwright install chromium` を実行するよう依頼して、もう一度試します。

[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp

## ブランチを公開してプルリクエストを作成する

機能の動作を確認したので、チームのレビュー用にプルリクエスト (PR) を作成します。まず `filtering-vscode` ブランチを公開します。

1. Codespace の **Source Control** パネルに移動し、Copilot が変更した内容を確認します。
2. **+** アイコンを選択して変更を stage します。
3. **Sparkle** ボタンを使ってコミット メッセージを生成します。

   ![変更内容を表示する Source Control パネル](../../../_images/ex3-source-control-changes.png)

4. **Publish** を選択してブランチをリポジトリに push します。

## プルリクエストを作成する

PR は github.com や GitHub コマンド ライン インターフェイス (CLI) などで作成できます。ここでは GitHub Copilot に依頼し、関連する issue を見つけて PR に関連付けます。

1. Copilot Chat パネルに移動し、**New Chat** を選択して新しいセッションを開始します。
2. エージェント ドロップダウンで **Agent** が選択され、Copilot が GitHub ツールを使えることを確認します。
3. 次のプロンプトを送信して PR を作成します。

   ```plaintext
   Find the issue in the repo related to filtering by category and publisher. Create a new pull request for the current branch, and associate it with the correct issue.
   ```

4. Copilot が情報を集めて操作を行うために **Continue** を求めたら選択します。GitHub ツールを初めて使う場合は GitHub への認証を求められることがあります。画面の案内に従います。
5. Copilot が issue を検索して該当のものを見つけ、PR を作成する様子を確認します。
6. Copilot が生成したリンクを選択して PR を確認します。**まだマージしないでください。**

## まとめと次のステップ

この演習では次のことを行いました。

- Model Context Protocol (MCP) と MCP サーバーが Copilot にツールを追加する仕組みを学びました。
- Playwright MCP サーバーをワークスペースに追加しました。
- 出荷前に、ブラウザーで絞り込み機能を手動テストするよう Copilot に依頼しました。
- ブランチを公開し、絞り込み作業の PR を作成しました。

MCP サーバーを使って機能を**テスト**しました。MCP は Copilot を拡張する方法の 1 つです。次は、アクセシビリティのような特定の作業を効率化する[カスタム エージェントを作成します][next-lesson]。

## リソース

- [MCP とは何か、なぜ話題になっているのか][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [GitHub MCP Server][github-mcp-server]
- [GitHub MCP Registry][mcp-registry]
- [VS Code の MCP サーバー][vscode-mcp-config]

[previous-lesson]: ../2-agent-mode/
[next-lesson]: ../4-custom-agents/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[github-mcp-server]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[remote-github-mcp-server]: https://github.blog/changelog/2025-06-12-remote-github-mcp-server-is-now-available-in-public-preview/
[vscode-mcp-config]: https://code.visualstudio.com/docs/agents/reference/mcp-configuration
