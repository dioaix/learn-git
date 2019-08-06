# 3.8.2 Gitbookの利用

## 3.8.2.1 環境の前提

PythonのVenv環境は構築・設定済みの環境を前提とする。
PythonのVenv環境を使って、NodeJSのインストールとgitbookのインストールをする。
<br><br><br>


## 3.8.2.2 Venv + Nodeenv + gitbook-cli仮想環境の準備


### 3.8.2.2.1 Venv仮想環境の準備

Venv環境の作成
```bash
$ cd ~/venv0

$ python3 -m venv ~/venv/venv37.nodeenv
```

補足 : 以下のコマンドでパッケージのクリアができる。  
python3 -m venv --clear ~/venv/venv37.nodeenv  
削除は以下の該当ディレクトリを削除する  
rm -r ~/venv/venv37.nodeenv  
<br><br><br>


Venv環境のActivate
```bash
$ source ~/venv/venv37.nodeenv/bin/activate

(venv37.nodeenv)$ python --version
Python 3.7.4

(venv37.nodeenv)$ pip install --upgrade pip
```
補足 : 以下のコマンドでパッケージのインストールができる。  
(venv37.nodeenv)$ pip install <パッケージ名>
<br><br><br>



### 3.8.2.2.2 Venv仮想環境で、Nodeenvをインストール

venv仮想環境の中で、各バージョンのNodeJSを使えるようにするため、Nodeenvをインストールする。

```bash
(venv37.nodeenv)$ pip search nodeenv
nodeenv (1.3.3)  - Node.js virtual environment builder

(venv37.nodeenv)$ pip install nodeenv


(venv37.nodeenv)$ nodeenv --version
1.3.3
```

補足 : pip を使ったパッケージ管理
https://docs.python.jp/3/tutorial/venv.html


補足 : Nodeenvを使ったNodeJSの環境構築
https://github.com/ekalinin/nodeenv

<br><br><br>



### 3.8.2.2.3 Nodeenvを使って、NodeJS仮想環境を作成する

最新バージョンのNodeJS仮想環境を作成
```bash
(venv37.nodeenv)$  cd ~/venv/venv37.nodeenv/

(venv37.nodeenv)$ nodeenv node127.gitbook
 * Install prebuilt node (12.7.0) ..... done.

(venv37.nodeenv)$ ls -la
total 8
drwxr-xr-x   7 dioaix  staff  224 Jul 30 13:27 .
drwxr-xr-x   4 dioaix  staff  128 Jul 30 13:20 ..
drwxr-xr-x  13 dioaix  staff  416 Jul 30 13:22 bin
drwxr-xr-x   2 dioaix  staff   64 Jul 30 13:20 include
drwxr-xr-x   3 dioaix  staff   96 Jul 30 13:20 lib
drwxr-xr-x   7 dioaix  staff  224 Jul 30 13:27 node127.gitbook
-rw-r--r--   1 dioaix  staff   75 Jul 30 13:20 pyvenv.cfg

(venv37.nodeenv)$ source ~/venv/venv37.nodeenv/node127.gitbook/bin/activate

(node127.gitbook) (venv37.nodeenv) $ node -v
v12.7.0

(node127.gitbook) (venv37.nodeenv) $ npm -v
6.10.0
```


Nodeenvで扱えるNodeJSのバージョンを確認する
```bash
(node127.gitbook) (venv37.nodeenv)$  nodeenv --list
0.0.1	0.0.2	0.0.3	0.0.4	0.0.5	0.0.6	0.1.0	0.1.1
0.1.2	0.1.3	0.1.4	0.1.5	0.1.6	0.1.7	0.1.8	0.1.9
・・・省略・・・
11.10.1	11.11.0	11.12.0	11.13.0	11.14.0	11.15.0	12.0.0	12.1.0
12.2.0	12.3.0	12.3.1	12.4.0	12.5.0	12.6.0	12.7.0
```
<br><br><br>



