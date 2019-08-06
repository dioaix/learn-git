# 3.4.3 Githubの関連設定

### PCでのGitHub用暗号鍵の生成

暗号鍵の生成
```bash
$ cd
$ ssh-keygen -t rsa -b 4096 -C "For dioaix@Github"

Chang rsa file name.
/Users/dioaix/.ssh/id_rsa_dioaix@github

Enter passphrase: pass
```
<br>


### GitHubで公開鍵を登録

PCから暗号鍵のデータをコピーする
```bash
$ pbcopy < /Users/dioaix/.ssh/id_rsa_dioaix@github.pub
```

GitHubのWebページで公開鍵を登録

Title : [PC Hostname] /Users/dioaix/.ssh/id_rsa_dioaix@github.pub

Key : Paste the public key from pbcopy to github.
<br>
<br>
<br>


### リモートリポジトリへの接続設定

SSH接続の設定

```bash
$ vim ~/.ssh/config

Host dioaix.github
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_rsa_dioaix@github
```
<br>

SSH接続テスト

```bash
$ ssh dioaix_github
Enter passphrase for key '/Users/dioaix/.ssh/id_rsa_dioaix@github': pass
PTY allocation request failed on channel 0
Hi dioaix! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.
```
<br>
