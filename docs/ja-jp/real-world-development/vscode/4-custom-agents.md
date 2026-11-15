---
title: "演習 4 - カスタム エージェント"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

## カスタム エージェントとは

GitHub Copilot の[カスタム エージェント][custom-agents-concept]は、開発ワークフローの特定のタスクや分野に合わせた AI アシスタントです。リポジトリの `.github/agents` にある Markdown ファイルで指示、ベスト プラクティス、コーディング パターン、専門知識を定義します。たとえば、[WCAG][wcag] 準拠を確認するアクセシビリティ エージェントや、セキュア コーディングを確認するセキュリティ エージェントを作成できます。

各ファイルには `name` と `description` を含む YAML frontmatter と、エージェントの動作、専門知識、指示を記載する本文が必要です。カスタム エージェントと [agent skill][agent-skills-concept] はどちらも AI に作業方法を伝えますが、大まかには **カスタム エージェントが作業者、スキルがツール**です。カスタム エージェントは独自のコンテキスト ウィンドウを持ち、スキルやほかのエージェントを連携させられます。

> [!NOTE]
> カスタム エージェントの作成に唯一の正解はありません。利用環境やシナリオに合わせて試し、改善してください。

[custom-agents-concept]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[agent-skills-concept]: https://docs.github.com/copilot/concepts/agents/about-agent-skills
[wcag]: https://www.w3.org/WAI/standards-guidelines/wcag/

## シナリオ

Tailspin Toys は、視覚能力や好みにかかわらず誰もが使えるクラウドファンディング サイトを目指しています。現在のダーク テーマは文字と背景のコントラストが不十分で読みにくいという意見を受け、デザイン チームは切り替え可能なハイ コントラスト モードを求めています。この演習では、アクセシビリティ用のカスタム エージェントを使って機能を実装します。

## アクセシビリティ用カスタム エージェントを確認する

アクセシビリティ エージェントはすでに作成されています。Codespace に戻り、アクセシビリティ用のブランチを `main` から作成します。演習 3 のフィルター PR とは分けて作業します。

```bash
git checkout main
git pull
git checkout -b accessibility-vscode
```

1. `.github/agents/accessibility.md` を開きます。
2. `name` と `description` を含む YAML frontmatter を確認します。

> [!CAUTION]
> カスタム エージェントには `name` と `description` を含む frontmatter が必要です。

3. アクセシブルなサイト向けの責任、ベスト プラクティス、HTML・CSS・JavaScript のコード例、よくある問題を確認します。

## Copilot Chat でカスタム エージェントを使う

VS Code の Copilot Chat では、`.github/agents` にあるカスタム エージェントをエージェントのドロップダウンから選択できます。

> [!TIP]
> **Copilot Chat を開く**
>
> Codespace に戻り、Copilot Chat パネルを開き、**New Chat** を選択して新しい会話を始めます。

1. Chat ビューのドロップダウンで **Agent** を選びます。
2. エージェントのドロップダウンから **Accessibility agent** を選択します。
3. 次のプロンプトを送信します。

    ```plaintext
    Add a high-contrast mode to the site. There should be a toggle for high contrast which the user can set, and the setting should persist across page reloads using local storage on the browser.
    ```

4. Copilot がコードベースを確認し、変更を提案して適用する様子を確認します。変更はファイル パスと差分とともにチャットに表示されます。
5. **Files changed** の一覧で、エージェントが変更したファイルを確認します。

> [!NOTE]
> 作業には数分かかることがあります。エージェントは Astro コンポーネント、CSS、関連テストなどを更新します。次の演習では、作業中の内容を確認して案内します。

## まとめと次のステップ

カスタム エージェントでアクセシビリティの専門知識と標準を再利用し、Copilot Chat の agent mode からエージェントを使いました。次は作業を[監視して案内し][next-lesson]、ライト モードの切り替えも同じセッションに追加します。

## リソース

- [カスタム エージェントについて][custom-agents]
- [IDE でカスタム エージェントを作成する][creating-custom-agents-ide]
- [VS Code のカスタム エージェント][custom-agents-vscode]
- [カスタム エージェントの構成][custom-agents-config]
- [awesome-copilot のカスタム エージェント][awesome-copilot-agents]

---

| [← 前のレッスン: Playwright MCP で機能をテストする][previous-lesson] | [次のレッスン: エージェントの監視と管理 →][next-lesson] |
|:--|--:|

[previous-lesson]: ../3-mcp/
[next-lesson]: ../5-managing-agents/
[custom-agents]: https://docs.github.com/copilot/concepts/agents/cloud-agent/about-custom-agents
[creating-custom-agents-ide]: https://docs.github.com/copilot/how-tos/use-copilot-agents/cloud-agent/create-custom-agents-in-your-ide
[custom-agents-vscode]: https://code.visualstudio.com/docs/copilot/customization/custom-agents
[custom-agents-config]: https://docs.github.com/copilot/reference/custom-agents-configuration
[awesome-copilot-agents]: https://github.com/github/awesome-copilot/tree/main/agents
