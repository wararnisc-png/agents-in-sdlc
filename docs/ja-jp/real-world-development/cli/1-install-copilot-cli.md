---
title: "レッスン 1 - GitHub Copilot CLI をインストールする"
description: "Codespace に Copilot CLI をインストールして認証し、基本操作を確認して、用意されたフィルター issue を見つけます。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

[GitHub Copilot CLI][about-copilot-cli] は、ターミナルで動作するエージェント型コーディング アシスタントです。コードベースの調査、コードの生成、コマンドの実行、外部ツールとのやりとりをコマンドラインから行えます。まずツールをインストールします。普段使っているツールで手順を進められます。

このレッスンでは、npm を使って Copilot CLI をインストールし、GitHub アカウントで認証し、ワークショップのリポジトリを信頼して簡単な会話を試し、組み込みの GitHub MCP サーバーからフィルター issue を見つけます。

## シナリオ

チームでは増え続けるバックログに対応するため、AI エージェントを使い始めています。Copilot CLI は、開発者が普段使っているターミナルでその機能を使えるようにします。このレッスンでインストールと認証を完了し、残りのワークショップに備えます。

## Copilot CLI をインストールする

Copilot CLI は [npm][install-cli]、WinGet、Homebrew でインストールできます。GitHub Codespaces には Node.js がインストール済みのため、npm を使います。

1. Codespace に戻り、ターミナルを開きます。
2. Node.js が必要なバージョンを満たしていることを確認します。

   ```bash
   node --version
   ```

   バージョン 24 以上が表示されます。

3. Copilot CLI をグローバルにインストールします。

   ```bash
   npm install -g @github/copilot
   ```

4. インストールを確認します。

   ```bash
   copilot --version
   ```

## GitHub で認証する

初回起動時に、Copilot CLI は GitHub アカウントでの認証を求めます。

1. Copilot CLI を起動します。

   ```bash
   copilot
   ```

2. 表示された device code の手順に従って認証し、Copilot CLI を許可します。
3. Copilot CLI は、現在のフォルダー内のファイルを読み取り、許可を得て編集やコード・シェル コマンドの実行を行うこと、許可設定はセッション中保持されることを説明し、フォルダーを信頼するか確認します。
4. 表示されたパスが Tailspin Toys リポジトリであることを確認し、**Yes, and remember this folder for future sessions** を選択します。

> [!NOTE]
> Codespace では GitHub セッションを通じて認証済みの場合があります。認証を求められずに起動した場合は、そのまま進めてください。

## 基本操作を確認する

通常のシェル プロンプトでは、コマンドは Codespace 上で直接実行されます。Copilot CLI の起動後は、自然言語をエージェントに送り、スラッシュ コマンドで会話を操作します。

1. `/model` を入力し、矢印キーで **Auto** を選択して <kbd>Enter</kbd> を 2 回押します。
2. `/help` で利用可能なコマンドを確認し、<kbd>Esc</kbd> で画面を閉じます。
3. 簡単な質問をして動作を確認します。

   ```plaintext
   What are the key files in this project?
   ```

4. Copilot が回答前にリポジトリを調べる様子を確認します。
5. `/mcp list` を入力し、組み込みの GitHub MCP サーバーが利用可能であることを確認します。
6. 次のプロンプトでフィルター issue を探します。

   ```plaintext
   Using GitHub MCP, find the issue in this repository titled "Allow users to filter games by category and publisher." Give me its URL and a short summary. Don't change anything.
   ```

7. URL を開いて issue を読みます。最初の変更を終えた後で使用します。

> [!TIP]
> 通常の Copilot CLI セッションは、ターミナルで現在チェックアウトしているブランチを使い、自動的に worktree を作成しません。変更を始める前に機能ブランチを作成します。

## ワークショップ用のショートカットを使う

通常、Copilot CLI は設定された許可の範囲外でツールを使う前に確認します。このワークショップでは `--yolo` を付けて起動し、Codespace 内で承認プロンプトを省略して演習に集中します。

> [!CAUTION]
> `--yolo` は完全な自動許可 (`--allow-all-tools`、`--allow-all-paths`、`--allow-all-urls`) を有効にします。Codespace や VM などの分離された環境でのみ使用し、日常の開発の既定値として alias に設定しないでください。詳細は[ツールの許可と拒否][allow-all-warning]を参照してください。

`--enable-all-github-mcp-tools` は、後のレッスンで issue やプルリクエストを扱うための GitHub MCP 読み取り・書き込みツールを有効にします。Codespace はローカル コンピューターへのアクセスを制限しますが、認証済みの GitHub リソースは実際のものです。公開やマージの前に変更をレビューしてください。

1. `/exit` で Copilot CLI を終了します。
2. リポジトリのルートから次のコマンドで再起動します。

   ```bash
   copilot --yolo --enable-all-github-mcp-tools
   ```

3. プロジェクトについてもう一度質問し、会話が動作することを確認してから `/exit` で終了します。

Copilot は会話を自動的に保存します。後で指示を変更したりエージェントを追加したりした後、`copilot --resume` で同じ会話とブランチに戻ります。

## まとめと次のステップ

npm で Copilot CLI をインストールして GitHub アカウントで認証し、ワークショップのリポジトリを信頼して、組み込みの GitHub MCP サーバーからフィルター issue を見つけました。次は最初の変更を行い、ゲーム カードに星評価を表示します。

## リソース

- [GitHub Copilot CLI をインストールする][install-cli]
- [GitHub Copilot CLI について][about-copilot-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../0-prerequisites/
[next-lesson]: ../2-add-star-rating/
[install-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
[about-copilot-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[allow-all-warning]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli#allowing-and-denying-tool-use
