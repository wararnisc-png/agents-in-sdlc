---
title: "レッスン 3 - エージェント モード: Plan と Autopilot"
description: "Plan で方針を合意し、Autopilot で issue からフィルターを構築して、Interactive モードで結果をレビューします。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

小さな機能を追加したら、次はより大きな変更に取り組みます。GitHub Copilot CLI は既存の開発フローに沿って作業できます。このレッスンでは、issue から新機能を作り、コードを検証し、動作を確認して、プロジェクトにマージするまでのエージェント主導の開発を始めます。

> [!NOTE]
> 機能開発を続ける間、同じ会話とブランチを使います。通常はファイル種別ごとに別のブランチや PR を使う場合もありますが、ここでは主な概念に集中するため手順を簡略化します。

このレッスンでは、GitHub issue から会話を始め、Plan モードで要件を決め、Autopilot モードで機能を実装し、コードをレビューして転送ブラウザーで手動検証します。その後、リポジトリの指示、`quality-checks` スキル、MCP 検証、QA エージェントを追加して機能の PR を作ります。

## シナリオ

Tailspin Toys のカタログが増え、カテゴリと出版社でゲームを絞り込む必要があります。バックログの issue には概要がありますが、複数カテゴリを組み合わせるなど、実装前に合意が必要です。Plan モードで方針を決めてから、範囲を限定して Autopilot に実装を許可します。

## 背景

AI コーディング エージェントを開発フローに導入しても、基本は変わりません。一般的な流れは次のとおりです。

1. 作業内容を記載した issue から始めます。
2. 実装計画を立てます。
3. コードを作成してレビューします。
4. テストを実行します。
5. 新機能を手動で検証します。
6. プルリクエスト (PR) を作成します。
7. レビューと継続的インテグレーションが成功したら、コードをマージします。

## 会話モード

**会話モード**は、エージェントにどの程度の自律性を与えるかを制御します。<kbd>Shift</kbd>+<kbd>Tab</kbd> で切り替えます。

- **Interactive**: エージェントが変更を提案し、次に進む前に入力を待ちます。
- **Plan**: エージェントが計画を作成します。プロジェクト ファイルは編集できません。
- **Autopilot**: エージェントがコードを作成し、テストを実行して、タスクが完了するまで自律的に改善します。

まず Plan モードで計画をレビューし、その後 Autopilot で実装します。

## issue から開始する

1. Codespace に戻り、星評価の PR がマージ済みであることを確認します。
2. `main` を更新し、フィルター用ブランチを作成します。

   ```bash
   git checkout main
   git pull --ff-only
   git checkout -b game-filters-cli
   ```

3. Copilot CLI を起動します。

   ```bash
   copilot --yolo
   ```

4. <kbd>Tab</kbd> を 2 回押して **Issues** タブを開きます。
5. <kbd>A</kbd> を押してすべての issue を表示し、矢印キーで **Allow users to filter games by category and publisher** を選びます。
6. <kbd>C</kbd> を押して issue をプロンプトに追加し、**Session** タブに戻ります。プロンプトには `#7` のような番号が含まれます。

## フィルター機能を計画する

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して **Plan** モードに切り替えます。
2. issue の参照に続けて次のプロンプトを入力します。

   ```plaintext
   Create a plan for implementing this feature.
   ```

3. フィルターの動作について質問されたら、希望する仕様を回答します。
4. 計画が完成したら、<kbd>Control</kbd>+<kbd>E</kbd> (Mac) または <kbd>Ctrl</kbd>+<kbd>E</kbd> (Windows/Linux) を押して展開し、内容を確認します。
5. 決めた仕様と異なる部分があれば、Copilot に修正を依頼します。

## Autopilot を承認する

1. **Accept plan and build on autopilot (recommended)** または同等の項目を選択します。
2. プロンプトの下に **Autopilot** が表示されていることを確認します。
3. Copilot が計画に沿ってコードを作成し、テストを実行する様子を確認します。

> [!NOTE]
> 承認すると、すぐに実装が始まることがあります。必ず計画を先に確認してください。依存関係が不足している場合やポートが競合する場合は、チェック完了と判断する前に環境の問題を解決します。

## 実装をレビューして検証する

1. <kbd>Shift</kbd>+<kbd>Tab</kbd> を押して Interactive モードに切り替えます。
2. `/diff` を入力し、フィルターの実装とテストを確認します。
3. issue と計画時の決定に沿っていることを確かめます。
4. <kbd>Esc</kbd> を押して差分表示を終了し、チェックの結果を確認します。失敗があれば修正を依頼します。

## 新機能を試す

1. Copilot に次のプロンプトを送り、アプリを起動します。

   ```plaintext
   Start the app so I can try the filtering feature in my browser. Tell me the URL and leave the server running.
   ```

2. ポート `4321` が利用可能になったら **Open in Browser** を選択します。
3. 計画で決めたカテゴリと出版社のフィルター、組み合わせ、リセット、結果なしの動作を確認します。
4. Codespace に戻り、Copilot が起動した開発サーバーを停止するよう依頼します。

## まとめと次のステップ

GitHub issue から会話を始め、Plan モードで要件を決め、Autopilot で実装し、コードをレビューしてブラウザーで手動検証しました。次は[カスタム指示を使って][next-lesson]、コードが文書化された規約に従うようにします。

## リソース

- [GitHub Copilot CLI の Autopilot][autopilot]
- [Copilot CLI コマンド リファレンス][cli-reference]

[autopilot]: https://docs.github.com/copilot/concepts/agents/copilot-cli/autopilot
[cli-reference]: https://docs.github.com/copilot/reference/copilot-cli-reference/cli-command-reference
[previous-lesson]: ../2-add-star-rating/
[next-lesson]: ../4-custom-instructions/