### 3.8.2.2.4 Venv+nodeenv環境でgitbook-cliをインストール

```bash
(node127.gitbook) (venv37.nodeenv) $ npm install -g gitbook-cli

(node127.gitbook) (venv37.nodeenv) $ which gitbook
/Users/dioaix/venv/venv37.nodeenv/node127.gitbook/bin/gitbook

# 正常にインストールできたかを確認
(node127.gitbook) (venv37.nodeenv) $ gitbook -V
```
<br><br><br>



### 3.8.2.2.5 Venv+nodeenv環境のDeactivate
ここでDeactivateをする必要がないが、手順確認のために、Deactivateを行う。

```bash
(node127.gitbook) (venv37.nodeenv) $ cd /Users/dioaix/venv/venv37.nodeenv

(node127.gitbook) (venv37.nodeenv) $ deactivate_node

(venv37.nodeenv) $ deactivate

$ python --version
Python 2.7.10
```
<br><br><br>











## 3.8.2.3 .gitignoreファイルの作成


### 3.8.2.3.1 Topic blanchの作成

「config-set-.gitignore/dioaix」という名のTopic blanchを作成する。
「/ユーザ名」でBlanchの名前をつけると、
誰が作成したBlanchなのかが一目瞭然で運用しやすくなる。

```bash
# 事前確認
$ git branch
* master

$ git branch -a
* master
  remotes/origin/master

# Topic blanchの作成
$ git branch config-set-.gitignore/dioaix
```
<br>


補足 : topicブランチの名前は、なんのためのブランチなのか説明する内容にする。  
例 : [Create | fix | improve]-何のために-何をする/ユーザ名  


<br>


```bash
# 正しく作成できたことを確認
$ git branch
  config-set-.gitignore/dioaix
* master

$ git branch -a
  config-set-.gitignore/dioaix
* master
  remotes/origin/master

# Topic blanchにcheckout
$ git checkout config-set-.gitignore/dioaix

$ git branch
* config-set-.gitignore/dioaix
  master

$ git branch -a
* config-set-.gitignore/dioaix
  master
  remotes/origin/master
```
<br><br><br>


### 3.8.2.3.2 ファイルの作成・編集

ワークツリーで、リポジトリのGit管理除外設定ファイルを作成する。
giboを使って、VScodeとGitbookに対応するように設定。

```bash
$ gibo dump VisualStudioCode Gitbook >> .gitignore

$ ls -la

$ cat .gitignore
```
<br>

### 3.8.2.3.3 Local repositoryでcommitする

作成したファイルをステージングエリアに追加する。
```bash
$ git add .gitignore

$ git status
On branch config-set-.gitgnore/dioaix
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   .gitignore
```
<br>


Commitをして、gitディレクトリに格納する。

```bash
$ git commit
```
<br>


Gitのグローバルの環境設定により、VScodeが立ち上がり、以下のコミットメッセージを記入する。
```text
Add .gitignore for Mac VScode and Gitbook

[Why] Set the .gitignore file to exclude unnecessary files in repository to use VScode, Gitbook.
[How] Create the .gitignore file using the tool gibo.
[Side-effects] Unintended files may be excluded.
```
<br><br><br>




### 3.8.2.3.4 Commit結果の確認


```bash
$ git status

$ git log --oneline config-set-.gitignore/dioaix
432eb86 (HEAD -> config-set-.gitignore/dioaix) Add .gitignore for Mac VScode and Gitbook
2fc8765 (origin/master, master) Initial commit

$ git log --oneline
432eb86 (HEAD -> config-set-.gitignore/dioaix) Add .gitignore for Mac VScode and Gitbook
2fc8765 (origin/master, master) Initial commit

$ git log --graph --pretty=format:"%h %s" config-set-.gitignore/dioaix
* 432eb86 Add .gitignore for Mac VScode and Gitbook
* 2fc8765 Initial commit

$ git log
commit 432eb86c14473fa3f90800f26c778b43f027f531 (HEAD -> config-set-.gitignore/dioaix)
Author: ‘dioaix’ <‘dioaix@email.com’>
Date:   Wed Jul 31 16:48:39 2019 +0900

    Add .gitignore for Mac VScode and Gitbook
    
    [Why] Set the .gitignore file to exclude unnecessary files in repository to use Mac, VScode, Gitbook.
    [How] Create the .gitignore file using the tool gibo.
    [Side effects] Unintended files may be excluded.

commit 2fc876567e47bc026b6655e8927525a8bab1cfdf (origin/master, master)
Author: dioaix <dioaix@email.com>
Date:   Mon Jul 29 16:39:53 2019 +0900

    Initial commit
```
<br><br><br>





