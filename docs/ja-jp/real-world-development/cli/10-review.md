---
title: "レッスン 10 - まとめと次のステップ"
description: "Copilot CLI のワークフロー、2 つのプルリクエスト、再利用可能なカスタマイズ、追加リソースを振り返ります。"
authors:
  - geektrainer
lastUpdated: 2026-09-29
---

Tailspin Toys の一連のワークフローで GitHub Copilot CLI を使いました。

- Codespace を準備し、Copilot CLI をインストールして、プロジェクトと用意されたフィルター issue を確認しました。
- 星評価を追加し、転送されたブラウザーで確認して、最初のプルリクエスト (PR) を手動でマージしました。
- フィルター issue から始め、Plan モードで方針を決め、Autopilot モードで構築し、Interactive モードでレビューしました。
- カスタム指示でエージェントを案内し、既存の `quality-checks` スキルを調整して、ユニット テスト、lint、型チェックを実行しました。
- Playwright Model Context Protocol (MCP) サーバーを追加し、実際のブラウザーでフィルターを確認しました。
- quality assurance (QA) カスタム エージェントを作成して選び、要件、テスト範囲、スキルの結果、ブラウザーでの検証を確認しました。
- フィルターの変更をまとめてレビューし、Agent Merge を使って PR をマージしました。
- コンテキスト、モデル、共有、cloud agent への任意の委任に使うスラッシュ コマンドを確認しました。

## リリースしたもの

ワークショップでは、更新済み `main` からそれぞれ独立したブランチを作り、2 つの PR を作成しました。

1. **星評価**: ゲーム カードに既存の `starRating` と未評価状態を表示します。
2. **フィルターと品質ワークフロー**: フィルターを実装し、指示を更新・適用し、`quality-checks` のレポートをカスタマイズし、QA プロファイルと関連テストを追加します。

フィルターを計画して PR を作成するまで、同じ会話とブランチを使いました。ワークショップを簡潔にするため、この作業を 1 つの PR にまとめています。

## 異なる方法で検証する

自動テスト、自分で行うブラウザー確認、MCP を通じた Copilot のブラウザー操作でコードを確認しました。`quality-checks` スキルは、ユニット テスト、lint、型チェックを新しい形式で報告します。QA エージェントは要件とテスト範囲の確認にこれらの結果を組み合わせました。

追加テストは実際の不足を補うものであるべきです。QA 実行で新しいテストが不要と判断される場合もあります。マージを許可する前にコードと根拠を確認し、変更後は必要な検証を再実行してください。

## ベスト プラクティス

Copilot に与えるコンテキストやツールが作業に影響します。このワークショップでは、指示の更新、スキルの調整、QA プロファイルの作成、MCP サーバーの設定を行いました。これらのカスタマイズは会話をまたいで再利用し、チームのニーズに合わせて調整できます。指示は標準を、スキルは繰り返し実行する作業を、カスタム エージェントは専門的な役割を定義します。MCP サーバーは外部ツールに接続します。エージェントの要約だけでなく、実際の変更とツールの結果を確認してください。

タスクに合わせて **モードとモデル** を選びます。構築前に方針を決めるには **Plan**、範囲の小さな変更を対話しながら進めるには **Interactive**、明確なタスクを任せるには **Autopilot** を使います。定型的な編集には高速なモデル、複雑な作業には高性能なモデルを選びます。

コンテキストは、インフラストラクチャと同じくらい重要です。何を、なぜ、どのように作るかを明確に伝えると、出力が大きく変わります。

## さらに試す

- `/review` でコード レビュー エージェントに変更を分析させます。
- `/rubber-duck` で問題を説明し、別の観点を得ます。
- `/fleet` で独立したサブタスクを並行して調整します。
- `/worktree` で別のタスクを分離します。
- `/delegate` で Copilot cloud agent にタスクを送信します。

## 次のステップ

ツールの使い方を上達させるには、継続して使うことが大切です。本番コード、個人プロジェクト、作ってみたい小さなアプリなどで試し、チームと学びを共有してください。

ターミナルから Tailspin Toys を拡張する場合は、オプションの [Foundry Backer Concierge シリーズ][foundry]に進みます。別の環境については、[VS Code ワークショップ][vscode]、[GitHub Copilot app ワークショップ][app]、[Copilot cloud agent ワークショップ][cloud]を確認してください。

## リソース

- [GitHub Copilot CLI について][about-cli]
- [Copilot CLI コマンド リファレンス][cli-reference]
- [Copilot CLI をカスタマイズする][customize-cli]
- [Copilot CLI でプルリクエストを管理する][manage-prs]

[previous-lesson]: ../9-cli-power-tools/
[foundry]: ../8-foundry-agent/
[vscode]: ../../vscode/
[app]: ../../app/
[cloud]: ../../cloud/
[about-cli]: https://docs.github.com/copilot/concepts/agents/about-copilot-cli
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[customize-cli]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot
[manage-prs]: https://docs.github.com/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests
