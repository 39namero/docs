# zsh に変更しよう

zsh への変更手順
https://blog.mktia.com/change-shell-from-bash-to-zsh-in-ubuntu/

echo $SHELL

ichiro@ASUS-VivoBook:~$ echo $SHELL
/bin/bash

which zsh

ichiro@ASUS-VivoBook:~$ which zsh
ichiro@ASUS-VivoBook:~$ 


ichiro@ASUS-VivoBook:~$ apt list zsh
一覧表示... 完了
zsh/impish-updates,impish-security 5.8-6ubuntu0.1 amd64
zsh/impish-updates,impish-security 5.8-6ubuntu0.1 i386
ichiro@ASUS-VivoBook:~$ sudo apt install zsh
[sudo] ichiro のパスワード: 
パッケージリストを読み込んでいます... 完了
依存関係ツリーを作成しています... 完了        
状態情報を読み取っています... 完了        
以下のパッケージが自動でインストールされましたが、もう必要とされていません:
  chromium-codecs-ffmpeg-extra gstreamer1.0-vaapi libfwupdplugin1
  libgstreamer-plugins-bad1.0-0 libva-wayland2
これを削除するには 'sudo apt autoremove' を利用してください。
以下の追加パッケージがインストールされます:
  zsh-common
提案パッケージ:
  zsh-doc
以下のパッケージが新たにインストールされます:
  zsh zsh-common
アップグレード: 0 個、新規インストール: 2 個、削除: 0 個、保留: 0 個。
4,753 kB のアーカイブを取得する必要があります。
この操作後に追加で 18.1 MB のディスク容量が消費されます。
続行しますか? [Y/n] y
取得:1 http://jp.archive.ubuntu.com/ubuntu impish-updates/main amd64 zsh-common all 5.8-6ubuntu0.1 [3,944 kB]
取得:2 http://jp.archive.ubuntu.com/ubuntu impish-updates/main amd64 zsh amd64 5.8-6ubuntu0.1 [809 kB]
4,753 kB を 7秒 で取得しました (730 kB/s)                                           
以前に未選択のパッケージ zsh-common を選択しています。
(データベースを読み込んでいます ... 現在 202384 個のファイルとディレクトリがインスト
ールされています。)
.../zsh-common_5.8-6ubuntu0.1_all.deb を展開する準備をしています ...
zsh-common (5.8-6ubuntu0.1) を展開しています...
以前に未選択のパッケージ zsh を選択しています。
.../zsh_5.8-6ubuntu0.1_amd64.deb を展開する準備をしています ...
zsh (5.8-6ubuntu0.1) を展開しています...
zsh-common (5.8-6ubuntu0.1) を設定しています ...
zsh (5.8-6ubuntu0.1) を設定しています ...
man-db (2.9.4-2) のトリガを処理しています ...


ichiro@ASUS-VivoBook:~$ which zsh
/usr/bin/zsh

ichiro@ASUS-VivoBook:~$ chsh -s $(which zsh)
パスワード: 

※ ここで gnome ごとログオフ・ログインしてターミナルを起動する

This is the Z Shell configuration function for new users,
zsh-newuser-install.
You are seeing this message because you have no zsh startup files
(the files .zshenv, .zprofile, .zshrc, .zlogin in the directory
~).  This function can help you with a few settings that should
make your use of the shell easier.

You can:

(q)  Quit and do nothing.  The function will be run again next time.

(0)  Exit, creating the file ~/.zshrc containing just a comment.
     That will prevent this function being run again.

(1)  Continue to the main menu.

(2)  Populate your ~/.zshrc with the configuration recommended
     by the system administrator and exit (you will need to edit
     the file by hand, if so desired).

--- Type one of the keys in parentheses --- 2
/home/ichiro/.zshrc:15: scalar parameter HISTFILE created globally in function zsh-newuser-install
(eval):1: scalar parameter LS_COLORS created globally in function zsh-newuser-install

2 のおすすめ設定を選択しておこう

vi .zshrc
〜
# 2022.6.1 add homebrew
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"





eval $($(brew --prefix)/bin/brew shellenv)
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"