### 3.8.2.3.5 Remote repositoryにPush



```bash
$ git branch -a
* config-set-.gitignore/dioaix
  master
  remotes/origin/master

$ git diff config-set-.gitignore/dioaix master

$ git push -u origin config-set-.gitignore/dioaix
Enter passphrase for key '/Users/dioaix/.ssh/id_rsa_dioaix@github': 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 1.01 KiB | 1.01 MiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
remote: 
remote: Create a pull request for 'config-set-.gitignore/dioaix' on GitHub by visiting:
remote:      https://github.com/dioaix/learn-git/pull/new/config-set-.gitignore/dioaix
remote: 
To dioaix.github:dioaix/learn-git.git
 * [new branch]      config-set-.gitignore/dioaix -> config-set-.gitignore/dioaix
Branch 'config-set-.gitignore/dioaix' set up to track remote branch 'config-set-.gitignore/dioaix' from 'origin'.

$ git branch -a
* config-set-.gitignore/dioaix
  master
  remotes/origin/config-set-.gitignore/dioaix
  remotes/origin/master

$ git branch -vv
* config-set-.gitignore/dioaix 432eb86 [origin/config-set-.gitignore/dioaix] Add .gitignore for Mac VScode and Gitbook
  master                       2fc8765 Initial commit
```
<br><br><br>



### 3.8.2.3.6 GitHubでのPull Requestし、レビューを依頼

GitHubのウェブページで、Pull Requestを作成し、レビューを依頼。
<br><br><br>



### 3.8.2.3.7 本番稼働環境へのデプロイ

通常では、レビューが終わると、本番稼働環境へデプロイを行う。  
その後、本番稼働環境で問題なく動作することをモニタリングする。  
本手順では、デプロイがないので、省略する。
<br><br><br>


### 3.8.2.3.8 Remote ripositoryでmasterにマージ

モニタリングして、問題がなければ、
GitHubのウェブページで、masterにマージする。
<br><br><br>


### 3.8.2.3.9 Remote ripositoryでTopic branchを削除

GitHubのウェブページで、config-set-.gitignore/dioaixを削除。
<br><br><br>


### 3.8.2.3.10 Local ripositoryでTopic branchを削除


```bash
$ git branch
  config-set-.gitignore/dioaix
* master

$ git branch -a
  config-set-.gitignore/dioaix
* master
  remotes/origin/config-set-.gitignore/dioaix
  remotes/origin/master

$ git branch -vv
  config-set-.gitignore/dioaix 432eb86 [origin/config-set-.gitignore/dioaix] Add .gitignore for Mac VScode and Gitbook
* master                       2fc8765 Initial commit

$ git branch -d config-set-.gitignore/dioaix
warning: deleting branch 'config-set-.gitignore/dioaix' that has been merged to
         'refs/remotes/origin/config-set-.gitignore/dioaix', but not yet merged to HEAD.
Deleted branch config-set-.gitignore/dioaix (was 432eb86).

$ git branch
* master

$ git branch -a
* master
  remotes/origin/config-set-.gitignore/dioaix
  remotes/origin/master

git branch -vv
* master 2fc8765 Initial commit
```
<br><br><br>


### 3.8.2.3.11 Remote ripository最新情報の反映

