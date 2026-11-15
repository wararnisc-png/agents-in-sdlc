---
title: "レッスン 5 - quality-checks スキルを調整して使う"
description: "既存の quality-checks スキルを確認し、結果のレポート形式を調整して、フィルター機能を検証します。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

コードを書くこと以外にも、手動で動作を確認したり、指示ファイルで標準に従わせたりする作業があります。テスト、lint、継続的インテグレーション (CI) のほかの部分はどうでしょうか。

このような作業には **agent skill** が適しています。スキルは、こうした操作を正しい方法で行うよう Copilot に伝えます。

このレッスンでは、既存の `quality-checks` スキルを確認し、結果の形式を調整し、スキルを再読み込みして実行します。

## シナリオ

Tailspin Toys はユニット テスト、lint、型チェックに `quality-checks` スキルを使っています。チームは、結果を読みやすくするためレポートを改善したいと考えています。

## 指示、スクリプト、リソース

Agent skill は、再利用可能なタスクの指示、実行可能なスクリプト、補助リソースをまとめ、必要なときにエージェントが読み込みます。基本となる構成は、スキル名のフォルダーと、その中の `SKILL.md` です。Markdown には、スキルの名前と説明を定義する frontmatter、処理の概要、呼び出すタイミングのガイダンスを記載します。必要に応じて、スクリプトやほかのリソースを含むサブフォルダーを追加できます。

> [!NOTE]
> スキルに追加のフォルダーやファイルは必須ではありません。Tailspin Toys の `quality-checks` スキルは、プロジェクトにあるコマンドを使うため、`SKILL.md` のみで構成されています。

スキルは、チームで共有・再利用するためにプロジェクトの `.github/skills` に置くことも、ユーザー用の `~/.copilot/skills` に置くこともできます。

## スキルを確認する

1. Codespace に戻り、Codespaces エディターで `.github/skills/quality-checks/SKILL.md` を開きます。
2. 先頭にある `name` と `description` を読みます。description は Copilot がスキルを呼び出すタイミングを判断するために使います。
3. テストと lint の手順を Copilot に伝える指示を確認します。
4. まだ **Results output formatting** セクションがないことを確認します。

## 変更前にスキルを実行する

1. Interactive モードでフィルターの会話に戻ります。
2. 次のプロンプトを送信し、3 つのチェックを実行します。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. 最後に表示されるレポートを確認します。

## レポートを調整する

どのコマンドを実行したか、成功したか、ツールがどのような結果を返したかを明確にするため、スキルにレポート形式を追加します。

1. `.github/skills/quality-checks/SKILL.md` を開きます。
2. ファイルの最後に次のセクションを追加します。

   ```markdown
   ## Results output formatting

   Upon completion, report each command that ran and whether it passed, failed, or was blocked. Include test counts, durations, errors, warnings, and other metrics only when the tool reports them. Identify the next action for any failure or blocker, and never describe a skipped or incomplete check as passed.
   ```

3. ファイルを保存します。

## 更新したスキルを実行する

Copilot CLI は、会話を再起動せずに編集済みのスキルを再読み込みできます。

1. 次のコマンドを入力します。

   ```plaintext
   /skills reload
   ```

2. 先ほどと同じプロンプトを送信します。

   ```plaintext
   Run the quality-checks skill for unit tests, lint, and type checks.
   ```

3. レポートを確認し、最初の結果と比較します。

## まとめと次のステップ

既存の agent skill を調整して実行しました。変更はフィルター機能の PR に含めます。次は [Playwright MCP サーバー][next-lesson]を使い、Copilot にサイトを直接操作させます。

## スキルの例

以下のコミュニティの例は参考資料であり、追加の作業項目ではありません。

- [Agent Skills 仕様][skill-spec]
- [コントリビューション ワークフロー: `make-repo-contribution`][contribution-example]
- [要件ドキュメント: `prd`][prd-example]
- [図とエクスポート スクリプト: `drawio`][drawio-example]
- [ブラウザー テスト: `webapp-testing`][browser-example]

[previous-lesson]: ../4-custom-instructions/
[next-lesson]: ../6-mcp-playwright/
[skill-spec]: https://agentskills.io/specification
[contribution-example]: https://github.com/github/awesome-copilot/tree/main/skills/make-repo-contribution
[prd-example]: https://github.com/github/awesome-copilot/tree/main/skills/prd
[drawio-example]: https://github.com/github/awesome-copilot/tree/main/skills/drawio
[browser-example]: https://github.com/github/awesome-copilot/tree/main/skills/webapp-testing
