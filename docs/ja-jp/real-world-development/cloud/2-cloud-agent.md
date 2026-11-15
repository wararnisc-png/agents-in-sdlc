---
title: "演習 2 - GitHub Copilot cloud agent"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

| [← 前のレッスン: カスタム指示][previous-lesson] |
|:--|

多くの組織が技術的負債を抱えています。未解決のセキュリティ問題、更新が必要なレガシー コード、バックログに残ったままの機能リクエストなどです。GitHub Copilot cloud agent は、コードの更新や機能追加などを自律的に行います。作業が終わると、人がレビューできるドラフト PR を作成します。

この演習では、次の操作を行います。

- コード生成環境をカスタマイズします。
- 安全に作業を行う方法を確認します。
- issue の範囲を明確にする重要性を学びます。
- issue を Copilot に割り当てます。

## シナリオ

Tailspin Toys には、対応したい技術的負債があります。最初のサイトを作った請負業者が残したドキュメントの状態は理想的ではなく、実際にはほとんどありません。まず、アプリケーションのすべての公開関数に TSDoc doc comment を追加します。

さらに、デザイン チームはゲームを見つけやすくしたいと考えています。各ゲームの詳細ページに同じカテゴリの別タイトルを表示し、訪問者がゲームを見続けられるようにします。まだ完成度の高い実装は必要なく、UX の受け入れテストに使えるものを求めています。この作業はブロッカーですが、現時点では優先度の高い issue がほかにあります。

どちらも優先度が下がりやすく、Copilot cloud agent に割り当てるのに適した作業です。cloud agent が非同期に取り組む間、開発者は別の作業に集中できます。その後、戻って成果をレビューし、期待どおりであることを確認します。

## GitHub Copilot cloud agent について