```bash
$ git branch --remote
  origin/config-set-.gitignore/dioaix
  origin/master

$ git fetch -p
Enter passphrase for key '/Users/dioaix/.ssh/id_rsa_dioaix@github': 
From dioaix.github:dioaix/learn-git
 - [deleted]         (none)     -> origin/config-set-.gitignore/dioaix
remote: Enumerating objects: 5, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (4/4), done.
remote: Total 4 (delta 0), reused 3 (delta 0), pack-reused 0
Unpacking objects: 100% (4/4), done.
   2fc8765..f82e112  master     -> origin/master

$ git branch -a
* master
  remotes/origin/master
```
<br><br><br>



### 3.8.2.3.12 Remote ripositoryのmasterの変更分をLocal ripositoryのmasterにマージ

```bash
$ git checkout master
Already on 'master'

$ git fetch origin master
Enter passphrase for key '/Users/dioaix/.ssh/id_rsa_dioaix@github': 
From dioaix.github:dioaix/learn-git
 * branch            master     -> FETCH_HEAD

# [ローカル] → [リモート追跡]の差分を見る
$ git diff master origin/master

$ git merge --no-ff origin/master
```
<br><br><br>
<br><br><br>








## 3.8.2.4 gitbookの初期化


### 3.8.2.4.1 Topic blanchの作成

「config-init-gitbook/dioaix」という名のTopic blanchを作成する。
「/ユーザ名」でBlanchの名前をつけると、
誰が作成したBlanchなのかが一目瞭然で運用しやすくなる。

```bash
# 事前確認
$ git branch
* master

$ git branch -a
* master
  remotes/origin/master

# Topic blanchの作成
$ git branch config-init-gitbook/dioaix

# 正しく作成できたことを確認
$ git branch
  config-init-gitbook/dioaix
* master

$ git branch -a
  config-init-gitbook/dioaix
* master
  remotes/origin/master

# Topic blanchにcheckout
$ git checkout config-init-gitbook/dioaix

$ git branch
* config-init-gitbook/dioaix
  master

$ git branch -a
* config-init-gitbook/dioaix
  master
  remotes/origin/master
```
<br><br><br>


### 3.8.2.4.2 ファイルの作成・編集

ワークツリーで、SUMMARY.mdファイルを作成し、目次を作る。

```text
# Summary

* [Introduction](README.md)
* [1 中文](part1/README.md)
* [2 English](part2/README.md)
* [3 日本語](part3/README.md)
    * [3.1 はじめに](part3/chapter1/README.md)
        * [3.1.1 本書の目的](part3/chapter1/section1.md)
        * [3.1.2 対象読者](part3/chapter1/section2.md)
        * [3.1.3 免責](part3/chapter1/section3.md)
        * [3.1.4 Gitの概要](part3/chapter1/section4.md)
    * [3.2 前提環境](part3/chapter2/README.md)
        * [3.2.1 開発環境](part3/chapter2/section1.md)
        * [3.2.2 本書で使う仮情報](part3/chapter2/section2.md)
    * [3.3 PC環境の設定](part3/chapter3/README.md)
        * [3.3.1 Mac OS X 10.14](part3/chapter3/section1.md)
        * [3.3.2 CentOS 7](part3/chapter3/section2.md)
        * [3.3.3 Window 10](part3/chapter3/section3.md)
    * [3.4 Githubの設定](part3/chapter4/README.md)
        * [3.4.1 Githubのアカウント作成](part3/chapter4/section1.md)
        * [3.4.2 Githubの設定](part3/chapter4/section2.md)
        * [3.4.3 GithubでRemote Repositoryの作成](part3/chapter4/section3.md)
    * [3.5 Local Repositoryの作成](part3/chapter5/README.md)
        * [3.5.1 最初からリポジトリを作成](part3/chapter5/section1.md)
        * [3.5.2 既存Remote RepositoryからClone](part3/chapter5/section2.md)
    * [3.6 Github-flow](part3/chapter6/README.md)
        * [3.6.1 Github-flowの概要](part3/chapter6/section1.md)
        * [3.6.2 プロジェクトFlow規約](part3/chapter6/section2.md)
        * [3.6.3 blanchの作成からデプロイの一連作業](part3/chapter6/section3.md)
    * [3.7 Gitlab-flow](part3/chapter7/README.md)
        * [3.7.1 Gitlab-flowの概要](part3/chapter7/section1.md)
        * [3.7.2 プロジェクトFlow規約](part3/chapter7/section2.md)
        * [3.7.3 blanchの作成からデプロイの一連作業](part3/chapter7/section3.md)
    * [3.8 便利なツールの利用](part3/chapter8/README.md)
        * [3.8.1 giboの利用](part3/chapter8/section1.md)
        * [3.8.2 Gitbookの利用](part3/chapter8/section2.md)
    * [3.9 よくある設定](part3/chapter9/README.md)
        * [3.9.1 Gitbook環境の構築](part3/chapter9/section1.md)
        * [3.9.1 複数Githubアカウントを同じPCでの利用](part3/chapter9/section2.md)
        * [3.9.2 upstreamの設定方法](part3/chapter9/section3.md)
    * [3.10 よくあるエラー対応](part3/chapter10/README.md)
        * [3.10.1 新規Local Repositoryから,Remote Repositoryにpush時のrejectエラー対処](part3/chapter10/section1.md)

```
<br><br><br>

