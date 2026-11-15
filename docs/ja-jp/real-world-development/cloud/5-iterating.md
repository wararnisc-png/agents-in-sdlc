---
title: "演習 5: GitHub Copilot の作業を反復して改善する"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

## 作業をレビューする

### シナリオ

このラボでは、コードへのドキュメント追加、関連ゲーム機能の実装、ハイ コントラストとライト モードを含むアクセシビリティ機能を Copilot に依頼しました。コードの変更を確認し、必要に応じてフィードバックを送ります。

ここで何度も確認したとおり、生成 AI を使ってもソフトウェア設計と DevOps の基本は変わりません。生成されたコードをレビューし、通常の DevOps プロセスに沿って進めます。チーム全体のレビューを有効にする前に、ドキュメント、関連ゲーム、アクセシビリティ機能のプルリクエストを確認します。

## セキュリティと GitHub Copilot cloud agent

Copilot cloud agent は非同期に動作するため、安全性を保つための制約があります。

- Copilot はリポジトリへの読み取りアクセスを持ち、書き込みは作業用ブランチに限られます。
- cloud agent は GitHub Actions 内に一時的な環境を作成して実行されます。
- GitHub Actions ワークフローの実行には、人による承認が必要です。
- [外部リソースへのアクセス][agent-firewall]は、MCP サーバーを含め、既定で制限されています。

## 生成されたドキュメントをレビューする

最初に、GitHub Copilot cloud agent がコードにドキュメントを追加した最初のプルリクエスト (PR) を、GitHub.com の標準的な PR インターフェイスで確認します。

> [!NOTE]
> PR に GitHub Copilot がファイアウォールでブロックされたという警告が表示されることがあります。Copilot は外部リソースへのアクセスが既定で制限されているため、これは想定された動作です。必要であれば、[cloud agent のファイアウォールをカスタマイズまたは無効化][agent-firewall]できます。

1. github.com でリポジトリを開きます。
2. **Pull Requests** を選択して、PR の一覧を開きます。
3. **Add missing documentation** またはそれに近いタイトルの PR を開きます。

> [!NOTE]
> Copilot がまだ作業中の場合、PR のタイトルに **[WIP]** が含まれます。その場合は作業の完了を待ってください。数分かかることがあります。その間に休憩したり、これまでに学んだことを振り返ったりできます。

4. PR の準備ができたら **Files changed** タブを選択し、変更をレビューします。

    ![Files changed タブ](../../../_images/shared-pr-files-changed.png)

5. 新たに更新されたコードを調べます。TSDoc doc comment やその他のドキュメントが追加されています。変更内容は状況によって異なります。

   TypeScript の規約、TSDoc doc comment、ファイル ヘッダーがあるかを確認してください。これらは演習 2 の最初に確認したカスタム指示ファイルから反映されています。

6. 更新内容をレビューして問題がなければ **Conversation** タブに戻り、下にスクロールします。
7. ワークフローが承認待ちであることを示す表示を探します。
8. ワークフローが承認待ちの場合は **Approve and run workflows** を選択します。

    ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. PR の checks セクションでワークフローがキューに入ったことを確認します。すべて問題なければ、単一 Astro アプリのプロジェクト チェックが成功します。完了まで数分かかる場合があります。

## GitHub Copilot に変更を依頼する

Copilot とプルリクエストで協力するときは、PR のコメントやコード上のインライン コメントでチーム メンバーと同じように `@copilot` を付けられます。Copilot はコメントを確認し、対応する新しいセッションを開始します。生成結果は確率的なため、必ずしも決まった文面で依頼できるわけではありません。次のような変更を依頼できます。

- 各コード ファイルの先頭に、ファイルの役割を簡潔に説明するコメント ヘッダーを追加する。
- TypeScript と Astro のファイルに TSDoc doc comment を追加する。
- Astro アプリの構成を説明する README を作成する。

1. 上記の例から選ぶか、コードベースに追加したいドキュメントについて別の提案を使い、`@copilot` を付けたコメントを追加して変更を依頼します。
2. **View Session** を選び、Copilot が作業する様子を確認します。Copilot は更新用の新しいセッションを開始します。
3. **Back to pull request** を選択して PR に戻ります。

    ![プルリクエストに戻る操作](../../../_images/ex7-back-to-pr.png)

4. Copilot の作業が完了すると、PR に新しいコミットが表示されます。
5. **Files changed** タブを選択し、変更をレビューします。

納得できるまで反復できます。準備ができたら、ドラフト PR をレビュー可能な状態にして `main` にマージします。

![PR をレビュー可能な状態にする操作](../../../_images/ex7-ready-for-review.png)

## 関連ゲーム機能をレビューする

ゲーム詳細ページに関連ゲームを表示する PR に戻ります。

1. github.com でリポジトリを開きます。
2. **Pull Requests** タブを選びます。
3. **Show related games on the game details page** などのタイトルの PR を選びます。
4. **Files changed** タブで生成されたコードをレビューします。
5. 更新内容をレビューして問題がなければ **Conversation** タブに戻り、下にスクロールします。
6. ワークフローが承認待ちであることを示す表示を探します。
7. ワークフローが承認待ちの場合は **Approve and run workflows** を選択します。

    ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

