---
title: "演習 1 - カスタム指示 (VS Code)"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: 前提条件][previous-lesson] · [次のレッスン: Agent mode →][next-lesson]

生成 AI を使うときは、コンテキストが重要です。作業方法に決まりがある場合や、Copilot に知っておいてほしい背景情報がある場合は、そのコンテキストにアクセスできるようにします。Copilot と特定のコンテキストを共有する方法はいくつかあります。その中でも重要なのが、コード生成に関するガイダンスを伝える[指示ファイル][instruction-files]です。

この演習では、次のことを行います。

- リポジトリのカスタム指示とパス指定の指示ファイルによって、プロジェクト固有のコンテキスト、コーディング ガイドライン、ドキュメント標準が Copilot に伝わるしくみを確認します。
- 現在の指示を適用した状態で、フィルター機能の最初のデータ部分となる publishers helper を生成します。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する新しい標準を追加します。
- 同じプロンプトを再実行し、生成コードが新しい標準に従う様子を確認します。
- 指示の更新とフィルター用データ部分を `main` にコミットし、次の演習で更新後のガイダンスを使えるようにします。

> [!CAUTION]
> 生成コードは、設定した標準から外れることがあります。Copilot の出力は確率的です。この演習では、文字単位で同じ結果になることではなく、指示の更新後に傾向が変わることを確認します。

## 指示ファイル

### シナリオ

Tailspin Toys では、データ層にユニット テストを用意し、UI をダーク モードでモダンな見た目にし、TSDoc doc comment と各ファイルの先頭に説明コメントを追加する標準があります。指示ファイルを使い、Copilot がこれらの方針に沿うようにします。

### カスタム指示

カスタム指示では、コーディング スタイルや要件などのコンテキストを Copilot に伝えます。これは、より適切な提案やコード スニペットを得るために、好みの規約、ライブラリ、コメントの書き方などを指定できる強力な機能です。リポジトリ全体にも、特定のファイル種別にも指示を作成できます。

- `.github/copilot-instructions.md` は、リポジトリへのすべてのリクエストに送られるプロジェクト レベルの指示です。技術スタック、プロジェクト概要、全体的なガイダンスを記載します。
- `.github/instructions/*.instructions.md` は、特定のタスクやファイル種別に適用します。たとえば TypeScript、UI コンポーネント、ユニット テスト向けの指示を記載できます。

> [!NOTE]
> IDE では、指示ファイルは Copilot Chat のコード生成にのみ使われ、コード補完や次の編集候補には使われません。Copilot Chat、Copilot CLI、Copilot cloud agent は、リポジトリ レベルの指示と `applyTo` frontmatter を持つ `*.instructions.md` ファイルを使用します。AGENTS.md や CLAUDE.md などの標準にも対応しています。

### 指示ファイルを管理するためのベスト プラクティス

指示ファイルの作成方法を詳しく説明することはこのワークショップの範囲外ですが、サンプル プロジェクトには代表的な方法が示されています。大まかな方針は次のとおりです。

- `copilot-instructions.md` には、何を開発しているか、プロジェクトの構成、全体的なコーディング標準など、プロジェクト レベルのガイダンスを記載します。
- `*.instructions.md` には、ユニット テスト、Astro コンポーネント、データ層などのファイル種別や特定タスク向けの指示を記載します。
- 自然な言葉を使い、明確なガイダンスと、コードをどう書くか・どう書かないかの例を示します。

指示ファイルの作成方法は 1 つではありません。試しながら、プロジェクトに合う方法を見つけてください。

> [!TIP]
> このリポジトリには、[UI 更新][ui-instructions]や [Astro][astro-instructions] などの指示ファイルがあります。VS Code の **Configure Chat → Generate Agent Instructions** や Copilot CLI の `/init` を使って、Copilot に指示ファイルの作成を依頼できます。[awesome-copilot][awesome-copilot] にある例も参考にしてください。

