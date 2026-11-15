---
title: "演習 3 - カスタム エージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタム エージェントとは

GitHub Copilot の[カスタム エージェント][custom-agents-concept]は、開発ワークフローの特定のタスクや分野に合わせた AI アシスタントです。リポジトリの `.github/agents` フォルダーに Markdown ファイルを置き、指示、ベスト プラクティス、コーディング パターン、専門知識を定義します。たとえば、[WCAG][wcag] 準拠を確認するアクセシビリティ エージェント、セキュア コーディングを確認するセキュリティ エージェント、テスト パターンを守るテスト エージェントを作成できます。

カスタム エージェントは、プロジェクト内の `.github/agents` またはグローバルな `~/.copilot/agents` にある Markdown ファイルで定義します。各ファイルには `name` と `description` を含む YAML frontmatter と、エージェントの動作、専門知識、指示を記載する本文が必要です。

### カスタム エージェントと agent skill の違い

カスタム エージェントと [agent skill][agent-skills-concept] はどちらも、主に Markdown ファイルで定義し、AI に作業方法を伝えます。大まかには、**カスタム エージェントが作業者、スキルがツール**です。

カスタム エージェントは独自のコンテキスト ウィンドウを持ち、スキルやほかのエージェントを連携させます。この演習では、アクセシビリティ エージェントがサイトをガイドラインに照らして確認・更新します。その際、プルリクエスト作業やテスト実行を管理するスキルを呼び出すこともできます。

> [!NOTE]
> カスタム エージェントの作成に唯一の正解はありません。利用環境やシナリオに合わせて試し、改善してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

この演習では、次の操作を行います。

- カスタム エージェントの定義方法を確認します。
- カスタム エージェントにタスクを割り当てます。

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず、誰もがクラウドファンディング プラットフォームを使えるようにしたいと考えています。ユーザーから、背景色と文字色のコントラストが不十分で、現在のダーク テーマが読みにくいという意見が寄せられました。デザイン チームは、オン・オフを切り替えられるハイ コントラスト モードを求めています。アクセシビリティ エージェントを使って機能を実装します。

## アクセシビリティ用カスタム エージェントを確認する

アクセシビリティ用のカスタム エージェントはすでに作成されています。内容を確認して、Copilot をどのように案内するか理解します。

Codespace に戻り、エージェントのファイルを確認します。

1. `.github/agents/accessibility.md` を開きます。
2. `name` と `description` フィールドを含む YAML frontmatter を確認します。

> [!CAUTION]
> カスタム エージェントには `name` と `description` を含む frontmatter が必要です。

3. 続くセクションを確認します。
   - アクセシブルな Web サイト向けのコードを生成する際の主な責任。
   - アクセシビリティのベスト プラクティス。
   - HTML、CSS、JavaScript のコード例。
   - よくある問題や間違い。

## issue を作成して割り当てる

Copilot cloud agent にハイ コントラスト モードの実装を依頼します。

1. リポジトリに移動します。
2. **Issues** タブを選択します。
3. **New issue** を選択して新しい issue のダイアログを開きます。
4. **Blank issue** を選択します。
5. **Title** に `Add high contrast mode to website` と入力します。
6. **Description** に次を入力します。

    ```plaintext
    We need a high contrast mode for the site. There should be a toggle for high contrast which the user can set. It should store the setting in local storage on the browser.
    ```

7. **Create** を選択して issue を作成します。
8. 右側の **Assign to Copilot** を選んで割り当てダイアログを開きます。
9. 一覧から **Accessibility agent** を選択します。

    ![カスタム エージェントとして Accessibility を選択した cloud agent 割り当て画面](../../../_images/ex5-select-custom-agent.png)

10. **Assign** を選択します。
11. Copilot がバックグラウンドで作業を開始します。

## まとめと次のステップ

カスタム エージェントを使うと、チームの専門知識や標準を再利用できる形で定義し、Copilot の作業を特定のタスクに合わせられます。エージェント セッションを[監視して案内する][next-lesson]方法を次の演習で確認します。

## リソース

- [カスタム エージェントについて][custom-agents]
- [組織でカスタム エージェントを使うための準備][org-custom-agents]
- [エンタープライズでカスタム エージェントを使うための準備][enterprise-custom-agents]

---

| [← 前のレッスン: GitHub Copilot cloud agent][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../2-cloud-agent/
[next-lesson]: ../4-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[org-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-organization/prepare-for-custom-agents
[enterprise-custom-agents]: https://docs.github.com/copilot/how-tos/administer-copilot/manage-for-enterprise/manage-agents/prepare-for-custom-agents
