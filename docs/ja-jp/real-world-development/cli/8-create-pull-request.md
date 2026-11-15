---
title: "レッスン 8 - 機能の PR を作成してマージする"
description: "フィルター、指示、スキル、QA プロファイル、テストをまとめてレビューし、PR を作成して Agent Merge を使います。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

フィルターの実装、指示の更新、スキル、品質保証 (QA) プロファイル、テストが 1 つのブランチに保存されています。これらをまとめてレビューし、プルリクエストを作成します。星評価の PR は自分でマージしましたが、今回は **Agent Merge** にマージの作業を任せます。

> [!NOTE]
> 通常は機能、指示、スキル、QA エージェントを複数の PR に分けます。このワークショップでは手順を簡潔にするため、フィルターと品質ワークフロー全体を 1 つの会話とブランチにまとめています。

このレッスンでは、Agent Merge の概要、変更と検証結果の確認、フィルター PR の作成、レビュー後の Agent Merge の有効化を行います。

## シナリオ

Copilot を使ってフィルター機能を計画、実装、検証しました。Tailspin Toys は残りの PR 作業を自動化したいと考えていますが、マージを許可する権限は開発者が保持します。

## Agent Merge について

**Agent Merge** は、プルリクエストをマージ可能にするために必要な作業を自動化します。有効にすると、Copilot は CI チェックの失敗を修正し、レビュー コメントに対応し、必要に応じて rebase を行います。その後、リポジトリで許可されていれば GitHub の自動マージを有効にします。Agent Merge を有効にする前に、変更をレビューして準備ができていることを確認してください。

## Agent Merge で PR を管理する

1. Codespace に戻ります。
2. `/agent` を入力してエージェント ダイアログを開きます。
3. **Default** を選択して <kbd>Enter</kbd> を押します。
4. `/pr create` で PR を作成します。
5. `/pr agentmerge` で Agent Merge を有効にします。
6. Copilot が PR の CI を監視します。すべて成功すると、マージが実行されます。
7. `PR #14 was squash-merged successfully.` など、マージ成功を示すメッセージを確認します。

> [!IMPORTANT]
> Agent Merge は、必須の承認、ブランチ保護、マージ キュー、リポジトリ設定、権限不足を回避しません。ブロックされた場合は理由を確認し、リポジトリで許可されている場合はレビュー済み PR を手動でマージしてください。

## まとめと次のステップ

コードの生成、テストと検証、プルリクエストの処理を自動化しました。次は[Copilot CLI のスラッシュ コマンド][next-lesson]で、コンテキスト、モデル、共有、cloud agent への任意の委任を確認します。

## リソース

- [Copilot CLI でプルリクエストを管理する][manage-prs]
- [Copilot CLI コマンド リファレンス][cli-reference]

[previous-lesson]: ../7-qa-agent/
[next-lesson]: ../9-cli-power-tools/
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
