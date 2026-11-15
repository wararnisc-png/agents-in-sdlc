---
title: "演習 1 - カスタム指示 (Cloud agent)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Copilot cloud agent →][next-lesson]

生成 AI を使うときは、コンテキストが重要です。作業方法に決まりがある場合や、Copilot に知っておいてほしい背景情報がある場合は、その情報にアクセスできるようにします。[指示ファイル][instruction-files]を使うと、Copilot に作業内容だけでなく方法も伝えられます。

この演習では、次の操作を行います。

- リポジトリのカスタム指示とパス指定の指示ファイルによって、プロジェクト固有のコンテキスト、コーディング ガイドライン、ドキュメント標準が Copilot に伝わる方法を確認します。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加します。

> [!NOTE]
> VS Code や CLI の harness とは異なり、ここではプロンプトの変更前後を比較しません。Copilot cloud agent は GitHub issue に対して非同期で動作するため、リアルタイムで影響を並べて示すのは困難です。後の演習で cloud agent が作成したプルリクエストをレビューするときに、指示ファイルの影響を確認します。

## 指示ファイル

### シナリオ

Tailspin Toys には開発上のガイドラインがあります。

- データ層には必ずユニット テストを用意します。
- UI はダーク モードで、モダンな見た目にします。
- コードのドキュメントには TSDoc doc comment を使います。
- 各ファイルの先頭に、ファイルの役割を説明するコメント ブロックを追加します。

指示ファイルを使い、Copilot がこれらの開発方針に沿って作業できるようにします。

### カスタム指示

カスタム指示では、コーディング スタイルや要件などのコンテキストを Copilot に伝えます。リポジトリ全体、または特定のファイル種別に指示を設定できます。

指示ファイルには次の 2 種類があります。

- `.github/copilot-instructions.md` は、リポジトリに対するすべてのリクエストで Copilot に送られます。技術スタック、プロジェクト概要、ベスト プラクティスなど、広く関係する情報を記載します。
- `.github/instructions/*.instructions.md` は、特定のタスクやファイル種別に適用します。たとえば TypeScript、UI コンポーネント、ユニット テスト向けのガイドラインを記載できます。

> [!NOTE]
> IDE では、指示ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。
>
> Copilot Chat、Copilot CLI、Copilot cloud agent は、リポジトリ レベルの指示ファイルと、`applyTo` frontmatter を持つ `*.instructions.md` ファイルの両方を使います。
>
> Copilot は AGENTS.md や CLAUDE.md など、ほかの標準の指示ファイルにも対応しています。

### 指示ファイルを管理するためのベスト プラクティス

指示ファイルの作成に関する詳しい説明はこの演習の範囲外ですが、このサンプル プロジェクトには代表的な方法を示す例があります。基本的には、次の点を参考にしてください。

- `copilot-instructions.md` には、プロジェクトの説明、構成、全体的なコーディング標準などを記載します。
- `*.instructions.md` には、ユニット テスト、Astro コンポーネント、データ層など、特定のファイル種別やタスクに関する指示を記載します。
- 自然な言葉を使い、明確なガイドラインと、コードをどう書くか・どう書かないかの例を示します。

指示ファイルの作成方法は 1 つではありません。試しながら、プロジェクトに合う方法を見つけてください。

> [!TIP]
> 多くのプロジェクトでは、[UI 更新][ui-instructions]や [Astro][astro-instructions] などのタスク向け指示ファイルを用意しています。Copilot に指示ファイルの作成を依頼することもできます。VS Code では **Configure Chat → Generate Agent Instructions**、Copilot CLI では `/init` を使えます。[awesome-copilot][awesome-copilot] では、指示ファイルやカスタム エージェントの例を確認できます。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトの指示ファイルを確認する

このリポジトリに含まれる指示ファイルを確認します。共通の `copilot-instructions.md` と、タスク別の `*.instructions.md` ファイルがあります。

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの概要に加え、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** の **GitHub Actions Workflows** の指示は、Copilot とのすべてのやりとりに適用されます。
3. `.github/instructions` フォルダーを確認します。Astro ファイル、Drizzle データ層、テストなどの指示があります。
4. `.github/instructions/unit-tests.instructions.md` を開き、先頭の `applyTo` フィールドを確認します。この glob はリポジトリのルートからの相対パスで、たとえば `**/*.test.ts` に一致する TypeScript テスト ファイルに適用されます。
5. このプロジェクトのユニット テストを作成する際の指示を確認します。
6. `.github/instructions/drizzle.instructions.md` の末尾まで読み、`unit-tests.instructions.md` などの指示ファイルやプロジェクト内のファイルへのリンクを確認します。パスはリポジトリのルートではなく、指示ファイルからの相対パスです。

> [!NOTE]
> `copilot-instructions.md` の **Code formatting requirements** セクションにはプロジェクトのコーディング標準が記載されていますが、コード内のドキュメントに関するルールはまだありません。次の手順で TSDoc doc comment とファイル先頭のコメント ヘッダーを追加します。

## リポジトリ全体に適用する標準を追加する

cloud agent は、issue が対象とするブランチの指示ファイルを読み込みます。次の演習で issue を割り当てるとき、Copilot が `main` からブランチを作成するため、追加した指示を `main` に反映します。

1. Codespace のターミナルで、新しいブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions-cloud
   ```

2. `.github/copilot-instructions.md` を開きます。
3. **Code formatting requirements** セクションを探します。現在、コード内ドキュメントのルールがありません。
4. 既存の標準の直後に、次の Markdown を追加します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

5. `copilot-instructions.md` を保存します。

> [!TIP]
> リポジトリ レベルの `.github/copilot-instructions.md` は、doc comment のルールなど、プロジェクト全体の標準を置く場所です。特定の言語やファイル種別には `*.instructions.md` を使います。

## 指示の変更をコミット、プッシュ、マージする

cloud agent は、割り当て先のブランチから指示ファイルを読み込みます。次の演習で作業を割り当てる前に、変更を `main` にマージしてください。

1. 変更をステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md
   git commit -m "Add doc comment and file-header standards to copilot instructions"
   ```

2. ブランチをプッシュします。

   ```bash
   git push -u origin custom-instructions-cloud
   ```

3. github.com で `custom-instructions-cloud` から `main` に向けたプルリクエストを作成し、マージします。

> [!TIP]
> このワークショップではブランチの流れを再現するためにブランチを作成しますが、`main` に直接コミットしてもかまいません。

## まとめと次のステップ

指示ファイルが Copilot にコンテキストを伝える仕組みを確認し、`.github/copilot-instructions.md` にリポジトリ全体の標準を追加しました。残りの演習で cloud agent が作成するプルリクエストをレビューすると、この標準が使われていることを確認できます。

次は [Copilot cloud agent に最初の issue を割り当てます][next-lesson]。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [Copilot 用の優れたカスタム指示を書く 5 つのヒント][copilot-instructions-five-tips]
- [指示ファイルやその他のリソースを集めた Awesome Copilot][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-cloud-agent/
[instruction-files]: https://docs.github.com/copilot/customizing-copilot/about-customizing-github-copilot-chat-responses
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
