---
slug: ja-jp/real-world-development/app
title: "GitHub Copilot app"
authors:
  - geektrainer
lastUpdated: 2026-10-22
---

**[GitHub Copilot app](https://docs.github.com/copilot/concepts/agents/github-copilot-app)** は Copilot CLI を基盤とするデスクトップ アプリケーションです。エージェントを使った開発を、集中して作業できる単一のワークスペースにまとめます。並行エージェント セッション、切り替え可能なセッション モード、共有 Canvas、GitHub issue とプルリクエストのネイティブな管理機能を備えています。さらに **Agent Merge** を使うと、リベース、レビュー フィードバック、継続的インテグレーション (CI) の修正、マージまでプルリクエストを進められます。

このワークショップでは、Tailspin Toys の開発を一連の流れで進めます。

1. プロジェクトを準備し、アプリをインストールしてリポジトリを接続し、ワークスペースと登録済みのバックログを確認します。
2. 星評価の小さな変更を加え、ブラウザーで確認して、最初のプルリクエスト (PR) を手動でマージします。
3. 絞り込み issue から始め、**Plan** モードで方針を定め、**Autopilot** モードで実装し、**Interactive** モードでレビューします。
4. リポジトリの指示を更新し、絞り込み機能の作業に適用します。
5. 既存の `quality-checks` スキルをカスタマイズし、プロジェクトのチェックを実行します。
6. Playwright Model Context Protocol (MCP) サーバーを追加し、ブラウザーで絞り込み機能を確認します。
7. 品質保証 (QA) カスタム エージェントを作成し、要件、テスト範囲、検証の証拠をレビューします。
8. 絞り込み機能全体の変更を確認し、2 つ目の PR に Agent Merge を使います。
9. Canvas が使えることを確認し、Database Explorer を使った後、リポジトリに保存するトリアージ Canvas を作成してテストします。必要な機能を利用できない場合は、ブロッカーを記録し、読み取り専用の代替手段を使うか、まとめに進みます。

ワークショップを簡潔にするため、作成する PR は 2 つです。1 つ目は星評価、2 つ目は指示の更新、スキルの更新、QA プロファイル、テストを含む絞り込み機能です。各作業は更新済みの `main` から始めます。絞り込みと品質のワークフローでは、1 つのセッション、worktree、ブランチを共有し、各ツールを学ぶ間もそれまでの作業を活用します。最後の Canvas 演習も同じセッションで行い、PR ワークフローを繰り返さずに共有スペースの作成とテストに集中します。

## レッスン

| レッスン | トピック | 説明 |
|--------|-------|-------------|
| [0. 前提条件][ex0] | セットアップ | Node.js をインストールし、Tailspin Toys プロジェクトの自分用コピーを作成します |
| [1. Copilot app をインストールする][ex1] | セットアップ | アプリをインストールしてプロジェクトに接続し、ワークスペースを確認します |
| [2. 星評価を追加する: 小さな改善][ex2] | 最初の変更 | 既存の評価と未評価時の表示を追加し、1 つ目の PR をマージします |
| [3. エージェント モード: Plan と Autopilot][ex3] | エージェント モード | issue に基づいて機能を計画し、Autopilot で構築して、Interactive モードでレビューします |
| [4. カスタム指示で Copilot を導く][ex4] | コンテキスト | 指示を確認・更新し、絞り込み機能に適用します |
| [5. quality-checks スキルのカスタマイズと使用][ex5] | 繰り返し実行できるチェック | 既存のスキルを確認し、レポート形式を変更して実行します |
| [6. Playwright MCP で機能を検証する][ex6] | ブラウザーでの確認 | Customize から MCP を設定し、絞り込みの動作を確認します |
| [7. QA エージェントの作成と使用][ex7] | 要件とテスト範囲 | 専門家プロファイルを作成して選び、最終検証の証拠を集めます |
| [8. 機能 PR の作成とマージ][ex8] | レビューとマージ | 絞り込み、指示、スキル、QA プロファイル、テストをレビューし、2 つ目の PR に Agent Merge を使います |
| [9. Canvas を確認して作成する][ex9] | コラボレーション | Database Explorer を使い、リポジトリに保存するトリアージ Canvas を作成してテストします |
| [10. 振り返りと次のステップ][ex10] | まとめ | ワークフロー、成果物、追加リソースを確認します |

## 前提条件

このワークショップを始める前に、次のものを用意してください。

- [ ] 有効な **Copilot Student、Pro、Pro+、Business、Enterprise** プランがある GitHub アカウント
- [ ] **macOS、Linux、Windows** のいずれかを実行するコンピューター
- [ ] コンピューターに[インストールされた Git][install-git]

> [!TIP]
> 有料プランを利用していない場合、認証済みの学生は [GitHub Education][callout-student-plan-education] を通じて GitHub Copilot を無料で利用できます。**Copilot Student** プランには、このワークショップで使うエージェント、MCP、コードレビュー、Copilot CLI の機能が含まれているため、どのハーネスも完了できます。

> [!NOTE]
> Copilot app は Codespace ではなく自分のコンピューターで動作します。そのため、[前提条件の演習][ex0]では、アプリのインストール前に Node.js をインストールし、プロジェクトの自分用コピーを作成します。

> [!NOTE]
> Copilot Business または Copilot Enterprise を使う場合、管理者が **GitHub Copilot app** ポリシーを有効にしておく必要があります。このポリシーは Copilot CLI のポリシーとは別です。

## はじめる

**[前提条件から始める →][ex0]**

[ex0]: 0-prerequisites/
[ex1]: 1-install-copilot-app/
[ex2]: 2-add-star-rating/
[ex3]: 3-agent-modes/
[ex4]: 4-custom-instructions/
[ex5]: 5-agent-skills/
[ex6]: 6-mcp-playwright/
[ex7]: 7-qa-agent/
[ex8]: 8-create-pull-request/
[ex9]: 9-canvases/
[ex10]: 10-review/
[install-git]: https://github.com/git-guides/install-git
[callout-student-plan-education]: https://github.com/education/students
