---
title: "レッスン 6 - Playwright MCP で機能を検証する"
description: "Copilot CLI で Playwright MCP を確認または設定し、ブラウザーでフィルター機能を調べます。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

コードを書くこと以外にも、データや外部サービスとの連携、Copilot が利用する自動化ツールの追加が必要です。MCP サーバーを使うと、Copilot CLI に組み込まれていないツールやサービスを利用できます。

このレッスンでは、Model Context Protocol (MCP) と Copilot CLI での利用方法を確認し、必要に応じて Playwright MCP サーバーを追加して、エージェントにブラウザーでフィルター機能を試させます。

## シナリオ

ユニット テストやエンドツーエンド テストは重要ですが、UI の変更を検証するには、実際に UI を操作する必要があります。ユーザーと同じようにサイトを使う手段を Copilot に与え、変更が期待どおりに動くか確認します。

## Model Context Protocol (MCP) とは

[Model Context Protocol (MCP)][mcp-blog-post] は、AI エージェントが外部のツールやサービスと通信するための仕組みです。MCP を使うと、最新情報にアクセスしたり、エージェントに操作を依頼したりできます。MCP サーバーがエージェントと外部ツールの間の橋渡しをします。

- **[GitHub MCP Server][github-mcp]** は、GitHub リポジトリ、issue、プルリクエストを管理する API を提供します。
- **[Playwright MCP Server][playwright-mcp-server]** は、Playwright によるブラウザー自動化機能を提供します。

GitHub には、MCP サーバーを見つけてエコシステムに貢献するための [MCP registry][mcp-registry] があります。

> [!CAUTION]
> MCP サーバーはほかの依存関係と同様に扱ってください。使用前にソース コードと発行元を確認し、セキュリティへの影響を検討します。

## Playwright MCP サーバーを追加する

Copilot CLI で Playwright MCP サーバーがまだ利用できない場合は、追加します。すでに設定済みであれば、この手順を省略して次に進みます。

1. Codespace に戻り、Copilot CLI で次のコマンドを入力します。

   ```plaintext
   /mcp add
   ```

2. 名前に `playwright` と入力して <kbd>Tab</kbd> を押します。
3. サーバーの種類として **STDIO** を確認し、<kbd>Enter</kbd>、次に <kbd>Tab</kbd> を押します。
4. **Command** の入力欄に次を貼り付けます。

   ```plaintext
   npx -y @playwright/mcp@latest --headless --no-sandbox
   ```

5. <kbd>Control</kbd>+<kbd>S</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>S</kbd> (Windows/Linux) で保存し、<kbd>Esc</kbd> でダイアログを閉じます。

## Playwright で機能を確認するよう Copilot に依頼する

1. 次のプロンプトで、Playwright MCP を使って機能を検証するよう Copilot に伝えます。

   ```plaintext
   Start the app and use Playwright MCP to check filtering against the issue and our plan. Tell me what works and what doesn't, without making changes. Stop the server you started when you're done.
   ```

Copilot は必要に応じてアプリを起動し、Playwright でブラウザーを操作してからサーバーを停止し、結果を報告します。MCP サーバーを明示しなくても Copilot が適切なツールを選ぶ場合があります。

## まとめと次のステップ

Copilot CLI で Playwright MCP サーバーを使い、実際のブラウザーでフィルター機能を確認しました。次はスキルとブラウザー ツールを組み合わせる[QA カスタム エージェント][next-lesson]を作成します。

## リソース

- [MCP とは何か、なぜ話題になっているのか][mcp-blog-post]
- [Microsoft Playwright MCP Server][playwright-mcp-server]
- [Copilot CLI に MCP サーバーを追加する][add-mcp]

[previous-lesson]: ../5-agent-skills/
[next-lesson]: ../7-qa-agent/
[mcp-blog-post]: https://github.blog/ai-and-ml/llms/what-the-heck-is-mcp-and-why-is-everyone-talking-about-it/
[playwright-mcp-server]: https://github.com/microsoft/playwright-mcp
[github-mcp]: https://github.com/github/github-mcp-server
[mcp-registry]: https://github.com/mcp
[add-mcp]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-mcp-servers