[GitHub Copilot cloud agent](https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent#overview-of-copilot-cloud-agent-formerly-copilot-coding-agent) は、人間の開発者と同様にバックグラウンドで作業します。[GitHub issue を Copilot に割り当てる](https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions)と、Copilot は進行状況を追跡するドラフト プルリクエストを作成し、環境を準備して作業を開始します。作業中または完了後にセッションを確認でき、レビューの準備ができるとプルリクエストで通知されます。

## 範囲を明確にした指示の重要性

GitHub Copilot によって、考える作業がなくなるわけではありません。単純に見える作業にも複雑さがあります。[cloud agent に依頼するタスクの範囲][cloud-agent-best-practices]を明確にし、AI ペア プログラマーとして扱ってください。作業を段階に分け、学びながら試して調整します。生成 AI を使っても、ソフトウェア開発の基本は変わりません。

## このリポジトリのカスタム指示

前の演習では、カスタム指示と Copilot への影響を確認しました。カスタム指示の演習をすでに完了していれば `.github/copilot-instructions.md` を実際に確認しています。まだの場合は、今のうちに簡単に目を通してください。cloud agent に作業を割り当てる前に、このリポジトリに含まれる指示ファイルを読み取り専用で確認すると、後から指示の影響を見つけやすくなります。

- `.github/copilot-instructions.md` の **Code standards** セクションで、TypeScript の規約と TSDoc doc comment の要件を確認します。
- `.github/instructions/unit-tests.instructions.md` の `applyTo` frontmatter を確認します。この指示は `**/*.test.ts` に適用されます。

次のセクションで `Code lacks documentation` issue を cloud agent に割り当てるとき、生成された PR に TSDoc doc comment、TypeScript の規約、コメント ヘッダーがあるか確認してください。これらの内容は指示ファイルに基づいています。後の演習で PR をレビューするときにも、もう一度確認します。

## Copilot cloud agent の開発環境を設定する

コードを作成するには、誰が作業する場合でも、通常は環境の準備とセットアップ スクリプトの実行が必要です。ソフトウェア エンジニアと同じように作業する Copilot にタスクを割り当てる場合も同様です。

cloud agent は作業時に [GitHub Actions][github-actions] を使います。`.github/workflows/copilot-setup-steps.yml` に設定する[セットアップ ワークフロー][setup-workflow]を作成すると、作業を始める前に必要な開発ツールや依存関係を準備できます。このラボには、単一の Astro アプリ向けに Node.js、プロジェクトの依存関係、エンドツーエンド テスト用のブラウザー バイナリ、マイグレーションとシードを適用した SQLite データベースを用意するワークフローがあらかじめ設定されています。

```yaml
name: "Copilot Setup Steps"

# リポジトリの "Actions" タブからセットアップ手順をテストできます。
on: workflow_dispatch

env:
  ASTRO_TELEMETRY_DISABLED: "1"

jobs:
  copilot-setup-steps:
    runs-on: ubuntu-latest
    # *手順*に必要な最小限の権限を設定します。Copilot の操作には専用のトークンが使われます。
    permissions:
      # 依存関係のインストールなど、セットアップ手順の一部としてリポジトリを複製する場合は `contents: read` 権限が必要です。複製しない場合は、手順の完了後に Copilot が自動的に複製します。
      contents: read
    steps:
      - name: Checkout code
        uses: actions/checkout@v5

      # フロントエンド / アプリのセットアップ - Node.js (アプリ全体は Astro + Drizzle/libSQL)
      - name: Set up Node.js
        uses: actions/setup-node@v6
        with:
          node-version: "lts/*"
          cache: "npm"
          cache-dependency-path: "./package-lock.json"

      - name: Install JavaScript dependencies
        run: npm ci

      - name: Install Playwright browsers
        run: npx playwright install --with-deps chromium

      # ビルドとテストでデータを使えるように、ローカル SQLite データベースをマイグレーションしてシードします。
      - name: Set up the database
        run: npm run db:setup
```

通常の GitHub ワークフロー ファイルと同様ですが、重要な点がいくつかあります。

- `copilot-setup-steps` という 1 つのジョブがあり、Copilot がプルリクエストの作業を始める前に GitHub Actions で実行されます。
- `workflow_dispatch` トリガーがあるため、リポジトリの **Actions** タブからワークフローを手動実行できます。Copilot が起動するのを待たずに、正常に実行されるかテストできます。

## コードのドキュメントを追加する

ドキュメントの重要性は広く理解されていますが、多くのプロジェクトでは情報が古かったり、まったくなかったりします。この種の技術的負債が放置されると、生産性が低下し、コードベースの保守や新しい開発者の参加が難しくなります。幸い、Copilot はドキュメントの作成が得意です。Copilot cloud agent に割り当てるのにぴったりの issue です。バックグラウンドで必要なドキュメントを作成します。後の演習で成果をレビューします。

1. 新しいブラウザー タブで github.com のリポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい issue のダイアログを開きます。
4. **Blank issue** を選択して issue を作成します。
5. **Title** に `Code lacks documentation` と入力します。
6. **Description** に次のテキストを入力します。

    ```plaintext
    Our organization has a requirement that functions and methods include TSDoc doc comments where helpful. Unfortunately, recent updates haven't followed this standard. We need to update the existing code to ensure doc comments are included where they clarify behavior.
    ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して割り当て画面を開きます。

    ![Copilot を issue に割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

    ![Copilot の割り当て詳細](../../../_images/ex4-assign-copilot-details.png)

10. **Pull Requests** タブを選択します。
11. 新しく作成されたプルリクエスト (PR) を開きます。タイトルは `[WIP]: Code lacks documentation` のようになります。新しい PR が一覧に表示されない場合は、1、2 分待ってからブラウザーを更新します。
12. 数分後、Copilot が todo リストを作成したことを確認します。

> [!NOTE]
> Copilot の todo リストが PR に表示されるまで数分かかることがあります。Copilot は環境を準備し (前述のワークフローを実行)、プロジェクトを分析して、問題に取り組む最善の方法を決めています。

13. todo リストを確認し、Copilot が実行するタスクを確認します。
14. プルリクエストのタイムラインを下にスクロールし、Copilot が issue の作業を開始したことを示す更新を探します。
15. **View session** ボタンを選択します。

    ![Copilot セッションの表示](../../../_images/ex4-view-session.png)

> [!CAUTION]
> 更新された表示を確認するため、ブラウザーを更新する必要がある場合があります。

16. ライブ セッションをスクロールして、Copilot が問題を解決する様子を確認します。コードを調査して状態を理解し、計画を考えて適切な進め方を決め、コードを作成する様子を確認できます。

作業には数分かかることがあります。cloud agent の主な目的は、非同期に作業して開発者が別のタスクに集中できるようにすることです。別の作業を依頼してからアプリの機能開発を進めます。

通常、この作業には数分かかります。cloud agent の主な目的の 1 つは、開発者が別の作業に集中できるよう非同期にタスクを実行することです。この利点を活用して、もう 1 つのタスクを cloud agent に割り当て、その間にアプリへ機能を追加するコードを書きます。

## ゲーム詳細ページに関連ゲームのセクションを追加する

すでに確認したように、GitHub Copilot cloud agent の大きな利点は、作業を分担できることです。デザイン チーム向けの関連ゲーム セクションの追加は長時間かからないかもしれませんが、その時間もほかの作業に使えます。Copilot cloud agent に依頼しましょう。

1. github.com でリポジトリを開きます。
2. **Issues** タブを選択します。
3. **New issue** を選択して、新しい issue のダイアログを開きます。
4. **Blank issue** を選択して空のテンプレートを使います。
5. **Title** に `Show related games on the game details page` と入力します。
6. **Description** に次の内容を入力します。

    ```markdown
    We want to help people discover more games by showing related games on each game's details page. The design team wants to explore the UX and do some acceptance testing. Our requirements are:

   - Add a data-access helper in `src/lib/` that returns other games in the same category as a given game, excluding that game
   - Show a "Related games" section on the game details page that uses the helper
   - Handle the case where a game has no related games
   - There should be unit tests created for the new helper
   - Before creating the PR, ensure all tests pass
    ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選択して割り当て画面を開きます。

    ![Copilot を issue に割り当てる画面](../../../_images/shared-assign-copilot.png)

9. **Assign** を選択します。

しばらくすると、issue の最初のコメントに 👀 が表示され、Copilot が作業中であることがわかります。

![Copilot が issue に取り組んでいることを示す目の絵文字](../../../_images/ex4-issue-eyes-emoji.png)

Copilot は 2 つ目の依頼にも取り組んでいます。cloud agent はソフトウェア エンジニアと同じように動くため、作業中ずっと監視する必要はなく、完了してからレビューできます。ここでカスタム エージェントの作成と使用に取り組みましょう。

## まとめと次のステップ

[GitHub Copilot cloud agent][copilot-agents] に issue を割り当て、技術的負債の解消、新機能の作成、フレームワーク間のコード移行などを非同期で依頼する方法を確認しました。環境のカスタマイズ、安全な作業、明確な issue の範囲についても学びました。

次はカスタム エージェントを作成して使います。cloud agent は [MCP サーバー][cloud-agent-mcp]とカスタム指示も利用できます。

## リソース

- [Copilot cloud agent について][copilot-agents]
- [GitHub issue を Copilot に割り当てる][assign-issue]
- [Copilot cloud agent セットアップ ワークフローのベスト プラクティス][cloud-agent-best-practices]

| [次のレッスン: カスタム エージェント →][next-lesson] |
|--:|

[previous-lesson]: ../1-custom-instructions/
[next-lesson]: ../3-custom-agents/
[cloud-agent-mcp]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/extend-cloud-agent-with-mcp
[assign-issue]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/start-copilot-sessions
[setup-workflow]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[copilot-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-cloud-agent
[cloud-agent-best-practices]: https://docs.github.com/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/customize-the-agent-environment
[github-actions]: https://docs.github.com/actions
