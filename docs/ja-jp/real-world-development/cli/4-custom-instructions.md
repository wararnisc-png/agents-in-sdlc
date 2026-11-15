---
title: "レッスン 4 - カスタム指示で Copilot を導く"
description: "リポジトリの指示を確認し、ドキュメント標準を追加して、フィルターのコードに適用します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

生成 AI を使うときは、コンテキストが重要です。作業方法に決まりがある場合は、Copilot が参照できるようにします。[指示ファイル][instruction-files]では、必要なコードだけでなく、その構成方法も説明できます。フィルター機能を実装したので、Copilot が使った指示を確認し、ドキュメント標準を追加してコードに適用します。

このレッスンでは、リポジトリの指示とパス指定の指示ファイルがエージェントに伝わる方法を確認し、コーディング標準を守るために指示を更新して、その影響を確認します。

## シナリオ

Tailspin Toys には次の開発標準があります。

- コメントはコードを言い換えるのではなく、意図や自明でない判断を説明します。
- `db/` と `src/lib/` のエクスポート関数は、目的、パラメーター、戻り値を TSDoc/JSDoc で説明します。`db` 引数を注入する場合は、その引数についても記載します。
- 再利用可能な Astro コンポーネントは `Props` の契約を説明し、関連コードの変更時にコメントを更新します。
- 既存のフォーマットと lint の指示を維持します。

## 指示ファイル

カスタム指示では、コーディング スタイルや要件などのコンテキストを Copilot に伝えます。

- `.github/copilot-instructions.md` は、リポジトリへのすべてのリクエストに送信する共通の指示です。
- `.github/instructions/*.instructions.md` は、特定の言語、ファイル種別、タスクに関するガイドラインです。

> [!NOTE]
> ほかの指示ファイル形式や環境ごとのサポート状況は異なります。形式に依存する前に、[カスタム指示のサポート リファレンス][custom-instructions-support]を確認してください。

## このプロジェクトのカスタム指示を確認する

1. Codespace に戻り、ターミナルではなく Codespaces エディターで `.github/copilot-instructions.md` を開きます。
2. プロジェクトの概要と、リポジトリ全体に適用されるコーディング ガイダンスを確認します。
3. `.github/instructions` フォルダーを開き、Astro、Drizzle データ層、テストなどの指示を確認します。
4. `.github/instructions/unit-tests.instructions.md` の `applyTo` フィールドを確認します。
5. `.github/instructions/drizzle.instructions.md` にある、関連指示ファイルやプロジェクト内の例へのリンクを確認します。

## チームの方針に合わせて指示を更新する

1. `.github/copilot-instructions.md` の **Code formatting guidance** セクションを開きます。
2. セクションの最後に、次の項目を追加します。

   ```markdown
   - All new TypeScript should contain TSDocs comments for documentation purposes.
   ```

変更は自動的に保存されます。

## 更新したガイダンスを適用する

Copilot CLI は会話の開始時にリポジトリの指示を読み込みます。フィルターの会話を終了して再開すると、機能に関するコンテキストを保ったまま、新しい指示を読み込めます。

1. フィルターの会話が開いている場合は `/exit` で終了します。会話は自動的に保存されます。
2. リポジトリのルートで `game-filters-cli` ブランチから会話を再開します。

   ```bash
   copilot --resume
   ```

   会話を選ぶよう求められた場合はフィルターの会話を選択し、`game-filters-cli` ブランチをチェックアウトしていることを確認します。
3. 次のプロンプトを送信します。

   ```plaintext
   We just updated our instructions and code guidance. Can you please update the code you generated to match that guidance?
   ```

4. `/diff` を入力し、変更された TypeScript ファイルを確認します。TSDoc が追加され、コードを正確に説明していることを確かめます。

## まとめと次のステップ

Copilot CLI が指示ファイルからコンテキストを得る方法を確認し、機能に新しい標準を適用しました。次は[再利用可能な quality-checks スキルを調整して実行][next-lesson]し、lint とテストを一貫して実行します。

## リソース

- [Copilot CLI のカスタム指示を追加する][instruction-files]
- [カスタム指示のサポート][custom-instructions-support]
- [カスタム指示を作成するためのベスト プラクティス][instructions-best-practices]
- [指示ファイルの例を集めた Awesome Copilot][awesome-copilot]

[instruction-files]: https://docs.github.com/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions
[instructions-best-practices]: https://docs.github.com/copilot/concepts/prompting/response-customization#writing-effective-custom-instructions
[awesome-copilot]: https://awesome-copilot.github.com/
[custom-instructions-support]: https://docs.github.com/copilot/reference/custom-instructions-support
[previous-lesson]: ../3-agent-modes/
[next-lesson]: ../5-agent-skills/
