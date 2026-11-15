---
title: "レッスン 9 - GitHub Copilot CLI のスラッシュ コマンド"
description: "コンテキスト、モデル、セッション共有、cloud agent への任意の委任に使うスラッシュ コマンドを確認します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

GitHub Copilot CLI には、操作、詳細情報、追加設定に使う多くのスラッシュ コマンドがあります。これまで `/diff`、`/mcp`、`/skills`、`/agent`、`/pr` を使いました。ここでは、ほかの便利なコマンドを確認します。

このレッスンでは、`/context` と `/compact` で会話コンテキストを確認し、`/model` でモデルを調べ、`/share` でセッションを共有し、並列作業、worktree、cloud agent への委任に使う任意のコマンドを確認します。

## Copilot CLI のコンテキストを確認する

大きなタスクでは、モデルのコンテキスト ウィンドウの上限に近づくことがあります。Copilot CLI は必要に応じて会話を自動的に圧縮します。スラッシュ コマンドで確認や圧縮もできます。

1. Codespace に戻り、リポジトリのルートで Copilot CLI を起動します。
2. `/context` を入力します。
3. モデル、現在のトークン使用量、システム指示・ツール・メッセージ・空き容量へのコンテキストの配分を確認します。
4. `/compact` を入力して会話を圧縮します。
5. もう一度 `/context` を入力して比較します。会話が短い場合は大きな違いがないこともあります。

> [!NOTE]
> コンテキスト ウィンドウが埋まると、Copilot CLI は自動的にコンテキストを圧縮します。タイミングを指定する場合は `/compact` を使います。関係のない別タスクを始める場合は、`/clear` または `/new` で新しい会話を始めます。

## モデルを選ぶ

モデルごとに得意分野が異なります。Copilot CLI で利用可能なモデルを確認して選びます。

1. `/model` を入力します。
2. 利用可能なモデルと使用量の情報を確認します。
3. 現在のモデルを使うか、別のモデルを選ぶか、<kbd>Esc</kbd> で一覧を閉じます。

## セッションを共有する

`/share` は、セッションを Markdown または HTML ファイルにエクスポートしたり、共有可能なリンクを作成したり、GitHub gist として公開したりできます。

1. `/help` を入力し、インストール済みバージョンの `/share` オプションを確認します。
2. 共有する場合は、たとえばローカル Markdown に保存する `/share file` など、目的に合う方法を選びます。
3. エクスポートにはプロンプト、応答、プロジェクトの詳細が含まれる場合があります。送信または公開する前に内容を確認してください。

リンクや gist の公開は任意です。チームが共有を意図していないリポジトリや会話の内容を公開しないでください。

## 省略可能: 作業を拡張または委任する

Copilot CLI には、大きなタスクに使える次のコマンドもあります。

- `/fleet` は独立したサブタスクをサブエージェントに分割し、並列で実行できます。
- `/worktree` は別のタスク用に独立した Git worktree を作成できます。
- `/delegate` はタスクを Copilot cloud agent に送信します。cloud agent は非同期に作業し、プルリクエストを作成する場合があります。

これらのコマンドは追加の worktree やリモート作業を作成するため、任意の操作です。試す場合は、範囲の明確な新しいタスクから始め、通常のワークフローで結果をレビューしてください。非同期エージェントの作業について詳しく知りたい場合は、[cloud agent ワークショップ][cloud-workshop]に進んでください。

## まとめと次のステップ

スラッシュ コマンドを使って Copilot CLI を設定し、セッションを共有し、内部の状況を確認しました。ほかのコマンドもあります。次は[学んだことと次のステップを振り返り][next-lesson]ます。

## リソース

- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI のコンテキスト管理][context-management]
- [Copilot cloud agent について][about-cloud-agent]

[previous-lesson]: ../8-create-pull-request/
[next-lesson]: ../10-review/
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[context-management]: https://docs.github.com/copilot/concepts/agents/copilot-cli/context-management
[about-cloud-agent]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-workshop]: ../../cloud/
