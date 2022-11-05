# git-remote-repository.md

Gitでリモートリポジトリを作成する
https://spirits.appirits.com/doruby/12220/

## test 作成

### git local 初期設定

git config --global user.name "ichiro"

git config --global user.email namero.dotanba@icloud.com

git config --list --show-origin
    file:/home/ichiro/.gitconfig    user.name=ichiro
    file:/home/ichiro/.gitconfig    user.email=namero.dotanba@icloud.com

### remote repository 作成

pwd
    /home/kentaro/ドキュメント/develop/repos

mkdir sample.git
cd sample.git

git --bare init
    hint: Using 'master' as the name for the initial branch. This default branch name

### local repository 作成

pwd
    /home/ichiro/Documents/develp/git

mkdir sample-repo
cd sample-repo

git init

touch sample.txt
git add sample.txt

git commit -m "first commit"
    hint: Using 'master' as the name for the initial branch. This default branch name
    hint: is subject to change. To configure the initial branch name to use in all
    hint: of your new repositories, which will suppress this warning, call:
    hint: of your new repositories, which will suppress this warning, call:
    hint:
    hint:   git config --global init.defaultBranch <name>
    hint:
    hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
    hint: 'development'. The just-created branch can be renamed via this command:
    hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
    hint: 'development'. The just-created branch can be renamed via this command:
    hint:
    hint:   git branch -m <name>
    Initialized empty Git repository in /home/ichiro/Documents/develp/git/sample-repo/.git/

### remote repository を追加して push

git remote add origin ssh://kentaro@192.168.0.21/home/kentaro/ドキュメント/develop/repos/sample.gitG
e    hint: of your new repositories, which will suppress this warning, call:
    hint:
    hint:   git config --global init.defaultBranch <name>
    hint:
    hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
    hint: 'development'. The just-created branch can be renamed via this command:
    hint:
    hint:   git branch -m <name>
    Initialized empty Git repository in /home/kentaro/ドキュメント/develop/repos/sample.git/

git push origin master
    kentaro@192.168.0.21's password:
    Enumerating objects: 3, done.
    Counting objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 212 bytes | 14.00 KiB/s, done.
    Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
    To ssh://192.168.0.21/home/kentaro/ドキュメント/develop/repos/sample.git
    * [new branch]      master -> master

### リモートリポジトリを削除する場合

ローカルで

git remote remove origin


リモートで

rm -rf sample.git

## 本格作成

### remote repository 作成

pwd
    /home/kentaro/ドキュメント/develop/repos

mkdir org.git
cd org.git

git --bare init
    hint: Using 'master' as the name for the initial branch. This default branch name
    hint: is subject to change. To configure the initial branch name to use in all
    hint: of your new repositories, which will suppress this warning, call:
    hint: 
    hint: 	git config --global init.defaultBranch <name>
    hint: 
    hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
    hint: 'development'. The just-created branch can be renamed via this command:
    hint: 
    hint: 	git branch -m <name>
    Initialized empty Git repository in /home/kentaro/ドキュメント/develop/repos/org.git/

### local repository 確認

pwd
    /home/ichiro/Documents/install_docs

git branch
    * master

### remote repository を追加して push

git remote add org ssh://kentaro@192.168.0.21/home/kentaro/ドキュメント/develop/repos/org.git

git push org master
    kentaro@192.168.0.21's password: 
    Enumerating objects: 38, done.
    Counting objects: 100% (38/38), done.
    Delta compression using up to 2 threads
    Compressing objects: 100% (38/38), done.
    Writing objects: 100% (38/38), 30.84 KiB | 1.81 MiB/s, done.
    Total 38 (delta 3), reused 0 (delta 0), pack-reused 0
    To ssh://192.168.0.21/home/kentaro/ドキュメント/develop/repos/org.git
    * [new branch]      master -> master



## リモートリポジトリ名を変更したいのでやり直し（三回目）

リポジトリを削除して作り直す

### ローカルで

pwd
    /home/ichiro/Documents/install_docs

git remote remove org

### リモートで

pwd
    /home/kentaro/ドキュメント/develop/repos

rm -rf org.git


### remote repository 作成

pwd
    /home/kentaro/ドキュメント/develop/repos

mkdir ubuntu_install_docs.git
cd ubuntu_install_docs.git

git --bare init
    hint: Using 'master' as the name for the initial branch. This default branch name
    hint: is subject to change. To configure the initial branch name to use in all
    hint: of your new repositories, which will suppress this warning, call:
    hint: 
    hint: 	git config --global init.defaultBranch <name>
    hint: 
    hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
    hint: 'development'. The just-created branch can be renamed via this command:
    hint: 
    hint: 	git branch -m <name>
    Initialized empty Git repository in /home/kentaro/ドキュメント/develop/repos/ubuntu_install_docs.git/

### local repository 確認

pwd
    /home/ichiro/Documents/install_docs

git branch
    * master

### remote repository を追加して push

git remote add ubuntu_install_docs ssh://kentaro@192.168.0.21/home/kentaro/ドキュメント/develop/repos/ubuntu_install_docs.git

git push ubuntu_install_docs master
    kentaro@192.168.0.21's password: 
    Enumerating objects: 38, done.
    Counting objects: 100% (38/38), done.
    Delta compression using up to 2 threads
    Compressing objects: 100% (38/38), done.
    Writing objects: 100% (38/38), 30.84 KiB | 1.81 MiB/s, done.
    Total 38 (delta 3), reused 0 (delta 0), pack-reused 0
    To ssh://192.168.0.21/home/kentaro/ドキュメント/develop/repos/org.git
    * [new branch]      master -> master

### repository を分けよう

master から develop を作成する

git switch -c develop master

git push -u レポジトリ名 作成したブランチ名

git push -u ubuntu_install_docs develop
    kentaro@192.168.0.21's password: 
    Total 0 (delta 0), reused 0 (delta 0), pack-reused 0
    To ssh://192.168.0.21/home/kentaro/ドキュメント/develop/repos/ubuntu_install_docs.git
    * [new branch]      develop -> develop
    Branch 'develop' set up to track remote branch 'develop' from 'ubuntu_install_docs'.

git branch -a
    * develop
    master
    remotes/ubuntu_install_docs/develop
    remotes/ubuntu_install_docs/master

## MacBook Pro から remote repository を clone

git clone --branch develop ssh://kentaro@192.168.0.21/home/kentaro/ドキュメント/develop/repos/ubuntu_install_docs.git

cd ubuntu_install_docs

git pull ubuntu_install_docs develop

大体できるようにはなったのだが…

git branch -a
    * develop
    remotes/origin/HEAD -> origin/master
    remotes/origin/develop
    remotes/origin/master

Mac 側で origin となるのをなんとかしたい
だって、Ubuntu 側からは

    remotes/ubuntu_install_docd/develop

となっている

## 変更時の操作・まとめ

### Mac 側

git pull origin develop  

git add git-remote-repository.md
git commit git-remote-repository.md

git push -u origin develop

### Ubuntu 側

git pull ubuntu_install_docs develop

git add git-remote-repository.md
git commit git-remote-repository.md

git push -u ubuntu_install_docs develop
