---
title: "演習 5 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

[← 前のレッスン: カスタム エージェント][previous-lesson]

Copilot を agent mode で使うと、コードベースの調査、変更の提案、ファイルの編集、コマンドの実行を自律的に行います。VS Code の Copilot Chat では、ツール呼び出しやファイル編集を確認し、差分を受け入れるか取り消すかを選び、追加プロンプトで作業を案内できます。

この演習では、アクセシビリティ エージェントの作業をリアルタイムで監視し、変更をレビューして受け入れ、進行中のセッションにライト モードを追加するよう依頼します。

## シナリオ

[演習 4][previous-lesson]で使ったアクセシビリティ エージェントがハイ コントラスト モードを実装しています。作業中にデザイン チームからライト モードの追加依頼がありました。新しい会話を始めず、同じセッションに追加の指示を送ります。

## Copilot の進行状況を監視する

Copilot Chat には、エージェントが確認したファイル、実行したコマンド、提案した編集が表示されます。編集の差分には **Keep** と **Undo** の操作があります。

1. 演習 4 で使った Copilot Chat ビューに戻ります。
2. ツール呼び出し、ファイルの読み取り・編集、ターミナル コマンドを確認します。
3. **Keep** を選ぶと変更を受け入れ、**Undo** を選ぶと取り消して再度試せます。
4. チャット上部の **Files changed** を開き、セッションで変更されたファイルを確認します。
5. ハイ コントラスト モードの実装が完了し、変更の概要が表示されるまで待ちます。

> [!NOTE]
> ターミナル コマンドなどで許可が必要な場合、エージェントは一時停止して **Allow** を表示します。内容を確認し、許可してもよいコマンドだけ承認してください。

## ライト モードを追加するようエージェントに依頼する

同じ会話を続けると、エージェントは前の作業内容、変更したコンポーネント、スタイル、local storage の使い方を保持しています。

1. Copilot Chat の入力欄に次のプロンプトを送信します。

    ```plaintext
    Nice work! Now add a light-mode toggle alongside the high-contrast toggle. Light mode should follow the same pattern — persist via local storage and be accessible from the same area of the UI. The user should be able to enable high-contrast and light mode independently.
    ```

2. エージェントが既存の変更を確認し、ライト モードの追加を提案する様子を確認します。
3. 各差分をレビューし、**Keep** または **Undo** を選びます。
4. 作業が意図と異なる場合は、入力欄の横にある **Stop** で止め、補足のプロンプトを送ります。

> [!TIP]
> セッション中の追加指示は、最初からやり直すより効率的です。「CSS を簡潔にして重複する selector ではなく CSS 変数を使う」「3 つ目の toggle を追加せず、既存の設定パネルにライト モードを統合する」などと依頼できます。

## 作業内容をレビューする

1. VS Code の **Source Control** ビューを開きます。
2. 変更されたファイルの一覧を確認します。
3. いくつかの差分を開き、ARIA 属性、キーボード操作、セマンティック HTML、local storage による設定の保持などを確認します。
4. 問題がなければ、Source Control パネルから変更をステージしてコミットします。次のレッスンで公開します。

## まとめと次のステップ

Copilot Chat agent mode のセッションを監視し、各ファイルの編集をレビューし、変更を受け入れるか取り消すか選び、追加プロンプトで作業を広げる方法を学びました。次はアクセシビリティの変更をプルリクエストとして公開します。

## リソース

- [VS Code の Copilot Chat][copilot-chat-vscode]
- [agent mode の使用][agent-mode]

---

| [← 前のレッスン: カスタム エージェント][previous-lesson] | [次のレッスン: Copilot の作業を改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../4-custom-agents/
[next-lesson]: ../6-iterating/
[copilot-chat-vscode]: https://code.visualstudio.com/docs/copilot/chat/copilot-chat
[agent-mode]: https://code.visualstudio.com/docs/copilot/chat/chat-agent-mode
