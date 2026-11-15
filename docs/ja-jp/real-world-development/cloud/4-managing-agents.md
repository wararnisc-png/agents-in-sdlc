---
title: "演習 4 - エージェントの監視と管理"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

これまでの演習で、Copilot cloud agent にユーザー体験の改善と機能追加に関する 3 つのタスクを依頼しました。cloud agent は非同期かつ自律的に作業しますが、進行状況を監視することも大切です。

GitHub.com の[エージェント ページ][agents-page]では、開いているプルリクエストがあるエージェント タスクを確認できます。作業内容を調べたり、進行中のセッションに追加の指示を送ったりできます。

この演習では、エージェント ページでタスクを監視し、実行中のセッションに追加機能を依頼します。

## シナリオ

ハイ コントラスト モードを作成するよう依頼した後、チームはライト モードも追加したいと考えました。エージェントの作業を案内して、両方のモードを実装します。

## Copilot cloud agent のタスクを確認する

1. [Copilot agents ページ](https://github.com/copilot/agents)を開きます。
2. メイン ペインと左ペインに表示されるタスクを確認します。コード ドキュメントの追加、ゲームを変更する API の生成、サイトのハイ コントラスト モードの追加などが表示されます。
3. 実行中のタスクを選択し、Copilot が行った操作を確認します。リポジトリのチェックアウト、環境の作成、MCP サーバーの設定、タスクを完了するための作業などが含まれます。

> [!NOTE]
> 表示される手順は、Copilot の作業状況や進め方によって異なります。

4. 右側のプルリクエスト (PR) ペインで、PR と変更ファイルを確認します。

## cloud agent に追加の指示を送る

ハイ コントラスト モードの実装中に、ライト モードも追加するよう依頼します。

1. ハイ コントラスト モードのセッションを選択します。タイトルは Copilot が付けた名前や作業状況によって異なります。

    ![ミッション コントロールのアクセシビリティ セッション](../../../_images/ex6-accessibility-session.png)

2. セットアップが完了して作業が始まるまで、セッションを数分確認します。
3. **Steer active session while Copilot is working** ダイアログに次のプロンプトを入力します。

    ```plaintext
    While we are working on a high contrast mode, let's also add a light mode. There should be a switch for this mode as well where users can select their desired display mode.
    ```

    ![Agents ページのセッション案内ダイアログ](../../../_images/ex6-steer-cloud-agent-task.png)

4. <kbd>Enter</kbd> を押してプロンプトを送信します。
5. Copilot が要求を受け取り、作業に追加したことを確認します。

## Copilot に作業を続けてもらう

Copilot は、メッセージを送信した時点で実行している手順を終えた後、新しい要求を作業に反映します。非同期作業が続く間に、これまでに学んだことを振り返りましょう。

## まとめと次のステップ

Copilot agents ページで cloud agent のタスクを監視し、進行中のセッションに追加機能を依頼しました。次は Copilot が作成したプルリクエストを[反復して改善します][next-lesson]。

## リソース

- [Copilot agents ページ][agents-page]
- [カスタム エージェントについて][custom-agents]

---

| [← 前のレッスン: カスタム エージェント][previous-lesson] | [次のレッスン: Copilot の作業を改善する →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-custom-agents/
[next-lesson]: ../5-iterating/
[agents-page]: https://github.blog/changelog/2025-07-03-agents-page-for-copilot-coding-agent-in-public-preview
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
