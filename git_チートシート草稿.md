# git チートシート草稿

## ベアリポジトリから、ローカルリポジトリを作成

`git clone /home/kentaro/ドキュメント/develop/repos/ubuntu_install_docs.git`

特定のブランチを取得する場合

`git clone --branch develop /home/kentaro/ドキュメント/develop/repos/ubuntu_install_docs.git`

特定のブランチの最終コミットのみ取得する場合

`git clone --depth 1 --branch develop /home/kentaro/ドキュメント/develop/repos/ubuntu_install_docs.git`

-oオプションを使用することで、origin以外の名前を指定することができる

`git clone -o target /home/kentaro/ドキュメント/develop/repos/ubuntu_install_docs.git`

`ls -ld ubuntu_install_docs`

```
    drwxrwxr-x 3 kentaro kentaro 4096 11月  1 22:47 ubuntu_install_docs
```

`cd ubuntu_install_docs`

`git branch`

```
    * master
```

`git branch -r`

```
    origin/HEAD -> origin/master
    origin/develop
    origin/master
```

`git switch develop`

```
    Branch 'develop' set up to track remote branch 'develop' from 'origin'.
    Switched to a new branch 'develop'
```

`git branch`

```
    * develop
    master
```

`git switch -c optiplex/ichi0001`
`
`git branch`

```
    develop
    master
    * optiplex/ichi0001
```

## ベアリポジトリ・ブランチ削除

特定のローカルリポジトリで以下を実行する

`git push origin --delete future/code000`

各ローカルリポジトリで以下を実行することで、削除も含めて同期
（ -p フラグは "prune" (取り除く) を意味する ）

`git fetch -p`

## ローカルにないリモートブランチを取得する

上の `git fetch -p` と関連し、ローカルにないリモートブランチを取得するには以下とする

git fetch

git branch -r

## アップストリーム（upstream）ブランチについて

作業中のローカルブランチと関連付けられているリモートリポジトリのブランチの最新の状態を反映するには

`git pull`

とする

関連付けられているブランチのことをアップストリーム（upstream）ブランチという

アップストリームブランチは以下コマンドで確認できる

`git branch -vv`

`git remote -v`

アップストリーム以外のブランチを指定したい場合はgit pullに引数をつけて実行

`git pull origin feature/hogehoge`

アップストリームブランチを明示的に設定する場合は、以下コマンドを実行

`git branch --set-upstream-to=<remote>/<branch> [ローカルブランチ名]`

## git fetch

`git fetch --all`