ファイルが作成されていることを確認。
```bash
$ ls -la
total 24
drwxr-xr-x  10 dioaix  staff   320 Jul 31 21:00 .
drwxr-xr-x  10 dioaix  staff   320 Jul 29 18:07 ..
drwxr-xr-x  15 dioaix  staff   480 Jul 31 20:59 .git
-rw-r--r--   1 dioaix  staff  1196 Jul 31 20:42 .gitignore
drwxr-xr-x   3 dioaix  staff    96 Jul 30 13:51 .vscode
-rw-r--r--   1 dioaix  staff    11 Jul 31 16:59 README.md
-rw-r--r--   1 dioaix  staff  2583 Jul 31 21:00 SUMMARY.md
drwxr-xr-x   3 dioaix  staff    96 Jul 31 21:00 part1
drwxr-xr-x   3 dioaix  staff    96 Jul 31 21:00 part2
drwxr-xr-x  13 dioaix  staff   416 Jul 31 21:00 part3
```
<br><br><br>




### 3.8.2.4.3 gitbookの仮想環境(Venv+nodeenv環境)のActivate

```bash
$ cd ~/venv

$ ls
venv37			venv37.nodeenv

$ source ~/venv/venv37.nodeenv/bin/activate

(venv37.nodeenv)$ source ~/venv/venv37.nodeenv/node127.gitbook/bin/activate

(node127.gitbook) (venv37.nodeenv) $
```
<br><br><br>




### 3.8.2.4.4 Local repositoryでcommitする

作成したファイルをステージングエリアに追加する。
```bash
$ git add .

$ git status
```
<br><br><br>


Commitをして、gitディレクトリに格納する。

```bash
$ git commit
```
<br><br><br>


Gitのグローバルの環境設定により、VScodeが立ち上がり、以下のコミットメッセージを記入する。
```text
Add SUMMARY.md and gitbook init files

[Why] Init gitbook.
[How] Creat SUMMARY.md and run gitbook init command.
[Side-effects] None.
```
<br><br><br>


### 3.8.2.4.5 Commit結果の確認


