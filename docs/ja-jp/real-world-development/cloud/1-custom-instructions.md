---
title: "演習 1 - カスタム指示 (Cloud agent)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を使うときは、コンテキストが重要です。タスクを特定の方法で進める必要がある場合や、Copilot に知っておいてほしい背景情報がある場合は、そのコンテキストを参照できるようにします。[指示ファイル][instruction-files]を使うと、Copilot が実行する内容だけでなく、その進め方も伝えられます。

この演習では、次のことを行います。

- リポジトリのカスタム指示とパス単位の指示ファイルを使って、プロジェクト固有のコンテキスト、コーディング ガイドライン、ドキュメント標準が Copilot に伝わる仕組みを確認します。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加します。

> [!NOTE]
> VS Code および CLI ハーネスとは異なり、この演習では変更前後のプロンプトを比較しません。Copilot cloud agent は GitHub issue を非同期で処理するため、影響をリアルタイムに並べて示すのが難しいためです。後続の演習で cloud agent が作成するプルリクエストをレビューするときに、指示ファイルの影響を確認できます。

## 指示ファイル

### シナリオ

Tailspin Toys には開発プラクティスに関するガイドラインと要件があります。たとえば、次のとおりです。

- データ レイヤーには必ず単体テストを用意します。
- UI はダーク モードにし、現代的な印象にします。
- コード内のドキュメントには TSDoc の doc comment を使います。
- 各ファイルの先頭に、ファイルの役割を説明するコメント ブロックを置きます。

指示ファイルを使い、これらのプラクティスに沿ってタスクを実行するための情報を Copilot に提供します。

### カスタム指示

カスタム指示は、コンテキストや設定を Copilot に提供し、コーディング スタイルや要件を理解させます。好みのコーディング規約、ライブラリ、追加したいコメントの種類などを指定できます。リポジトリ全体に対する指示も、特定のファイル種別に対するタスク レベルの指示も作成できます。

指示ファイルは 2 種類あります。

- `.github/copilot-instructions.md` は、リポジトリへの**すべての**リクエストで Copilot に送られる指示ファイルです。技術スタック、作成中のものの概要、ベスト プラクティス、全体に適用するガイダンスなど、プロジェクト レベルの情報を含めます。
- `.github/instructions/*.instructions.md` は、特定のタスクやファイル種別に適用できます。TypeScript や Astro などの言語、UI コンポーネントの作成、単体テストの追加などに関するガイダンスに使います。

> [!NOTE]
> 統合開発環境 (IDE) では、指示ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、コード生成時にリポジトリ レベルの指示ファイルと、`applyTo` frontmatter を持つ `*.instructions.md` ファイルの両方を使います。
>
> Copilot は [ほかの標準に基づく指示ファイル][custom-instructions-support]もサポートしており、AGENTS.md や CLAUDE.md も利用できます。

### 指示ファイルを管理するためのベスト プラクティス

指示ファイルの作成を詳しく扱うことは、このワークショップの範囲外です。サンプル プロジェクトの例は、一般的な方法を示しています。

- `copilot-instructions.md` には、作成中のものの説明、プロジェクト構造、全体的なコーディング標準など、プロジェクト レベルのガイダンスを記述します。
- `*.instructions.md` ファイルは、単体テスト、Astro コンポーネント、データ レイヤーなどのファイル種別や、特定のタスク向けに使います。
- 自然言語で明確に記述し、望ましいコードと望ましくないコードの例を示します。

指示ファイルの作成方法や AI の使い方に唯一の正解はありません。試しながら、プロジェクトに合った方法を見つけてください。

> [!TIP]
> GitHub Copilot を使うプロジェクトには、十分な指示ファイルを用意してください。このプロジェクトには [UI の更新][ui-instructions]や [Astro][astro-instructions]など、さまざまなタスク向けのファイルがあります。
>
> Copilot に指示ファイルを生成してもらうこともできます。VS Code の **Configure Chat → Generate Agent Instructions** や Copilot CLI の `/init` など、利用する環境によって方法が異なります。必要な場面で、各環境のレッスンに説明があります。
>
> テンプレートや出発点には、指示ファイル、カスタム エージェントなどのリソースを集めた [awesome-copilot][awesome-copilot] を利用できます。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトのカスタム指示ファイルを確認する

