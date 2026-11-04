---
slug: ja-jp/real-world-development/vscode
title: "Visual Studio Code"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

VS Code の **[GitHub Copilot Chat](https://code.visualstudio.com/docs/copilot/chat/copilot-chat)** を使うと、普段使っているコード エディターで GitHub Copilot を利用できます。Visual Studio Code と GitHub Codespaces で agent mode の Copilot Chat を使い、Model Context Protocol (MCP) で外部ツールに接続し、カスタム エージェントを活用します。統合開発環境 (IDE) を離れずに作業でき、Copilot はファイル、ターミナル、問題の全体を確認できます。

まずカスタム指示を追加し、Copilot がそれに従うことを確認します。次に agent mode を使い、ユーザー インターフェイス (UI)、データ レイヤー、テストをまたぐ絞り込み機能を構築します。続いて Playwright MCP サーバーを接続し、プルリクエストを開く前に Copilot にブラウザーを操作させて機能をテストします。最後に、アクセシビリティ作業用のカスタム エージェントを確認して使い、エディターを離れずに Copilot の変更を監視、案内、改善します。

## 演習

| 演習 | トピック | 説明 |
|----------|-------|-------------|
| [0. 前提条件][ex0] | セットアップ | リポジトリと Codespace を作成します |
| [1. カスタム指示][ex1] | コンテキスト | VS Code でカスタム指示を追加して確認します |
| [2. Agent Mode][ex2] | コード生成 | agent mode で絞り込み機能を構築します |
| [3. Playwright MCP][ex3] | 外部ツール | Playwright MCP サーバーを使ってブラウザーで機能をテストします |
| [4. カスタム エージェント][ex4] | 専門エージェント | カスタム エージェントを確認して使います |
| [5. エージェントの管理][ex5] | 監視 | エージェント セッションを監視して案内します |
| [6. 反復][ex6] | レビュー | Copilot の作業をローカルでレビューし、次の手順を選びます |
| [任意: Foundry を組み込む][foundry-toolkit] | AI エージェント | VS Code と Foundry Toolkit を使う 3 つのモジュールでモデルを準備し、エージェントをデプロイしてサイトに接続します |

## 前提条件

このワークショップに参加する前に、次のものを用意してください。

- [ ] 有効な **Copilot Student、Pro、Pro+、Business、Enterprise** プランがある GitHub アカウント
- [ ] GitHub Codespaces へのアクセス

> [!TIP]
> 有料プランを利用していない場合、認証済みの学生は [GitHub Education][callout-student-plan-education] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使うエージェント、MCP、コードレビュー、Copilot CLI の機能が含まれています。

[callout-student-plan-education]: https://github.com/education/students

## はじめる

**[演習 0: 前提条件から始める →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-custom-instructions/
[ex2]: 2-agent-mode/
[ex3]: 3-mcp/
[ex4]: 4-custom-agents/
[ex5]: 5-managing-agents/
[ex6]: 6-iterating/
[foundry-toolkit]: 7-foundry-toolkit/
