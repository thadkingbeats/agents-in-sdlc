---
title: "レッスン 8 - 機能 PR の作成とマージ"
description: "絞り込み機能、指示、スキルの更新、QA プロファイル、テストをレビューし、プルリクエスト (PR) を作成して Agent Merge を使います。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

絞り込み機能の実装、指示の更新、スキルの更新、品質保証 (QA) プロファイル、テストは、すべて 1 つのブランチに保存されています。まとめてレビューし、プルリクエストを作成します。星評価のプルリクエスト (PR) は手動でマージしましたが、今回は **Agent Merge** に処理を任せます。

> [!NOTE]
> 通常は機能、指示の更新、スキルの更新、QA エージェントを複数の PR に分けます。ワークショップを簡潔にするため、絞り込み機能と品質ワークフロー全体を 1 つの会話とブランチで進め、この PR にまとめます。

このレッスンでは、次のことを行います。

- Agent Merge とマージ ライフサイクルの自動化について学びます。
- 機能全体の変更と検証の証拠を確認します。
- 絞り込み機能の PR を作成します。
- レビュー後にのみ Agent Merge を有効にし、PR がマージされたことを確認します。

## シナリオ

絞り込み機能の開発では、Copilot を使って計画、実装、検証を行いました。Tailspin Toys では、マージを許可する権限を開発者が保持したまま、残りの PR 作業を自動化したいと考えています。

## Agent Merge とは

**Agent Merge** は、プルリクエストを取り込むために必要な残りの作業を自動化します。有効にすると、失敗した継続的インテグレーション (CI) チェックの修正、レビュー コメントへの対応、必要に応じたリベースなど、PR を妨げている問題を Copilot が処理します。リポジトリで許可されていれば、最後に GitHub の自動マージを有効にします。

これまでは開発者自身が **Merge pull request** を選択しました。Agent Merge に任せることもできますが、有効化する前に作業をレビューし、準備ができていることを確認してください。

## Agent Merge で PR を管理する

コードを作成できたので、まとめてレビューし、PR を作成して、残りの処理を Agent Merge に任せます。

1. Codespace に戻ります。
2. `/agent` を入力してエージェント ダイアログを開きます。
3. 選択肢から **Default** を選び、<kbd>Enter</kbd> を押します。
4. `/pr create` コマンドを使って PR を作成します。
5. PR の変更ファイルと検証結果をレビューし、マージの準備ができていることを確認します。
6. `/pr agentmerge` を使って Agent Merge を有効にします。
7. Copilot が PR の CI を監視します。すべて成功すると、マージが実行されます。
8. Copilot から「PR #14 was squash-merged successfully.」のようなメッセージが表示されたことを確認します。

> [!IMPORTANT]
> Agent Merge は、必須の承認、ブランチ保護、マージ キュー、リポジトリ設定、権限不足を回避しません。処理がブロックされた場合は報告された理由を確認し、リポジトリで許可されていればレビュー後に手動でマージします。

## まとめと次のステップ

コード生成、テストと検証、プルリクエストの処理など、開発プロセスの一部を自動化しました。このレッスンでは次のことを行いました。

- Agent Merge とマージ ライフサイクルの自動化について学びました。
- 機能全体の変更と検証の証拠を確認しました。
- 絞り込み PR を作成しました。
- レビュー後に Agent Merge を有効にし、PR のマージを確認しました。

次は、コンテキスト、モデル、共有、任意のクラウド委任に使える[便利な Copilot CLI スラッシュ コマンド][next-lesson]を確認します。

## リソース

- [Copilot CLI でプルリクエストを管理する][manage-prs]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
