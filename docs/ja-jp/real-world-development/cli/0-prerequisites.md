---
title: "レッスン 0 - 前提条件"
description: "Tailspin Toys のコピーを作成し、Copilot CLI ワークショップ用の GitHub Codespace を準備します。"
authors:
  - geektrainer
lastUpdated: 2026-09-18
---

Copilot CLI のレッスンを始める前に、必要な準備を整えます。Tailspin Toys リポジトリの自分用コピーを作成し、[Codespace][codespaces] を起動します。次のレッスンでは、統合ターミナルを使って Copilot CLI をインストールし、実行します。

このレッスンでは、Tailspin Toys プロジェクトのコピーをテンプレートから作成し、Codespace を作成してプロジェクトの準備ができていることを確認します。

## ラボ用リポジトリを設定する

Tailspin Toys プロジェクトのコピーを使います。[テンプレート リポジトリ][tailspin-template]から作成してください。新しいリポジトリにはラボに必要なファイルがすべて含まれています。

1. 新しいブラウザー ウィンドウで [Tailspin Toys テンプレート][tailspin-template]を開きます。
2. **Use this template**、**Create a new repository** の順に選択して自分用のコピーを作成します。
3. GitHub または Microsoft が主催するイベントでワークショップを受講している場合は、メンターの案内に従ってください。それ以外の場合は、GitHub Copilot を利用できる組織にリポジトリを作成します。
4. 作成したリポジトリのパス (`organization-or-user-name/repository-name`) をメモします。以降の演習で使用します。

> [!NOTE]
> テンプレートからリポジトリを作成すると、GitHub issue のバックログが自動的に作成されます。ワークショップではこの issue を使うため、自分で登録する必要はありません。

ワークショップ テンプレートの新しいコピーを使ってください。リポジトリには、指示、アプリケーション コード、テスト、`quality-checks` スキル、バックログが含まれています。古いコピーを使う場合は、必要なファイルが含まれていることをファシリテーターに確認してください。

## Codespace を作成する

次に、ワークショップで使う Codespace を作成します。[GitHub Codespaces][codespaces] は、ブラウザーでコードを記述、実行、デバッグできるクラウドベースの開発環境です。

1. 作成したリポジトリを開きます。
2. **Code** を選択します。
3. **Codespaces** タブを選び、**Create codespace on main** を選択します。
4. Codespace のセットアップが完了するまで待ちます。テンプレートがプロジェクトの依存関係、Playwright Chromium、ローカル データベースをインストールします。
5. **Do you trust the authors of the files in this folder?** と表示された場合は、**Trust Folder & Continue** を選びます。
6. リポジトリのルートでターミナルを開き、アプリを起動します。

   ```bash
   npm run dev
   ```

7. Codespaces がポート `4321` を使用可能と通知したら、**Open in Browser** を選択し、Tailspin Toys サイトが表示されることを確認します。
8. ターミナルに戻り、<kbd>Ctrl</kbd>+<kbd>C</kbd> で開発サーバーを停止します。

## まとめと次のステップ

準備ができました。テンプレートからプロジェクトのコピーを作成し、Codespace を起動して、プロジェクトが準備できたことを確認しました。次は Codespace に[GitHub Copilot CLI をインストール][next-lesson]し、GitHub アカウントで認証します。

## リソース

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces の使用を開始する][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[next-lesson]: ../1-install-copilot-cli/
[codespaces]: https://github.com/features/codespaces
