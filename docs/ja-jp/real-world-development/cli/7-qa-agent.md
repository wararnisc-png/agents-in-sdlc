---
title: "レッスン 7 - QA エージェントを作成して使う"
description: "issue の要件、quality-checks スキル、Playwright MCP を組み合わせる QA カスタム エージェントを作成します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

`quality-checks` スキルで自動チェックを実行し、Playwright MCP でブラウザー上のフィルター動作を確認しました。次はこれらを、明確な QA プロセスを持つカスタム エージェントにまとめます。

このレッスンでは、指示・スキル・MCP ツールを使うカスタム エージェントの動作を確認し、再利用可能な品質保証プロファイルを作成して、フィルター issue に照らした結果をレビューします。

## シナリオ

Tailspin Toys は、プルリクエスト (PR) を作成する前に、要件、コード品質、自動チェック、テスト範囲、ブラウザーでの動作を一貫して確認したいと考えています。カスタム エージェントで QA プロセスを調整し、再利用可能なレポートを作成します。

## カスタム エージェントとは

カスタム エージェントは、目的、指示、利用可能なツールを Markdown プロファイルで定義する、Copilot の専門エージェントです。この演習では `.github/agents/qa.agent.md` に QA の役割を定義します。リポジトリの指示はチーム標準を、`quality-checks` スキルは繰り返し実行するチェックを、Playwright MCP はブラウザー ツールを提供します。QA プロファイルは、これらを使って要件を評価し、結果を報告する方法を定義します。

## QA プロファイルを作成する

1. Codespace に戻り、フィルターの会話が Interactive モードであることを確認します。
2. 既定のエージェントに次のカスタム エージェントを作成するよう依頼します。

   ```plaintext
   Create a custom agent named QA in .github/agents/qa.agent.md. It should check features against their issues and agreed requirements, follow the repository instructions, run the quality-checks skill, use Playwright MCP to verify behavior, and add tests when coverage is missing.

   Have it report each requirement as pass, fail, or blocked with supporting evidence. It must ask before changing implementation code, and it must not commit changes or open pull requests.

   Just create the profile for now so I can review it.
   ```

## プロファイルを確認する

1. `/diff` を入力し、`.github/agents/qa.agent.md` を開きます。
2. frontmatter を確認します。`description` は必須で、`name` は任意ですが、表示名として設定できます。
3. 要件から開始し、リポジトリの指示に従い、`quality-checks` スキルと Playwright MCP を使うことを確認します。
4. 根拠を示して結果を報告すること、実装コードを変更する前に確認すること、コミットや PR 作成を行わないことを確認します。
5. 不足や範囲の逸脱があれば、既定のエージェントに修正を依頼します。

## issue に対して QA を実行する

1. 次のコマンドで QA エージェントを選択します。

   ```plaintext
   /agent QA
   ```

> [!NOTE]
> 新しく作成したエージェントが一覧に表示されない場合でも、次のコマンドで有効にできます。

2. 次のプロンプトを送信します。

   ```plaintext
   Review the filtering feature against the issue and the decisions in our plan. Is it ready for a PR?
   ```

3. QA エージェントのレポートを確認します。

## まとめと次のステップ

再利用可能な QA の役割を作成し、その結果を確認しました。次は[機能の PR に変更をまとめて Agent Merge を使います][next-lesson]。

## リソース

- [Copilot CLI 用のカスタム エージェントを作成する][create-agents]
- [カスタム エージェントの構成][agent-config]

[previous-lesson]: ../6-mcp-playwright/
[next-lesson]: ../8-create-pull-request/
[create-agents]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/create-custom-agents-for-cli
[agent-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
