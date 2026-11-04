---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

多くの組織は、未解決のセキュリティ問題、更新が必要なレガシー コード、実装する時間がなくバックログに残った機能要望など、技術的負債に直面しています。GitHub Copilot cloud agent は、コードの更新や機能追加などを自律的に実行できます。作業が完了すると、人がレビューできるドラフトのプルリクエスト (PR) を作成します。時間のかかる作業を任せることで、開発者はより大きな課題に集中できます。

Copilot cloud agent では、次のことを確認します。

- コード生成環境をカスタマイズする。
- 操作を安全に行う。
- 範囲を明確にした issue の重要性を理解する。
- issue を Copilot に割り当てる。

## シナリオ

Tailspin Toys には解決したい技術的負債があります。最初のサイトを開発した委託先は、ドキュメントをほとんど残していません。まず、アプリケーションのエクスポート関数すべてに TSDoc の doc comment を追加します。

また、デザイン チームはゲームを見つけやすくしたいと考えています。各ゲーム詳細ページに、同じカテゴリに属する関連ゲームを表示し、閲覧を続けられるようにします。洗練された実装はまだ必要なく、ユーザー エクスペリエンス (UX) の受け入れテストに使えるものを求めています。この作業は現在ブロックされていますが、より優先度の高い issue がほかにあります。

どちらも優先順位が下がりやすいタスクの例です。Copilot cloud agent に割り当てることで、開発者が別の作業を進めている間に非同期で処理できます。完了後に戻って、期待どおりか確認できます。

## GitHub Copilot cloud agent とは

[GitHub Copilot cloud agent][copilot-agents] は、人間の開発者と同様にバックグラウンドでタスクを実行できます。[GitHub issue を Copilot に割り当てる][assign-issue]など、複数の方法で作業を依頼できます。割り当てると、Copilot は進捗を追跡するドラフト PR を作成し、環境を設定して、タスクに取りかかります。実行中または完了後にセッションを確認できます。提案された解決策のレビュー準備ができると、PR で開発者に通知します。

## 範囲を明確にした指示の重要性

GitHub Copilot に魔法はありません。考える作業を省略できるわけではありません。一見簡単な操作にも複雑さが隠れています。[Copilot cloud agent に依頼するタスクの範囲を慎重に決めてください][cloud-agent-best-practices]。AI ペア プログラマーとして扱い、段階的に進め、学び、試し、適応させます。生成 AI を導入しても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム指示

前の演習ではカスタム指示と Copilot への影響を確認しました。カスタム指示の演習をすでに完了していれば、`.github/copilot-instructions.md` の動作を確認したはずです。まだの場合は、cloud agent に作業を割り当てる前に、このリポジトリに含まれる指示ファイルを読み取り専用で確認してください。後で影響を確認できます。

リポジトリの GitHub Web UI または起動中の Codespace で、次のファイルを開きます。

- `.github/copilot-instructions.md` — **Code standards** セクション、特に TypeScript の規約と TSDoc の doc comment に関する要件を確認します。
- `.github/instructions/unit-tests.instructions.md` — `**/*.test.ts` ファイルに適用される `applyTo` frontmatter を確認します。

次のセクションで `Code lacks documentation` issue を cloud agent に割り当てます。生成された PR に、これらの指示に由来する TSDoc の doc comment、TypeScript の規約、コメント ヘッダーがあるか確認してください。後の演習で PR をレビューするときに、改めて取り上げます。

## Copilot cloud agent の開発環境を設定する

コード作成には、通常、適切な環境と初期化スクリプトが必要です。Copilot にタスクを割り当てる場合も同様で、cloud agent はソフトウェア エンジニアのように作業します。

Cloud agent は [GitHub Actions][github-actions] を使って作業環境を準備します。`.github/workflows/copilot-setup-steps.yml` に設定した[セットアップ ワークフロー][setup-workflow]を実行し、必要な開発ツールや依存関係をインストールできます。ラボの流れを円滑にするため、あらかじめ設定されています。単一 Astro アプリ用に Node.js、プロジェクト依存関係、エンドツーエンド テスト用のブラウザー バイナリ、マイグレーションとシードを適用した SQLite データベースを用意します。

```yaml
name: "Copilot Setup Steps"

# リポジトリの "Actions" タブからセットアップ手順をテストできます
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # 必要な権限だけを設定します。Copilot は自身の操作用トークンを受け取ります。
    permissions:
      # セットアップ手順の一部としてリポジトリをクローンする場合 (依存関係のインストールなど) は、contents: read が必要です。クローンしない場合は、手順の完了後に Copilot が自動的にクローンします。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / アプリのセットアップ - Node.js (アプリ全体は Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # アプリのビルドとテスト用に、ローカル SQLite データベースをマイグレーションしてシードします。
      - name: Set up the database
        run: npm run db:setup
```