[ui-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md
[astro-instructions]: https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/astro.instructions.md
[awesome-copilot]: https://github.com/github/awesome-copilot
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support

## このプロジェクトの指示ファイルを確認する

1. `.github/copilot-instructions.md` を開きます。
2. プロジェクトの簡潔な説明と、**Agent notes**、**Code standards**、**Scripts**、**Repository Structure** などのセクションを確認します。**Code standards** にある **GitHub Actions Workflows** の入れ子の指示は、Copilot とのあらゆるやりとりに適用されます。
3. `.github/instructions` フォルダーを開いて内容を確認します。Astro ファイル、Drizzle データ層、テストなどの指示があります。
4. `.github/instructions/unit-tests.instructions.md` を開きます。先頭の `applyTo` フィールドは、リポジトリ ルートからの相対 glob を定義します。ここでは、たとえば `**/*.test.ts` に一致する TypeScript テスト ファイルに適用されます。
5. このプロジェクトでユニット テストを作成する際の指示を確認します。
6. `.github/instructions/drizzle.instructions.md` を開いて末尾までスクロールします。`unit-tests.instructions.md` などの別の指示ファイルや、プロジェクト内の既存ファイルへのリンクがあります。大きな指示を再利用可能な小さなファイルに分け、Copilot が生成時に参考にできる例を示せます。ここにあるパスは指示ファイルからの相対パスです。

> [!NOTE]
> **Code formatting requirements** にはコード内ドキュメントのルールがありません。次に TSDoc doc comment とファイル ヘッダーの標準を追加します。

## 変更用ブランチを作成する

1. 前の演習で使った Codespace に戻ります。
2. <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押してターミナルを開きます。
3. ブランチを作成して切り替えます。

   ```bash
   git checkout -b custom-instructions
   ```

## 指示を更新する前に Copilot Chat を使う

> [!TIP]
> **Copilot Chat を開く**
>
> 以下の演習を始める前に Codespace に戻り、Copilot Chat パネルを開いて **New Chat** を選択し、新しい会話を始めます。モードとモデルの選択は演習ごとに異なります。必要な選択肢は、それぞれの手順で説明します。

1. 前の演習で開いたタブを閉じます。
2. `src/lib/publishers.ts` を開きます。
3. Chat ビューのドロップダウンから **Agent** を選択します。

   ![Chat ビューのエージェント ピッカー](../../../_images/shared-chat-mode-selector.png)

4. 次のプロンプトを送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

5. Copilot がプロジェクトを調査してコードを更新します。ヘルパー ファイルとテストが変更されることがあります。
6. 提案されたヘルパーは、通常、最初の引数として `db` クライアントを受け取り、型付き出版社配列を返す関数です。これは `src/lib/*.ts` に適用される `.github/instructions/drizzle.instructions.md` のデータ層規約によるものです。
7. 提案されたコードに TSDoc doc comment とファイル先頭コメントがないことを確認します。

> [!CAUTION]
> Copilot は確率的に動作するため、指示を更新する前からコメントを追加する場合もあります。その場合も問題ありません。ここで確認するのは、指示の更新後に一貫性がどのように改善するかです。

## リポジトリ全体に適用する標準を追加する

1. `.github/copilot-instructions.md` を開きます。
2. 27 行目付近にある **Code formatting requirements** セクションを見つけます。このセクションにはプロジェクトのコーディング標準が記載されていますが、コード内ドキュメントのルールはありません。そのため、先ほど生成されたヘルパーには doc comment がありませんでした。
3. 既存の標準のすぐ下に次の Markdown を追加し、Copilot にファイル ヘッダーと TSDoc doc comment を追加するよう指示します。

   ```markdown
   - Every exported function should have a TSDoc comment describing its purpose, parameters, and return value.
   - Before imports or any code, add a comment block to the file that explains its purpose.
   ```

4. `copilot-instructions.md` を保存します。

> [!TIP]
> 前のレッスンで確認したように、指示ファイルはリポジトリ レベル (`.github/copilot-instructions.md`) に置いて全体に適用することも、特定の言語、ファイル種別、タスク向けの `*.instructions.md` として作成することもできます。doc comment のルールのようなプロジェクト全体の標準には、リポジトリ レベルのファイルが適しています。

## 同じプロンプトを再実行して変化を確認する

1. Copilot Chat に戻り、**New Chat** を選択して会話のバッファーをクリアします。
2. `src/lib/publishers.ts` をクリックして、Copilot が適切なファイルに注目するようにします。
3. 前と**同じプロンプト**を送信します。

   ```plaintext
   Create or update src/lib/publishers.ts with a data-access helper that returns a list of all publishers with the name and id for each. Apply the file changes.
   ```

4. 提案されたファイルの先頭に、次のようなコメント ブロックが追加されていることを確認します。

   ```typescript
   /**
    * Tailspin Toys Crowd Funding プラットフォーム用の出版社データアクセス ヘルパーです。
    * データベースから出版社情報を取得する関数を提供します。
    */
   ```

   ```typescript
   /**
    * すべての出版社の ID と名前の一覧を返します。
    *
    * @param db - Drizzle データベース クライアント。
    * @returns 出版社オブジェクトの配列に解決する Promise。
    */
   ```

5. 提案された関数に TSDoc コメントが付いていることを確認します。

これで新しいプロジェクト標準を Copilot に伝え、次の演習で使うコードに適用しました。

## 指示とブランチをコミットしてプッシュする

1. <kbd>Control</kbd>+<kbd>\`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>\`</kbd> (Windows/Linux) を押して新しいターミナルを開きます。
2. ターミナルで `git status` を実行し、指示ファイルの更新とヘルパーの変更があることを確認します。
3. 指示ファイルと Copilot がヘルパーの基礎として変更したすべてのファイルをステージしてコミットします。

   ```bash
   git add .github/copilot-instructions.md src/lib/publishers.ts
   # git status にテストなどの関連する補助的な変更が表示された場合は、それらのファイルも追加します。
   git commit -m "Add doc comment standards and publishers helper foundation"
   ```

4. ブランチをリポジトリにプッシュします。

   ```bash
   git push -u origin custom-instructions
   ```

## プルリクエストを作成してマージする

ブランチをプッシュしたら、バックログにあるドキュメント標準の issue と関連付けたプルリクエストを作成します。手動で行うこともできますが、プロジェクトに接続済みの GitHub tools を使って Copilot に任せられます。Copilot に issue を探し、issue をクローズする PR を作成してからマージするよう依頼します。

> [!NOTE]
> Copilot に GitHub 上の操作を依頼するのはこれが初めてです。プロジェクト テンプレートでは GitHub tools がワークスペースに接続済みなので、設定は不要です。Copilot が初めてツールを使うときに、VS Code で GitHub へのサインインを求められる場合があります。画面の指示に従ってください。この接続 (Model Context Protocol) のしくみは、後の演習で学びます。

1. Codespace で Copilot Chat を開きます。
2. <kbd>Control</kbd>+<kbd>Command</kbd>+<kbd>I</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>I</kbd> (Windows/Linux) を押して Copilot Chat ビューを開き、エージェント ピッカーで **Agent** が選択されていることを確認します。
3. 指示ファイルの更新に関する issue を探し、現在のブランチから PR を作成して、その issue をクローズすることと、今後のフィルター作業に向けた publishers helper の基礎も追加したことを記載するよう Copilot に依頼します。

   ```
   Find the issue related to updating the instructions file. Create a new PR from the current branch, highlight that the PR closes that issue, and include that we also added the publishers helper foundation for the upcoming filtering work.
   ```

4. Copilot が issue を探して PR を作成します。
5. Copilot に GitHub 操作の許可を求められたら、コマンドを確認してから適切に **Allow** を選択します。
6. PR が作成されたら、次のプロンプトで PR を `main` にマージし、ローカル ブランチも `main` に戻して最新状態にするよう依頼します。

   ```
   Merge the PR into main. Then return to main locally, and pull the latest code so we are up to date.
   ```

7. Copilot に GitHub 操作やシェル コマンドの許可を求められたら、内容を確認し、適切な場合に許可します。

これで GitHub Copilot のサポートを使ってプルリクエストを作成し、マージできました。

## まとめと次のステップ

このプロジェクトの指示ファイルから Copilot がコンテキストを取得するしくみを確認し、VS Code の Copilot Chat を使って次のことを行いました。

- 既存の指示でコード生成プロンプトを送り、Copilot の出力を確認しました。
- `.github/copilot-instructions.md` にリポジトリ全体に適用する標準を追加しました。
- 同じプロンプトを再実行し、提案されたコードが新しい標準に従う様子を確認しました。
- 指示の更新と publishers helper の基礎を `main` にコミットし、次の演習で利用できるようにしました。

次は [agent mode][next-lesson] で、コードベース全体にわたる新機能を Copilot に追加してもらいます。

## リソース

- [GitHub Copilot のカスタマイズに使う指示ファイル][instruction-files]
- [カスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [Copilot 用の優れたカスタム指示を書く 5 つのヒント][copilot-instructions-five-tips]
- [GitHub Copilot の個人用カスタム指示][personal-instructions]
- [指示ファイルの例を集めた Awesome Copilot][awesome-copilot]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-agent-mode/
[instruction-files]: https://code.visualstudio.com/docs/copilot/copilot-customization
[instructions-best-practices]: https://docs.github.com/enterprise-cloud@latest/copilot/using-github-copilot/coding-agent/best-practices-for-using-copilot-to-work-on-tasks#adding-custom-instructions-to-your-repository
[personal-instructions]: https://docs.github.com/copilot/customizing-copilot/adding-personal-custom-instructions-for-github-copilot
[copilot-instructions-five-tips]: https://github.blog/ai-and-ml/github-copilot/5-tips-for-writing-better-custom-instructions-for-copilot/
