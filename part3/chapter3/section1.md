# 3.3.1 Mac OS X 10.14


## 3.3.1.1 Gitの環境設定

Gitに関するグローバル環境設定

```bash
$ git --version

$ git config --list
$ git config --system --list
$ git config --global --list
$ git config --local --list

$ git config --global core.autocrlf false
$ git config --global core.ignorecase
$ git config --global color.ui true

$ git config --global core.editor 'code --wait'
$ git config --global merge.tool 'code --wait "$MERGED"'
$ git config --global push.default simple

$ git config --list
```

補足 : Gitの設定は以下の順番で設定の読み込みをする。  
　　そのため、最後に読み込まれるリポジトリごとの設定が一番優先される。  
  - 1 /etc/gitconfig (git config --system) : システム全体の設定  
  - 2 ~/.gitconfigか~/.config/git/config (git config --global) : 各ユーザの設定  
  - 3 .git/config (git config --local) : リポジトリごとの設定  
<br>
<br>
<br>

## 3.3.1.2 giboのインストールと設定

### giboのインストール

各種環境のGit管理除外設定が煩雑なため、
自動で該当環境設定をしてくれるツールgiboを導入する。

```bash
$ brew install gibo
```
<br>

### giboを使ってGit管理除外ファイルを設定

ここでは、例として、MacOS向けの設定のみを行う。

```bash
$ gibo update
$ ls -la ~/.gitignore-boilerplates
$ gibo list

$ cd
$ gibo dump macOS >> .gitignore_global

$ git config --global -l
$ git config --global core.excludesfile '~/.gitignore_global'
$ git config --global -l
```
<br>
