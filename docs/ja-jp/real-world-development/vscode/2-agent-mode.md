---
title: "演習 2 - Copilot agent mode で機能を追加する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

アプリの簡単な更新でも、複数のファイルを変更し、テストを実行する必要があることがあります。開発者は必要なファイルを探して変更し、テストを実行してデバッグし、変更し忘れたファイルを見つけてさらに更新します。Copilot Agent Mode は IDE 内でより自律的に作業できます。既存のプロジェクト構成を調査し、必要な変更を行い、テストなどのタスクを実行して、見つかった間違いを自動的に修正します。この演習では、Agent Mode でサイトに機能を追加します。

> [!NOTE]
> 名前は似ていますが、agent mode と cloud agent は異なる用途向けです。agent mode は IDE 内で動作し、すばやくやりとりできます。cloud agent は issue とプルリクエストを通じてチーム メンバーのように非同期で作業します。

この演習では、次の方法を学びます。

- Copilot Agent Mode がプロジェクトを調査し、関連ファイルを特定して、複数のファイルを連携して変更する。
- GitHub Copilot Agent Mode が UI とデータ層にまたがる新機能を実装する。
- Copilot Agent Mode が生成した変更とテストをレビューしてから、コードベースにマージする。

## シナリオ

ゲームの一覧が増えてきたため、カテゴリと出版社で絞り込めるようにします。前の演習で追加した publishers helper を使い、Copilot Agent Mode で残りのデータ層、UI、テストの作業を行います。

## Tailspin Toys の Web サイトを実行する

変更を始める前に、Tailspin Toys の Web サイトの現在の機能を確認します。これは開発者をテーマにしたボードゲームのクラウドファンディング サイトです。単一の Astro アプリで、ビルド時に静的 HTML を生成します。ページは frontmatter 内で Drizzle ORM を通じてローカル SQLite データベースを参照します。別のバックエンド API やクライアント側 UI フレームワークはありません。再利用可能なデータアクセス ヘルパーは `src/lib/` に置き、インタラクティブ動作は Astro の `<script>` と標準 DOM API で実装します。

### Web サイトを起動する

`npm run dev` タスクで Astro 開発サーバーを起動できます。GitHub Codespace で次の手順を行います。

1. Codespace に戻ります。前の演習から `main` に戻っているはずです。
2. Codespace で <kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) を押して新しいターミナルを開きます。
3. フィルター作業用のブランチを作成して切り替えます。

   ```bash
   git checkout main
   git pull
   git checkout -b filtering-vscode
   ```

4. 次のコマンドを実行して Web サイトを起動します。

   ```bash
   npm run dev
   ```

   Astro の開発サーバーが起動すると、次のような URL が表示されます。

   ```bash
   🚀 Tailspin Toys is ready!
      Astro server: http://localhost:4321
      Press Ctrl-C to stop.
   ```

> [!NOTE]
> `http://localhost:4321` を開くか尋ねるダイアログが表示された場合は、**x** を選択して閉じます。

5. <kbd>Command</kbd> (Mac) または <kbd>Ctrl</kbd> (Windows/Linux) を押しながら、ターミナルに表示された `http://localhost:4321` を選択して Web サイトを開きます。

> [!NOTE]
> Codespace のターミナルで localhost URL を選択すると、`https://<your-codespace-name>-4321.app.github.dev/` に自動転送されます。これは Web サーバーをホストしている Codespace へのプライベート トンネルです。

### Web サイトを確認する

Web サイトが起動したら、次の主な機能を確認できます。

- **Home Page**: タイトル、画像、説明を含むボードゲームの一覧を表示します。
- **Game Details Page**: ゲームを選択すると、タイトル、説明、出版社、カテゴリなどの詳細ページを表示します。

## Copilot でバックログを確認する

> [!TIP]
> **Copilot Chat を開く**
>
> 以下の演習を始める前に Codespace に戻り、Copilot Chat パネルを開いて **New Chat** を選択し、新しい会話を始めます。モードとモデルの選択は演習ごとに異なります。必要な選択肢は、それぞれの手順で説明します。

Web サイトはすでに動作しますが、新しい機能を追加して改善します。テンプレートからプロジェクトを設定すると GitHub issue のバックログが自動的に作成されるため、Copilot に一覧を表示するよう依頼します。

1. Chat ビューのエージェントのドロップダウンから **Agent** を選択します。Agent は複数のファイルにわたって自律的に計画・実装し、ターミナル コマンドを実行してツールを呼び出します。

   ![Chat ビューのエージェント ピッカー](../../../_images/shared-chat-mode-selector.png)

2. 使用可能なモデル一覧から **Claude Sonnet 4.5** を選択します。

> [!CAUTION]
> ワークショップの作成者は特定のモデルを推奨していません。作成時に Claude Sonnet 4.5 を使ったため、例の結果を揃えて学習しやすくする目的で手順に含めています。ただし、LLM は確率的に動作するため、提案は例と異なる場合があります。これは通常の動作です。

> [!NOTE]
> Copilot は確率的に動作するため、別の MCP コマンドを使う場合がありますが、タスクは完了できます。

3. 次のプロンプトを Copilot に送ります。

   ```plaintext
   Please show me the backlog of items from my GitHub repository. Help me prioritize them based on those which will be most useful to the user.
   ```

4. issue を一覧表示するコマンドを実行するには **Continue** を選択します。
5. Copilot が生成した issue の一覧を確認します。