```bash
$ git status

$ git log --oneline config-init-gitbook/dioaix
f0efeca (HEAD -> config-init-gitbook/dioaix) Add SUMMARY.md and gitbook init files
f82e112 (origin/master, master) Merge pull request #1 from dioaix/config-set-.gitignore/dioaix
432eb86 Add .gitignore for Mac VScode and Gitbook
2fc8765 Initial commit

$ git log --oneline
f0efeca (HEAD -> config-init-gitbook/dioaix) Add SUMMARY.md and gitbook init files
f82e112 (origin/master, master) Merge pull request #1 from dioaix/config-set-.gitignore/dioaix
432eb86 Add .gitignore for Mac VScode and Gitbook
2fc8765 Initial commit

$ git log --graph --pretty=format:"%h %s" config-init-gitbook/dioaix
* f0efeca Add SUMMARY.md and gitbook init files
*   f82e112 Merge pull request #1 from dioaix/config-set-.gitignore/dioaix
|\  
| * 432eb86 Add .gitignore for Mac VScode and Gitbook
|/  
* 2fc8765 Initial commit

$ git log
commit f0efeca729ff2cbc5db2b0d54c0f0075409ec20d (HEAD -> config-init-gitbook/dioaix)
Author: ‘dioaix’ <‘dioaix@email.com’>
Date:   Wed Jul 31 21:07:06 2019 +0900

    Add SUMMARY.md and gitbook init files
    
    [Why] Init gitbook.
    [How] Creat SUMMARY.md and run gitbook init command.
    [Side effects] None.

commit f82e11277299888cd9733caa5b2e1e62c06e7724 (origin/master, master)
Merge: 2fc8765 432eb86
Author: dioaix <dioaix@email.com>
Date:   Wed Jul 31 19:30:53 2019 +0900

    Merge pull request #1 from dioaix/config-set-.gitignore/dioaix
    
    Add .gitignore for Mac VScode and Gitbook

commit 432eb86c14473fa3f90800f26c778b43f027f531
Author: ‘dioaix’ <‘dioaix@email.com’>
Date:   Wed Jul 31 16:48:39 2019 +0900

    Add .gitignore for Mac VScode and Gitbook
    
    [Why] Set the .gitignore file to exclude unnecessary files in repository to use Mac, VScode, Gitbook.
    [How] Create the .gitignore file using the tool gibo.
    [Side effects] Unintended files may be excluded.

commit 2fc876567e47bc026b6655e8927525a8bab1cfdf
Author: dioaix <dioaix@email.com>
Date:   Mon Jul 29 16:39:53 2019 +0900

    Initial commit
```
<br><br><br>





### 3.8.2.4.6 Remote repositoryにPush



```bash
$ git branch -a
* config-init-gitbook/dioaix
  master
  remotes/origin/master

$ git diff config-init-gitbook/dioaix master

$ git push -u origin config-init-gitbook/dioaix
Enter passphrase for key '/Users/dioaix/.ssh/id_rsa_dioaix@github': 
Enumerating objects: 56, done.
Counting objects: 100% (56/56), done.
Delta compression using up to 8 threads
Compressing objects: 100% (18/18), done.
Writing objects: 100% (55/55), 4.37 KiB | 638.00 KiB/s, done.
Total 55 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
remote: 
remote: Create a pull request for 'config-init-gitbook/dioaix' on GitHub by visiting:
remote:      https://github.com/dioaix/learn-git/pull/new/config-init-gitbook/dioaix
remote: 
To dioaix.github:dioaix/learn-git.git
 * [new branch]      config-init-gitbook/dioaix -> config-init-gitbook/dioaix
Branch 'config-init-gitbook/dioaix' set up to track remote branch 'config-init-gitbook/dioaix' from 'origin'.

$ git branch -a
* config-init-gitbook/dioaix
  master
  remotes/origin/config-init-gitbook/dioaix
  remotes/origin/master

$ git branch -vv
* config-init-gitbook/dioaix f0efeca [origin/config-init-gitbook/dioaix] Add SUMMARY.md and gitbook init files
  master                     f82e112 Merge pull request #1 from dioaix/config-set-.gitignore/dioaix
```
<br><br><br>



### 3.8.2.4.7 itHubでのPull Requestし、レビューを依頼

GitHubのウェブページで、Pull Requestを作成し、レビューを依頼。
<br><br><br>



### 3.8.2.4.8 本番稼働環境へのデプロイ