このリポジトリには、中心となる `copilot-instructions.md` と、タスク別の `*.instructions.md` ファイルがあります。エディターまたは GitHub の Web UI で確認します。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの概要に加え、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** の **GitHub Actions Workflows** のガイダンスも確認してください。これらの指示は Copilot とのあらゆるやり取りに適用されます。
3. `.github/instructions` フォルダーを開き、Astro ファイル、Drizzle データ レイヤー、テストなどの指示を確認します。
4. `.github/instructions/unit-tests.instructions.md` を開き、先頭の `applyTo` フィールドを確認します。ここでは、リポジトリ ルートからの相対 glob で対象ファイルを指定します。たとえば `**/*.test.ts` に一致する TypeScript テスト ファイルが対象です。
5. このプロジェクトの単体テスト作成に関する指示を確認します。
6. `.github/instructions/drizzle.instructions.md` を開いて末尾まで読み、`unit-tests.instructions.md` などの指示ファイルやプロジェクトの既存ファイルへのリンクを確認します。大きな指示を再利用しやすい単位に分け、コード生成時に Copilot が従う例を示せます。ここに記載されたパスは、リポジトリ ルートではなく指示ファイルからの相対パスです。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはプロジェクトのコーディング標準がありますが、コード内のドキュメントはまだ必須ではありません。次の手順で TSDoc の doc comment とファイル コメント ヘッダーのルールを追加します。

## リポジトリ標準を追加する

この演習で編集するのは、コード内に TSDoc の doc comment とファイル レベルのコメント ヘッダーを置くという、プロジェクト全体のルールです。後続の演習で issue を割り当てると、cloud agent がこの指示を使います。

編集前に作業ブランチを作成します。cloud agent は issue の対象ブランチから指示を読み取りますが、変更を整理してコミットするためにブランチを使います。

1. Codespace のターミナルで新しいブランチを作成し、切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

`.github/copilot-instructions.md` は Copilot にプロジェクト レベルの情報を提供します。コーディング標準を記述し、コード提案の質を高めます。

1. `.github/copilot-instructions.md` を開き直します。
2. 27 行目付近にある **Code formatting requirements** セクションを探します。コーディング標準は記載されていますが、コード内ドキュメントのルールはありません。
3. 既存の標準の直後に、次の Markdown 行を追加します。ファイル コメント ヘッダーと TSDoc の doc comment を Copilot に追加させます。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 指示ファイルは、全体的なガイダンスを置くリポジトリ レベル (`.github/copilot-instructions.md`) にも、特定の言語、ファイル種別、タスク向けの `*.instructions.md` にも作成できます。ここで追加する doc comment のルールのようなプロジェクト全体の標準には、リポジトリ レベルのファイルが適しています。

## 指示の更新をコミット、push、マージする

Cloud agent は issue の対象ブランチから指示ファイルを読み取ります。次の演習では Copilot に issue を割り当て、Copilot は `main` からブランチを作成します。そのため、指示の変更を `main` に取り込む必要があります。

1. 変更を stage してコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチを push します。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` へのプルリクエストを開き、マージします。次の演習で issue を割り当てたときに、cloud agent が更新した指示を読み込めるようになります。

> [!TIP]
> このワークショップで `main` に直接作業する場合は、ブランチの作成を省略して `main` にコミットしてもかまいません。実際のプロジェクトでの進め方を示すために、ここではブランチを使います。

## まとめと次のステップ

このプロジェクトの指示ファイルから Copilot がコンテキストを取得する仕組みを確認し、`.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加しました。残りのハーネスで cloud agent が作成するプルリクエストを確認すると、この標準が使われていることがわかります。

次は、[最初の issue を Copilot cloud agent に割り当てます][next-lesson]。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [Copilot のカスタム指示を書くための 5 つのヒント][copilot-instructions-five-tips]
- [Awesome Copilot — 指示ファイルなどのリソース集][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
