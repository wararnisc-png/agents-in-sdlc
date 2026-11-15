---
title: "演習 0: 前提条件"
authors:
  - geektrainer
lastUpdated: 2026-06-30
---

VS Code の演習を始める前に、Tailspin Toys リポジトリのコピーを作成し、作業用の [Codespace][codespaces] を起動して、エディターで GitHub Copilot Chat が動作することを確認します。

## ラボ用リポジトリを設定する

1. 新しいブラウザー ウィンドウで [Tailspin Toys テンプレート][tailspin-template]を開きます。
2. ラボのリポジトリ ページで **Use this template** を選択し、**Create a new repository** を選んで自分用のコピーを作成します。

    ![Use this template ボタン](../../../_images/ex0-use-template.png)

3. GitHub または Microsoft が主催するイベントでワークショップを受講している場合は、メンターの案内に従ってください。それ以外の場合は、GitHub Copilot を利用できる組織にリポジトリを作成します。

    ![リポジトリ テンプレートの設定を入力する画面](../../../_images/ex0-repository-settings.png)

4. 作成したリポジトリのパス (**organization-or-user-name/repository-name**) をメモします。

> [!NOTE]
> **バックログの準備**
>
> テンプレートからリポジトリを作成すると、GitHub issue のバックログが自動的に作成されます。ワークショップではこの issue を使うため、自分で登録する必要はありません。

## Codespace を作成する

[GitHub Codespaces][codespaces] は、ブラウザーでコードを記述、実行、デバッグできるクラウドベースの開発環境です。

1. 作成したリポジトリを開きます。
2. 緑色の **Code** ボタンを選択します。

    ![Code ボタンを選択する画面](../../../_images/ex0-code-button.png)

3. **Codespaces** タブを選び、**+** ボタンを選択して Codespace を作成します。

    ![新しい Codespace を作成する画面](../../../_images/ex0-create-codespace.png)

Codespace の作成には数分かかります。演習に必要な環境を手動でインストールするよりも早く完了します。

> [!CAUTION]
> 今後の演習でこの Codespace に戻ります。ブラウザーのタブを開いたままにしてください。

> [!NOTE]
> このワークショップは Codespace またはローカルの [dev container][dev-containers] で動作します。ローカルで実行する場合は、クローンしたリポジトリを VS Code で開き、表示されたら **Reopen in Container** を選択してください。

[codespaces]: https://github.com/features/codespaces
[dev-containers]: https://code.visualstudio.com/docs/devcontainers/containers

## GitHub Copilot Chat と agent mode を使う

VS Code で GitHub Copilot Chat の agent mode を使うには、IDE に GitHub Copilot Chat 拡張機能が必要です。GitHub Codespaces を使用している場合は、通常インストール済みです。

> [!TIP]
> 拡張機能がインストールされていない場合は、[Visual Studio Code Marketplace からインストール][copilot-chat-extension]するか、VS Code の Extensions ビューで **GitHub Copilot Chat** を検索し、**Install** を選択します。

1. Codespace に戻ります。
2. エディター右側に Copilot Chat がない場合は、Codespace 上部の **Copilot Chat** アイコンを選択します。
3. Copilot Chat の入力欄に `Hello world` などと入力し、Enter キーを押します。
4. 認証を求められた場合は、GitHub アカウントでサインインします。

    ![Copilot Chat の認証プロンプトの例](../../../_images/ex1-copilot-authentication.png)

## まとめ

ラボ用リポジトリのコピーを作成し、コードを書くための Codespace を準備しました。

## 次のステップ

次は Copilot にプロジェクトの規約を伝えます。[演習 1 - カスタム指示][next-lesson]に進んでください。

## リソース

- [GitHub Codespaces の概要][codespaces]
- [テンプレートからリポジトリを作成する][template-repository]
- [Codespaces の使用を開始する][codespaces-quickstart]

[tailspin-template]: https://github.com/github-samples/tailspin-toys
[template-repository]: https://docs.github.com/repositories/creating-and-managing-repositories/creating-a-template-repository
[codespaces-quickstart]: https://docs.github.com/codespaces/getting-started/quickstart
[copilot-chat-extension]: https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat
[next-lesson]: ../1-custom-instructions/
