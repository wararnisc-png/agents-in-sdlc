---
title: "レッスン 2 - 星評価を追加する: 小さな成果を得る"
description: "Copilot CLI でゲーム カードに小さな変更を加え、転送されたブラウザーで確認し、最初のプルリクエストとしてマージします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Copilot CLI をインストールし、会話を試しました。次はプロジェクトに初めて変更を加えます。ゲーム データには星評価がありますが、ホーム ページのゲーム カードにはまだ表示されていません。エージェントに表示を依頼し、変更をレビューして、最初のプルリクエストとしてマージします。

このレッスンでは、次の操作を行います。

- 機能ブランチで Copilot の会話を始めます。
- 小さな変更を依頼します。
- `/diff` で変更をレビューします。
- 転送されたブラウザーでアプリを確認します。
- 最初のプルリクエストを作成してマージします。

## シナリオ

Tailspin Toys の各ゲームには星評価があり、ゲーム詳細ページにはすでに表示されています。ホーム ページのゲーム カードにはタイトル、カテゴリ、出版社、説明しか表示されていません。まず、既存の評価を各カードに表示します。

## 会話の構成

**会話**は、Copilot CLI で作業する場です。通常の CLI 会話では、専用の worktree ではなく、ターミナルで現在チェックアウトしているリポジトリと Git ブランチを使います。保存した会話は後で再開できますが、ファイルとブランチは通常の Git 状態としてディスク上にあります。

会話では、プロンプトとエージェントの応答、ファイルを調査・編集するツールの操作、`/diff` で確認できる変更を見られます。

## 会話を始めて変更を依頼する

1. Codespace に戻ります。
2. 必要であれば、<kbd>Control</kbd>+<kbd>`</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>`</kbd> (Windows/Linux) でターミナルを開きます。
3. Copilot CLI を起動します。

   ```bash
   copilot --yolo
   ```

4. `/new` を入力して <kbd>Enter</kbd> を押し、新しいセッションを開始します。
5. 次のプロンプトを送信します。

   ```plaintext
   Show each game's starRating out of 5 in the game cards on the list page. If the rating is null, show "No rating yet". Keep the card layout as it is, add tests, and run the relevant checks.
   ```

Copilot がプロジェクトを確認し、ゲーム詳細を表示するファイルを探して必要なコードを作成します。

## 差分をレビューする

AI が生成した変更は、小さくてもマージ前にレビューします。

1. `/diff` を入力し、変更されたすべてのファイルを確認します。
2. 評価があれば数値で表示され、`starRating` が `null` なら `No rating yet` と表示されることを確認します。
3. どちらの状態もテストされていることを確認します。
4. Copilot が実行したチェックの結果を確認し、失敗があれば修正を依頼します。
5. レビュー後、<kbd>Esc</kbd> を押して差分画面を閉じます。

> [!NOTE]
> 生成 AI は確率的に動作するため、コードは例と異なる場合があります。特定の実装ではなく、動作を確認してください。

## 変更を確認する

コードを読むだけでなく、Codespaces で転送されたブラウザーから更新後の UI を確認します。

1. Copilot にアプリの起動を依頼します。

   ```plaintext
   Start the app so I can inspect the star-rating change in my browser. Tell me the URL and leave the server running.
   ```

2. Codespaces がポート `4321` を使用可能と通知したら、**Open in Browser** を選択します。
3. ゲーム カードに 5 段階評価が表示されることを確認します。
4. Copilot に、起動したサーバーを停止するよう依頼します。

   ```plaintext
   Stop the development server you started.
   ```

## 最初のプルリクエストを作成してマージする

1. Copilot の既定エージェントに、変更をコミットするよう依頼します。

   ```plaintext
   Commit the reviewed star-rating changes with an appropriate commit message.
   ```

2. `/pr create` を入力します。Copilot CLI が PR 作成時に既存のコミットをプッシュし、PR の URL を表示します。
3. Copilot CLI に表示された URL を <kbd>Command</kbd> (Mac) または <kbd>Ctrl</kbd> (Windows/Linux) を押しながら選択します。
4. 変更されたファイルとチェックをレビューし、**Merge pull request** を選択してマージを確定します。
5. Codespace に戻り、`/exit` で Copilot CLI を終了します。
6. ローカルの `main` を更新します。

   ```bash
   git checkout main
   git pull
   ```

## まとめと次のステップ

Copilot CLI で最初の変更をリリースしました。機能ブランチで会話を始め、ゲーム カードに変更を依頼し、`/diff` でレビューし、転送されたブラウザーで確認して、最初の PR をマージしました。次は [フィルター issue から始め、Plan と Autopilot モードを使って][next-lesson]大きな機能を構築します。

## リソース

- [GitHub Copilot CLI について][about-copilot-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../1-install-copilot-cli/
[next-lesson]: ../3-agent-modes/
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
