---
title: "レッスン 10 - 振り返りと次のステップ"
description: "Copilot CLI のワークフロー、2 つのプルリクエスト、再利用可能なカスタマイズ、追加リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

GitHub Copilot CLI を使い、Tailspin Toys の開発を一連の流れで進めました。次のことを行いました。

- Codespace を準備し、Copilot CLI をインストールして、プロジェクトを確認し、登録済みの絞り込み issue を見つけました。
- 星評価を追加し、転送ブラウザーで結果を確認して、最初のプルリクエスト (PR) を手動でマージしました。
- 絞り込み issue から始めて Plan モードで方針を定め、Autopilot モードで実装し、Interactive モードでレビューしました。
- カスタム指示でエージェントを導き、既存の `quality-checks` スキルをカスタマイズして、単体テスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーで絞り込み機能を確認しました。
- 品質保証 (QA) カスタム エージェントを作成して選び、要件、テスト範囲、スキルの結果、ブラウザー上の証拠を評価しました。
- 絞り込み機能全体の変更をレビューし、絞り込み PR に Agent Merge を許可しました。
- コンテキスト、モデル、共有、任意のクラウド委任に使うスラッシュ コマンドを確認しました。

## 作成したもの

ワークショップには、更新された `main` からそれぞれ作成する 2 つの PR があります。

1. **星評価:** 既存の `starRating` と未評価状態をゲームカードに表示します。
2. **絞り込みと品質のワークフロー:** 絞り込みを実装し、指示を更新して機能に適用し、`quality-checks` のレポートをカスタマイズし、QA プロファイルと関連テストを追加します。

絞り込みの計画から PR 作成までは、同じ会話とブランチを使いました。ワークショップを簡潔にするため、作業を 1 つの PR にまとめています。

## 検証の種類

自動テスト、自分で行うブラウザー確認、MCP を介した Copilot のブラウザー操作という複数の方法でコードを確認しました。`quality-checks` スキルは単体テスト、lint、型チェックを実行し、カスタマイズした形式で結果を報告しました。QA はその結果と、要件およびテスト範囲のレビューをまとめて PR の確認を支援しました。

追加するテストは、実際の不足を補うものである必要があります。QA の実行時に追加テストが不要と判断される場合もあります。マージを許可する前に、コードと根拠を確認してください。変更後は、影響を受ける検証結果も更新します。

## ベスト プラクティス

Copilot に与えるコンテキストとツールが、作業結果に影響します。このワークショップでは、指示を更新し、スキルをカスタマイズし、QA プロファイルを作成し、MCP サーバーを設定しました。チームのニーズに合わせて、これらのカスタマイズを会話間で再利用し、調整してください。指示は標準を設定し、スキルは繰り返し実行する作業を記述し、カスタム エージェントは専門家の役割を定義し、MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果を確認してください。

タスクに応じて**モードとモデル**を選びます。実装前に方針を考えるには **Plan**、範囲を絞った変更を確認しながら進めるには **Interactive**、明確に定義された作業には **Autopilot** を使います。定型的な編集には高速なモデルを、複雑な作業には高性能なモデルを選びます。

ツールと同様に、コンテキストも重要です。何を作るのか、なぜ必要か、どのように進めるかを明確に説明すると、結果が大きく変わります。

## さらに試す

基本的なワークフローを学びました。Copilot CLI には、ほかにも次のような機能があります。

- `/review` でコードレビュー エージェントに変更を分析してもらいます。
- `/rubber-duck` で問題を相談し、別の視点を得ます。
- `/fleet` で独立したサブタスクを並行して調整します。
- `/worktree` で別のタスクを分離します。
- `/delegate` で Copilot cloud agent にタスクを送信します。

## 次のステップ

どのツールでも、上達するには使い続けることが一番です。本番コード、趣味のコード、作ろうと思いながら何年も手を付けていない小さなアプリなどで活用してください。チームと学びを共有し、チームからも学びましょう。ドキュメントも引き続き確認してください。

ターミナルから Tailspin Toys を拡張するには、任意の [Foundry Backer Concierge シリーズ][foundry]に進みます。別の作業環境と比較するには、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、または [Copilot cloud agent ワークショップ][cloud]を確認してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
- [Copilot CLI でプルリクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
