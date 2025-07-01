# claude-code-devcontainer

Claude Code 向け Development Containers 設定ファイル

## Overview

[anthropics/claude-code](https://github.com/anthropics/claude-code/tree/main/.devcontainer) をベースに以下のカスタマイズを加えています。

- [mise](https://mise.jdx.dev/) をインストール
  - 参考: https://mise.jdx.dev/mise-cookbook/docker.html#docker-image-with-mise
- `/tmp` ディレクトリへの書き込みを許可
  - Claude が一括置換スクリプトなどを作成することがあったため
- 外向きの接続を全て許可
  - セキュリティ強度は下がるが、一部環境下で GitHub の IP 取得にあたって API レートリミットに引っかかるケースがあり、認証しないと取得エラーになるため

## How to use

筆者は以下のエイリアスを設定しています。
`mise install` でも同様に GitHub API 認証が必要となるケースがあり、コンテナビルド時ではなく起動後に行なっています。

```console
alias dcclaudeinit="devcontainer up --workspace-folder . --config ~/.config/devcontainer/claude/devcontainer.json && devcontainer exec --workspace-folder . --config ~/.config/devcontainer/claude/devcontainer.json --remote-env GITHUB_TOKEN=`gh auth token` mise install"
alias dcclaude="devcontainer exec --workspace-folder . --config ~/.config/devcontainer/claude/devcontainer.json claude --dangerously-skip-permissions"
```