通常では、レビューが終わると、本番稼働環境へデプロイを行う。
その後、本番稼働環境で問題なく動作することをモニタリングする。
本手順では、デプロイがないので、省略する。
<br><br><br>


### 3.8.2.4.9 Remote ripositoryでmasterにマージ

モニタリングして、問題がなければ、
GitHubのウェブページで、masterにマージする。
<br><br><br>


### 3.8.2.4.10 Remote ripositoryでTopic branchを削除

GitHubのウェブページで、config-init-gitbook/dioaixを削除。
<br><br><br>


### 3.8.2.4.11 Local ripositoryでTopic branchを削除


```bash
$ git branch
* config-init-gitbook/dioaix
  master

$ git branch -a
* config-init-gitbook/dioaix
  master
  remotes/origin/config-init-gitbook/dioaix
  remotes/origin/master

$ git branch -vv
* config-init-gitbook/dioaix f0efeca [origin/config-init-gitbook/dioaix] Add SUMMARY.md and gitbook init files
  master                     f82e112 Merge pull request #1 from dioaix/config-set-.gitignore/dioaix

$ git checkout master
Switched to branch 'master'

$ git branch -d config-init-gitbook/dioaix
warning: deleting branch 'config-init-gitbook/dioaix' that has been merged to
         'refs/remotes/origin/config-init-gitbook/dioaix', but not yet merged to HEAD.
Deleted branch config-init-gitbook/dioaix (was f0efeca).

$ git branch
* master

$ git branch -a
* master
  remotes/origin/config-init-gitbook/dioaix
  remotes/origin/master

$ git branch -vv
* master f82e112 Merge pull request #1 from dioaix/config-set-.gitignore/dioaix
```
<br><br><br>


### 3.8.2.4.12 Remote ripository最新情報の反映

```bash
$ git checkout master
Already on 'master'

$ git branch --remote
  remotes/origin/config-init-gitbook/dioaix
  origin/master

$ git fetch -p
Enter passphrase for key '/Users/dioaix/.ssh/id_rsa_dioaix@github': 
From dioaix.github:dioaix/learn-git
 - [deleted]         (none)     -> origin/config-init-gitbook/dioaix
remote: Enumerating objects: 57, done.
remote: Counting objects: 100% (57/57), done.
remote: Compressing objects: 100% (18/18), done.
remote: Total 56 (delta 1), reused 55 (delta 1), pack-reused 0
Unpacking objects: 100% (56/56), done.
   f82e112..085c4ee  master     -> origin/master

$ git branch -a
* master
  remotes/origin/master
```
<br><br><br>



### 3.8.2.4.13 Remote ripositoryのmasterの変更分をLocal ripositoryのmasterにマージ

```bash
$ git checkout master
Already on 'master'

$ git fetch origin master
Enter passphrase for key '/Users/diaoix/.ssh/id_rsa_dioaix@github': 
From dioaix.github:dioaix/learn-git
 * branch            master     -> FETCH_HEAD

# [ローカル] → [リモート追跡]の差分を見る
$ git diff master origin/master
```
<br>


コミット履歴付きでマージする。
```bash
$ git merge --no-ff origin/master
```
<br>


以下のコミットメッセージをVScodeで記載。
```text
Merge remote-tracking branch 'origin/master'

[Why] Merge origin/master to master.
[How] Delete branch config-init-gitbook/dioaix, and Merge origin/master to master.
[Side effects] None.
```
<br><br><br>




