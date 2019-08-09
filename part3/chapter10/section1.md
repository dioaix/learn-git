# 3.10.1 新規Local Repositoryから,Remote Repositoryにpush時のrejectエラー対処

新規でRemote RepositoryとLocal Repositoryを作成する場合、初めてのPushで下記の事象で、エラーが起きる場合がある。

## エラー事象
先にGitHubでRemote Repositoryを作成する時に、READMEを作成した場合、それ自体を一つのCommitと見なされて、Local RepositoryでPushすると下記のエラーでrejectされる。

```bash
$ git push -u origin master
Enter passphrase for key '/Users/dioaix/.ssh/id_rsa_dioaix@github': 
To dioaix.github:dioaix/learn-git.git
 ! [rejected]        master -> master (fetch first)
error: failed to push some refs to 'git@dioaix.github:dioaix/learn-git.git'
hint: Updates were rejected because the remote contains work that you do
hint: not have locally. This is usually caused by another repository pushing
hint: to the same ref. You may want to first integrate the remote changes
hint: (e.g., 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```


## 解決方法


まずは、READMEファイルをLocal Repositoryにマージする。

```bash
$ git fetch
Enter passphrase for key '/Users/dioaix/.ssh/id_rsa_dioaix@github':
warning: no common commits
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From github.com:dioaix/learn-git
 * [new branch]      master     -> origin/master




$ git merge --allow-unrelated-histories origin/master
Merge made by the 'recursive' strategy.
 README.md | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
```


「--allow-unrelated-histories」について
Gitのバージョン2.9より、無関係な履歴を持つ２つのblanch間でのmergeとpullでは，「--allow-unrelated-histories」を指定しないとできない。
<br><br><br>


その後、Local Repositoryのブランチより、Pushする。

```bash
$ git push -u origin master
Enter passphrase for key '/Users/dioaix/.ssh/id_rsa_dioaix@github':
Enumerating objects: 41, done.
Counting objects: 100% (41/41), done.
Delta compression using up to 4 threads
Compressing objects: 100% (34/34), done.
Writing objects: 100% (40/40), 16.13 KiB | 869.00 KiB/s, done.
Total 40 (delta 9), reused 0 (delta 0)
remote: Resolving deltas: 100% (9/9), done.
To dioaix.github:dioaix/learn-git.git
   7aa37d3..2f75409  master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```