8. PR の checks セクションでワークフローがキューに入ったことを確認します。すべて問題なければ、単一 Astro アプリのプロジェクト チェックが成功します。完了まで数分かかる場合があります。
9. **省略可能:** Codespace でこのブランチに切り替えて、関連ゲーム機能を手動でテストすることもできます。Codespace に移動してターミナルを開き、次のコマンドを実行します。`<branch-name>` は Copilot が作成したブランチ名 (たとえば **copilot/fix-8**) に置き換えてください。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

Copilot は関連ゲーム機能を作成しました。前の PR と同様に、Copilot に更新を依頼して反復できます。たとえば、表示する関連ゲームの数を調整したり、カスタム指示の更新前に依頼したため含まれていないコメント ヘッダーや TSDoc doc comment を追加したりできます。前の PR と同じように **Conversation** タブにコメントを追加すると、Copilot が内容を確認して新しいセッションを開始します。

## アクセシビリティ機能をレビューする

カスタム アクセシビリティ エージェントを使って実装した機能をレビューします。この PR には、演習 3 で依頼したハイ コントラスト モードと、演習 4 で追加したライト モードが含まれます。

1. github.com でリポジトリを開きます。
2. **Pull Requests** タブを選択します。
3. **Add high contrast mode to website** またはそれに近いタイトルの PR を選びます。

> [!NOTE]
> Copilot がまだ作業中の場合、PR のタイトルに **[WIP]** が含まれます。作業が完了するまで待ってください。数分かかる場合があります。

4. **Files changed** タブを開き、生成されたコードをレビューします。
5. 実装を確認し、特に次の点に注意します。
   - モードを切り替える UI コンポーネント
   - ユーザー設定を保存する local storage の利用
   - ハイ コントラスト モードとライト モードの CSS またはスタイル
   - アクセシビリティ属性、キーボード操作、ARIA ラベル
   - モード切り替えを管理する JavaScript または TypeScript
6. 更新内容をレビューして問題がなければ **Conversation** タブに戻り、下にスクロールします。
7. ワークフローが承認待ちであることを示す表示を探します。
8. ワークフローが承認待ちの場合は **Approve and run workflows** を選択します。

    ![Approve and run workflows](../../../_images/shared-approve-workflows.png)

9. PR の checks セクションでワークフローがキューに入ったことを確認します。すべて問題なければ、単一 Astro アプリのプロジェクト チェックが成功します。完了まで数分かかる場合があります。
10. **省略可能:** Codespace で Copilot が作成したブランチに切り替え、アクセシビリティ機能を手動でテストします。Codespace でターミナルを開き、次のコマンドを実行します。`<branch-name>` は Copilot が作成したブランチ名に置き換えてください。

    ```bash
    git fetch origin
    git checkout <branch-name>
    ```

    アプリを起動し、ブラウザーでハイ コントラストとライト モードの切り替えを試します。ページを再読み込みしても設定が保持されることを確認してください。

カスタム アクセシビリティ エージェントが、アクセシビリティのベスト プラクティスに沿って機能を実装するよう Copilot を導いたことに注目してください。アクセシビリティ上の懸念や改善点があれば、前の PR と同様にコメントで `@copilot` に変更を依頼できます。

## 省略可能な演習 — 作業を継続して委任する

cloud agent は、現実のバックログ項目を任せて、その間に別の作業に取りかかると効果を発揮します。この習慣を身につけるために、リポジトリでいくつか issue を作成して Copilot に割り当ててみてください。例:

- ゲーム詳細ページに支援者向けの関心フォームを作成する。
- ゲーム一覧ページにページネーションを実装する。
- データアクセス ヘルパーに入力検証とエラー処理を追加する。

## まとめ

Cloud agent harness を完了しました。このレッスンでは、次の操作を行いました。

- このリポジトリに用意されたカスタム指示を確認し、cloud agent の出力への影響を確認しました。
- Copilot cloud agent に issue を割り当て、環境の準備、計画、非同期の実行を確認しました。
- アクセシビリティ用のカスタム エージェントを作成して使い、ハイ コントラスト モードとライト モードの切り替えを追加しました。
- Copilot agents ページをミッション コントロールとして使い、作業中のアクセシビリティ セッションを監視して案内しました。
- cloud agent のプルリクエストをレビューして改善し、`@copilot` で変更を依頼してワークフローを承認しました。

## レビューと次のステップ

この harness は完了です。引き続き学ぶ場合は、ほかの harness で Copilot Chat、MCP、Plan モード、Autopilot モードを試してください。

- **[VS Code harness](../../vscode/)** — VS Code で Copilot Chat の agent mode と MCP 統合を試します。
- **[CLI harness](../../cli/)** — Plan と Autopilot モード、agent skill、QA エージェント、Playwright MCP、Agent Merge、cloud agent への任意の `/delegate` を使い、ターミナルから変更を届けます。

自分のリポジトリで試せるアイデア:

- リファクタリングやテスト カバレッジの issue を cloud agent に割り当てる。
- 別の分野に特化したカスタム エージェントを作成する。
- 別の技術スタック向けに `copilot-setup-steps.yml` を設定する。

## リソース

- [GitHub Copilot][github-copilot]
- [Copilot agents について][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent セットアップ ワークフローのベスト プラクティス][cloud-agent-best-practices]
- [Copilot cloud agent ファイアウォールの設定][agent-firewall]

---

| [← 前のレッスン: エージェントの管理][previous-lesson] |
|:--|

[github-copilot]: https://github.com/features/copilot
[cloud-agent-overview]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[agent-firewall]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-firewall
[previous-lesson]: ../4-managing-agents/