VScodeのコミットメッセージを閉じるとコミット付きでMergeが始まる。
```text
Merge made by the 'recursive' strategy.
 SUMMARY.md                  | 43 +++++++++++++++++++++++++++++++++++++++++++
 part1/README.md             |  2 ++
 part2/README.md             |  2 ++
 part3/README.md             |  2 ++
 part3/chapter1/README.md    |  2 ++
 part3/chapter1/section1.md  |  2 ++
 part3/chapter1/section2.md  |  2 ++
 part3/chapter1/section3.md  |  2 ++
 part3/chapter1/section4.md  |  2 ++
 part3/chapter10/README.md   |  2 ++
 part3/chapter10/section1.md |  2 ++
 part3/chapter2/README.md    |  2 ++
 part3/chapter2/section1.md  |  2 ++
 part3/chapter2/section2.md  |  2 ++
 part3/chapter3/README.md    |  2 ++
 part3/chapter3/section1.md  |  2 ++
 part3/chapter3/section2.md  |  2 ++
 part3/chapter3/section3.md  |  2 ++
 part3/chapter4/README.md    |  2 ++
 part3/chapter4/section1.md  |  2 ++
 part3/chapter4/section2.md  |  2 ++
 part3/chapter4/section3.md  |  2 ++
 part3/chapter5/README.md    |  2 ++
 part3/chapter5/section1.md  |  2 ++
 part3/chapter5/section2.md  |  2 ++
 part3/chapter6/README.md    |  2 ++
 part3/chapter6/section1.md  |  2 ++
 part3/chapter6/section2.md  |  2 ++
 part3/chapter6/section3.md  |  2 ++
 part3/chapter7/README.md    |  2 ++
 part3/chapter7/section1.md  |  2 ++
 part3/chapter7/section2.md  |  2 ++
 part3/chapter7/section3.md  |  2 ++
 part3/chapter8/README.md    |  2 ++
 part3/chapter8/section1.md  |  2 ++
 part3/chapter8/section2.md  |  2 ++
 part3/chapter9/README.md    |  2 ++
 part3/chapter9/section1.md  |  2 ++
 part3/chapter9/section2.md  |  2 ++
 part3/chapter9/section3.md  |  2 ++
 40 files changed, 121 insertions(+)
 create mode 100644 SUMMARY.md
 create mode 100644 part1/README.md
 create mode 100644 part2/README.md
 create mode 100644 part3/README.md
 create mode 100644 part3/chapter1/README.md
 create mode 100644 part3/chapter1/section1.md
 create mode 100644 part3/chapter1/section2.md
 create mode 100644 part3/chapter1/section3.md
 create mode 100644 part3/chapter1/section4.md
 create mode 100644 part3/chapter10/README.md
 create mode 100644 part3/chapter10/section1.md
 create mode 100644 part3/chapter2/README.md
 create mode 100644 part3/chapter2/section1.md
 create mode 100644 part3/chapter2/section2.md
 create mode 100644 part3/chapter3/README.md
 create mode 100644 part3/chapter3/section1.md
 create mode 100644 part3/chapter3/section2.md
 create mode 100644 part3/chapter3/section3.md
 create mode 100644 part3/chapter4/README.md
 create mode 100644 part3/chapter4/section1.md
 create mode 100644 part3/chapter4/section2.md
 create mode 100644 part3/chapter4/section3.md
 create mode 100644 part3/chapter5/README.md
 create mode 100644 part3/chapter5/section1.md
 create mode 100644 part3/chapter5/section2.md
 create mode 100644 part3/chapter6/README.md
 create mode 100644 part3/chapter6/section1.md
 create mode 100644 part3/chapter6/section2.md
 create mode 100644 part3/chapter6/section3.md
 create mode 100644 part3/chapter7/README.md
 create mode 100644 part3/chapter7/section1.md
 create mode 100644 part3/chapter7/section2.md
 create mode 100644 part3/chapter7/section3.md
 create mode 100644 part3/chapter8/README.md
 create mode 100644 part3/chapter8/section1.md
 create mode 100644 part3/chapter8/section2.md
 create mode 100644 part3/chapter9/README.md
 create mode 100644 part3/chapter9/section1.md
 create mode 100644 part3/chapter9/section2.md
 create mode 100644 part3/chapter9/section3.md
```
<br><br><br>

マージの結果を確認する。
```bash
$ git status
On branch master
nothing to commit, working tree clean
```