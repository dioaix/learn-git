# 3.5.1 ローカルリポジトリを作成（空のリモートリポジトリ）


## 3.5.1.1 Local Repositoryの作成

Local Repository用ディレクトリの作成

```bash
$ mkdir /Users/dioaix/Documents/git
$ ls -la /Users/dioaix/Documents/


$ mkdir /Users/dioaix/Documents/git/learn-git
$ ls -la /Users/dioaix/Documents/git/
```
<br>

Gitの初期化

```bash
$ cd /Users/dioaix/Documents/git/learn-git

$ git status
fatal: not a git repository (or any of the parent directories): .git

$ git init
Initialized empty Git repository in /Users/dioaix/Documents/git/learn-git/.git/
```
<br>

Gitのリポジトリの環境設定
```bash
$ git config --local user.name ‘dioaix’
$ git config --local user.email ‘dioaix@email.com’
```
補足 : 複数のGitHubアカウントを利用している場合、上記のように、それぞれのリポジトリでユーザ名とemailの設定を行う必要がある。
<br>
<br>
<br>

## 3.5.1.2 リモートリポジトリに関する設定

```bash
$ git remote add origin git@dioaix.github:dioaix/learn-git.git

$ git fetch
Enter passphrase for key '/Users/dioaix/.ssh/id_rsa_dioaix@github': 
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From dioaix.github:dioaix/learn-git
 * [new branch]      master     -> origin/master


$ git pull origin master
Enter passphrase for key '/Users/dioaix/.ssh/id_rsa_dioaix@github': 
From dioaix.github:dioaix/learn-git
 * branch            master     -> FETCH_HEAD


$ git branch -a
* master
  remotes/origin/master

$ git branch -vv
* master 2fc8765 Initial commit
```
<br>
<br>
<br>
