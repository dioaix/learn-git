# 3.6.3 Blanchの作成からデプロイの一連作業


## 3.6.3.1 Topic blanchの作成

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
<br><br><br>


補足 : topicブランチの名前は、なんのためのブランチなのか説明する内容にする。  
例 : [Create | fix | improve]-何のために-何をする/dioaix  


<br><br><br>


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


## 3.6.3.2 ファイルの作成・編集

ワークツリーで、リポジトリのGit管理除外設定ファイルを作成する。
giboを使って、VScodeとGitbookに対応するように設定。

```bash
$ gibo dump VisualStudioCode Gitbook >> .gitignore

$ ls -la

$ cat .gitignore
```
<br>

## 3.6.3.3 Local repositoryでcommitする

作成したファイルをステージングエリアに追加する。
```bash
$ git add .gitignore

$ git status
On branch config-set-.gitgnore/dioaix
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

        new file:   .gitignore
```
<br><br><br>


Commitをして、gitディレクトリに格納する。

```bash
$ git commit
```
<br><br><br>


Gitのグローバルの環境設定により、VScodeが立ち上がり、以下のコミットメッセージを記入する。
```text
Add .gitignore for Mac VScode and Gitbook

[Why] Set the .gitignore file to exclude unnecessary files in repository to use VScode, Gitbook.
[How] Create the .gitignore file using the tool gibo.
[Side-effects] Unintended files may be excluded.
```
<br><br><br>



参考 : Gitコミットメッセージのフォーマットを決める際、以下のリンクを参考すべき。
https://github.com/objectx/git-style-guide

その一部を以下に記載する。
>scodeを使って、コミットメッセージを書く
>サマリー行（コミットメッセージの 1行目）は 説明的で 且つ 簡潔な ものにしましょう。 理想的には 50文字以下 の長さで、キャピタライズされた命令形の現在時制であるべきです。 コミットの タイトル として使える様に、末尾にピリオドを付けてはいけません:
>サマリー行の後は 1行の空行を挟んで、より完全な説明が書かれるべきです。 この節は なぜ この変更が必要で、 どうやって 問題に対処したのか、そして、どんな 副作用 があるのかを 72文字 折り返しで記述します。
>また、関連する事項へのポインタ（例: 関連する issue への bug tracker 上でのリンク）があるのなら、ここに書かれるべきです:
>コミットメッセージを書く場合、1年後に参照される事迄考えた上で書きましょう
>コミット A が他の コミット B に依存する場合、その依存関係はコミットメッセージの中に明示されるべきです。 参照するにはコミットハッシュを使うのが良いでしょう
>また コミット A が コミット B で入り込んだバグを解決した場合、 コミット A のコミットメッセージで コミット B に言及すべきです
>コミットが他のコミットに縮約される場合、コミットの意図を明確にするために --squish と --fixup が適切に使われるべきです:
<br><br><br>


参考フォーマット
>Short (50 chars or fewer) summary of changes
>
>More detailed explanatory text, if necessary. Wrap it to
72 characters. In some contexts, the first
line is treated as the subject of an email and the rest of
the text as the body.  The blank line separating the
summary from the body is critical (unless you omit the body
entirely); tools like rebase can get confused if you run
the two together.
>
>Further paragraphs come after blank lines.
>
>- Bullet points are okay, too
>
>- Use a hyphen or an asterisk for the bullet,
  followed by a single space, with blank lines in
  between
>
>Source http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html

<br><br><br>



補足 : ファイル変更の取り消し方法
  - ①ステージングにaddしたことを取り消し。  
    
    - ワークツリーで変更した内容は取り消されない。  
      ステージングの状態を最後のコミットと同じ状態にする。  
　　　   git reset HEAD FileName  
    - ワークツリーで変更した内容を取り消す場合、  
　　　 --hardオプションを使うことができる。直前のコミットの状態になる。  
　　　   git reset --hard FileName  

  - ②直前のローカルリポジトリのコミットの状態に、ワークツリーのファイルを戻す  
　  - ワークツリーで変更した内容も取り消される  
　　　 git checkout -- FileNameまたはDerectoryName 

<br><br><br>





## 3.6.3.4 Commit結果の確認


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





## 3.6.3.5 Remote repositoryにPush



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



## 3.6.3.6 GitHubでのPull Requestし、レビューを依頼

GitHubのウェブページで、Pull Requestを作成し、レビューを依頼。
<br><br><br>



## 3.6.3.7 本番稼働環境へのデプロイ

通常では、レビューが終わると、本番稼働環境へデプロイを行う。
その後、本番稼働環境で問題なく動作することをモニタリングする。
本手順では、デプロイがないので、省略する。
<br><br><br>


## 3.6.3.8 Remote ripositoryでmasterにマージ

モニタリングして、問題がなければ、
GitHubのウェブページで、masterにマージする。
<br><br><br>


## 3.6.3.9 Remote ripositoryでTopic branchを削除

GitHubのウェブページで、config-set-.gitignore/dioaixを削除。
<br><br><br>


## 3.6.3.10 Local ripositoryでTopic branchを削除


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


## 3.6.3.11 Remote ripository最新情報の反映

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



## 3.6.3.12 Remote ripositoryのmasterの変更分をLocal ripositoryのmasterにマージ

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