このファイルは一般的な GitHub ワークフローと同じ形式ですが、いくつか重要な点があります。

- `copilot-setup-steps` という 1 つのジョブがあります。このジョブは、Copilot が PR の作業を始める前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーを使うと、リポジトリの **Actions** タブからワークフローを手動実行できます。Copilot に実行させる前に、ワークフローが成功するか確認できます。

## ドキュメントを追加する

ドキュメントの重要性は広く認識されていますが、情報が古かったり、まったくなかったりするプロジェクトは少なくありません。これは対応されないままになりやすい技術的負債であり、生産性を下げ、コードベースの保守や新しい開発者の参加を難しくします。Copilot はドキュメント作成を支援できるため、cloud agent に依頼するのに適した作業です。Copilot がバックグラウンドでドキュメントを生成します。後の演習で結果を確認します。

1. 新しいブラウザー タブで github.com のリポジトリに移動します。
2. **Issues** タブを選択します。
3. **New issue** を選択して issue 作成ダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次の内容を入力します。

   ```plaintext
   Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
   ```

7. **Create** を選択して issue を作成します。
8. 右側にある **Assign to Copilot** を選択して割り当てダイアログを開きます。

   ![issue への Copilot の割り当て](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。
10. **Pull Requests** タブを選択します。
11. `[WIP]: Code lacks documentation` のようなタイトルの新しい PR を開きます。一覧に PR がない場合は、少し待ってからブラウザーを更新します。
12. 数分後、Copilot が TODO リストを作成したことを確認します。

> [!NOTE]
> Copilot が PR に TODO リストを表示するまで数分かかる場合があります。前述のワークフローを実行して環境を作り、プロジェクトを分析して、問題への最適な対応方法を判断しています。

13. リストを確認し、実行するタスクを読みます。
14. PR のタイムラインを下にスクロールし、Copilot が issue の作業を始めたことを示す更新を確認します。
15. **View session** ボタンを選択します。

   ![Copilot セッションの表示](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 更新された表示を確認するために、ブラウザーを更新する必要がある場合があります。

16. ライブ セッションをスクロールし、Copilot がどのように問題を解決しているか確認します。コードを調べて状態を理解し、計画を考えて判断し、コードを作成する様子を確認できます。

完了まで数分かかることがあります。Copilot cloud agent の主な利点は、タスクを非同期で進め、開発者が別の作業に集中できることです。この利点を活用するため、もう 1 つタスクを割り当ててから、アプリの機能を追加する作業に移ります。

## ゲーム詳細ページに関連ゲームを追加する

GitHub Copilot cloud agent の利点の 1 つは、作業を分担できることです。デザイン チーム向けに関連ゲームを追加する作業に時間がかからないとしても、その時間を別の作業に使えます。Copilot cloud agent に依頼します。

1. github.com のリポジトリに戻ります。
2. **Issues** タブを選択します。
3. **New issue** を選択して issue 作成ダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次の内容を入力します。

   ```markdown
   We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
   ```

7. **Create** を選択して issue を作成します。
8. 右側にある **Assign to Copilot** を選択して割り当てダイアログを開きます。

   ![issue への Copilot の割り当て](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

まもなく、Copilot が作業を始めたことを示す 👀 が issue の最初のコメントに表示されます。

![Copilot が issue の作業中であることを示す目の絵文字](../../../_images/ex4-issue-eyes-emoji.png)

Copilot は 2 つ目の依頼にも取り組んでいます。Copilot cloud agent はソフトウェア エンジニアのように作業するため、常時監視する必要はありません。完了後にレビューします。次はカスタム エージェントの作成と使用を確認します。

## まとめと次のステップ

[GitHub Copilot cloud agent][copilot-agents] を確認しました。issue を Copilot に割り当て、非同期に作業させられます。技術的負債への対応、新機能の作成、別のフレームワークへのコード移行などを依頼できます。

この演習では次のことを行いました。

- コード生成環境をカスタマイズしました。
- 操作を安全に行う方法を確認しました。
- 範囲を明確にした issue の重要性を学びました。
- issue を Copilot に割り当てました。

Cloud agent がバックグラウンドで作業している間に、次はカスタム エージェントの作成と使用に進みます。[Copilot cloud agent は MCP サーバーも使用でき][cloud-agent-mcp]、前のモジュールで確認したカスタム指示も利用できます。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent セットアップ ワークフローのベスト プラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタム エージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
[github-actions]: https://docs.github.com/actions