Copilot は、ユーザーに最も役立つと考える項目を基に優先順位も付けています。

## 指示ファイルを確認する

コードの生成を agent に依頼する前に、作業のコンテキストを Copilot に与える指示ファイルを確認します。[user interface (UI) 指示ファイル](https://github.com/github-samples/tailspin-toys/blob/main/.github/instructions/ui.instructions.md)には、Web サイトに機能を追加する方法が記載されています。

1. Codespace で `.github/instructions/ui.instructions.md` に移動します。
2. 機能追加の進め方に関する全体的なガイダンスを確認します。次の内容が含まれます。
   - アーキテクチャの概要
   - コンポーネント設計、テスト容易性、アクセシビリティの原則
   - Astro、Tailwind CSS、Drizzle など、さまざまなファイル種別に対応する指示ファイルへのリンク

> [!TIP]
> 指示ファイルでは、ほかの指示ファイルやプロジェクト内のファイルを参照できます。パスは指示ファイルの場所からの相対パスです。これにより、再利用したり、大きな指示を小さく分けたり、例やテンプレートを示したりできます。

## フィルター機能を実装する

フィルターを完成させるには、少なくとも次の 3 つを更新します。

- データ層 (`src/lib/`) の残りのフィルター ロジックを追加または調整します。
- フィルターの動作を確認するテストを追加または更新します。
- ゲーム一覧ページにフィルター UI を追加します。

コードベースにマージする前に、テストを実行して成功を確認します。Copilot Agent Mode にこれらの作業を依頼します。

1. 現在の Copilot 会話を続けるか、**New Chat** を選択して新しい会話を始めます。
2. **Add Context**、**Instructions**、**ui** の順に選択します。

   ![UI 指示ファイルを選択する画面](../../../_images/ex3-select-instructions-file.png)

3. Chat ビューのエージェント ドロップダウンで **Agent** が選択されていることを確認します。

   ![Chat ビューのエージェント ピッカー](../../../_images/shared-chat-mode-selector.png)

4. モデルが **Claude Sonnet 4.5** のままであることを確認します。
5. バックログの関連 issue に基づいて機能を実装するよう、次のプロンプトを送信します。

   ```plaintext
   Please update the site to include filtering by publisher and category based on the requirements from the related GitHub issue in the backlog. A publishers helper already exists from the previous exercise, so preserve and refine that work as needed while completing the remaining data-layer, UI, and tests. Ensure all tests are passing before completion. The server is already running, so you do not need to start it up.
   ```

6. Copilot がプロジェクトを調査し、機能に関連するファイルを探す様子を確認します。データ層ヘルパー、UI、テストを見つけた後、ファイルを変更してテストを実行します。

   ![Copilot がプロジェクト ファイルを調査する画面](../../../_images/ex3-agent-mode-explores.png)

> [!NOTE]
> Copilot はプロジェクトを調査し、ファイルを変更し、テストを実行します。タスクやコードベースの複雑さによって数分かかることがあります。作業中、エディターに **Keep** と **Undo** が表示されることがあります。作業中に選択する必要はなく、完了後に変更ごとに表示されます。

7. Copilot に求められたら、**Continue** を選択してテストを実行します。

   ![Copilot Chat でテスト実行の確認を求めるダイアログ](../../../_images/ex3-agent-mode-run-tests.png)

8. 作業中に一時停止したり、テストが失敗したりすることがあります。Copilot はコード生成とテストを繰り返し、タスクを完了してエラーがないと判断するまで修正します。

   ![Copilot Agent Mode の完了した Chat セッション](../../../_images/ex3-agent-mode-proposed-changes.png)

9. 生成されたコードに問題がないか確認します。

> [!CAUTION]
> Copilot やほかの AI ツールが生成したコードは、必ずレビューしてください。

10. Web サイトを起動しているブラウザーに戻り、新機能を試します。
11. 動作とコードを確認したら、Copilot Chat で **Keep** を選択します。

## まとめと次のステップ

この演習では、GitHub Copilot Agent Mode で Tailspin Toys に新機能を追加する方法を確認しました。

- GitHub Copilot Agent Mode で UI とデータ層にまたがる機能を実装できます。
- Copilot Agent Mode はプロジェクトを調査し、関連ファイルを見つけて、協調して変更できます。
- コードベースにマージする前に、Copilot Agent Mode が生成した変更とテストをレビューします。

次は [Playwright MCP サーバーで機能をテスト][next-lesson]し、プルリクエストを作成します。

### ボーナス演習 — ページネーションを実装する

ゲーム一覧が増えると、ページネーションが必要になります。この演習で学んだスキルを使い、Copilot にページネーションの実装を依頼します。コードについては、次の点を検討してください。

- 既存の指示ファイルを使うなど、現在のベスト プラクティスに従います。
- ユーザーがページ サイズを選べるようにするか、固定値にするかを検討します。
- 希望する実装に必要なガイダンスをプロンプトに含めます。
- Copilot に変更や追加のコンテキストを伝え、反復して調整する必要があるかもしれません。これは Copilot を使う通常の開発フローです。

## リソース

- [Copilot の ask、edit、agent mode: 機能と使い分け][choose-mode]
- [VS Code の agent mode][vs-code-agent-mode]

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-mcp/
[choose-mode]: https://github.blog/ai-and-ml/github-copilot/copilot-ask-edit-and-agent-modes-what-they-do-and-when-to-use-them/
[vs-code-agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
