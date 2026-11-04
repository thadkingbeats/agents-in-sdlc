---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

前の演習では、Copilot cloud agent にユーザー エクスペリエンスの改善や機能追加に関する 3 つのタスクを依頼しました。cloud agent は非同期かつ自律的に作業しますが、タスクを監視することも重要です。

GitHub の[エージェント ページ][agents-page]など、cloud agent に割り当てたタスクを管理するツールがあります。このミッション コントロールでは、オープンなプルリクエスト (PR) があるすべてのエージェント タスクを確認できます。Model Context Protocol (MCP) サーバーの設定など、処理内容を調べたり、実行中のセッションに追加の指示を送ったりできます。

このレッスンでは、次のことを行います。

- エージェント ページで cloud agent のタスクを監視します。
- 実行中のセッションに指示を送り、機能追加を依頼します。

## シナリオ

チームは、ハイ コントラスト モードに加えてライト モードも追加したいと考えています。サイトのスタイルと切り替え機能をすでに変更中なので、追加するのが自然です。エージェントがライト モードとハイ コントラスト モードの両方を実装するよう、作業を案内します。

## Copilot cloud agent のタスクを確認する

Copilot cloud agent に割り当てたすべてのタスクの現在の状態を確認します。

1. [Copilot agents ページ](https://github.com/copilot/agents)に移動します。
2. メイン ペインと左ペインのタスク一覧を確認します。ドキュメントの更新、ゲームを変更する API の生成、Web サイトへのハイ コントラスト モード追加など、Copilot に割り当てたタスクが表示されます。
3. 実行中のタスクを選択し、Copilot が行った操作を確認します。リポジトリのチェックアウト、作業環境の作成、MCP サーバーの設定、タスク完了に向けた各種手順などが含まれます。

> [!NOTE]
> 表示される手順は、Copilot の作業状態や進め方によって異なります。

4. 右側に表示される PR ペインも確認します。ここから PR と変更ファイルを確認し、さらに監視できます。

## Cloud agent に指示を送る

実行中のタスクを確認したので、ハイ コントラスト モードの作業中にライト モードも追加するよう依頼します。

1. ハイ コントラスト モードを追加するセッションを選択します。エージェントが付けた名前や現在の作業状態によって、タイトルは異なります。

   ![ミッション コントロールに表示されたアクセシビリティ セッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが完了して作業が始まったことを示すメッセージが表示されるまで、数分間セッションを確認します。
3. **Steer active session while Copilot is working** ダイアログに、次のプロンプトを入力します。

   ```plaintext
   While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
   ```

   ![Copilot が作業中のセッションに指示するダイアログが強調表示されたエージェント ページ](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot がプロンプトを受け取り、作業計画に組み込むことを確認します。

## Copilot に作業を続けてもらう

Copilot は、メッセージを送信した時点で作業していた手順を終えてから、新しい依頼を取り込みます。

作業には数分かかります。その間に、これまでに学んだことを振り返ってください。

## まとめと次のステップ

GitHub Copilot cloud agent の監視と案内に使う中心的な場所である、Copilot agents ページを確認しました。ここでは、進行中と完了済みのタスクを追跡し、作業内容をレビューし、実行中のタスクに追加の指示を送れます。

このレッスンでは、次のことを行いました。

- ミッション コントロールとエージェント ページで cloud agent のタスクを監視しました。
- 実行中のセッションに指示を送り、機能追加を依頼しました。

Copilot がアクセシビリティ機能を実装している間に、[Copilot が作成したプルリクエストを改善します][next-lesson]。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタム エージェントについて][custom-agents]

---

| [← 前のレッスン: カスタム エージェント][previous-lesson] | [次のレッスン: Copilot の作業を反復して改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
