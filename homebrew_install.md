# homebrew install

##

https://brew.sh/index_ja
https://docs.brew.sh/Homebrew-on-Linux
https://docs.brew.sh/Installation

ichiro@ASUS-VivoBook:~$ apt list curl
一覧表示... 完了
curl/impish-updates,impish-security 7.74.0-1.3ubuntu2.2 amd64
curl/impish-updates,impish-security 7.74.0-1.3ubuntu2.2 i386
ichiro@ASUS-VivoBook:~$ sudo apt install curl
〜
ichiro@ASUS-VivoBook:~$ which curl
/usr/bin/curl

ichiro@ASUS-VivoBook:~$ apt list git
一覧表示... 完了
git/impish-updates,impish-security 1:2.32.0-1ubuntu1.2 amd64
git/impish-updates,impish-security 1:2.32.0-1ubuntu1.2 i386
ichiro@ASUS-VivoBook:~$ sudo apt install git
ichiro@ASUS-VivoBook:~$ which git
/usr/bin/git


/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

==> Checking for `sudo` access (which may request your password)...
==> Select a Homebrew installation directory:
- Enter your password to install to /home/linuxbrew/.linuxbrew (recommended)
- Press Control-D to install to /home/ichiro/.linuxbrew
- Press Control-C to cancel installation
[sudo] ichiro のパスワード: 

※ ここで Control-D を入力することで、/home/ichiro/.linuxbrew にインストールされる

〜
Updated 1 tap (homebrew/core).
Warning: /home/ichiro/.linuxbrew/bin is not in your PATH.
  Instructions on how to configure your shell for Homebrew
  can be found in the 'Next steps' section below.
==> Installation successful!

==> Homebrew has enabled anonymous aggregate formulae and cask analytics.
Read the analytics documentation (and how to opt-out) here:
  https://docs.brew.sh/Analytics
No analytics data has been sent yet (nor will any be during this install run).

==> Homebrew is run entirely by unpaid volunteers. Please consider donating:
  https://github.com/Homebrew/brew#donations

==> Next steps:
- Run these two commands in your terminal to add Homebrew to your PATH:
    echo 'eval "$(/home/ichiro/.linuxbrew/bin/brew shellenv)"' >> /home/ichiro/.profile
    eval "$(/home/ichiro/.linuxbrew/bin/brew shellenv)"
- Install Homebrew's dependencies if you have sudo access:
    sudo apt-get install build-essential
  For more information, see:
    https://docs.brew.sh/Homebrew-on-Linux
- We recommend that you install GCC:
    brew install gcc
- Run brew help to get started
- Further documentation:
    https://docs.brew.sh


ichiro@ASUS-VivoBook:~$ echo 'eval "$(/home/ichiro/.linuxbrew/bin/brew shellenv)"' >> /home/ichiro/.profile
ichiro@ASUS-VivoBook:~$ eval "$(/home/ichiro/.linuxbrew/bin/brew shellenv)"
ichiro@ASUS-VivoBook:~$ cat .profile 
〜
eval "$(/home/ichiro/.linuxbrew/bin/brew shellenv)"

ichiro@ASUS-VivoBook:~$ sudo apt-get install build-essential
〜

ichiro@ASUS-VivoBook:~$ brew install gcc
〜

ichiro@ASUS-VivoBook:~$ brew install sl
〜


## 追加設定

ichiro@ASUS-VivoBook:~$ echo $SHELL
/bin/bash

test -d ~/.linuxbrew && eval "$(~/.linuxbrew/bin/brew shellenv)"
test -d /home/linuxbrew/.linuxbrew && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
test -r ~/.bash_profile && echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.bash_profile
echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.profile


## cask を追加

以下のメッセージより

```
 % brew search gimp 
==> Formulae
gmp ✔

If you meant "gimp" specifically:
It was migrated from homebrew/core to homebrew/cask.
You can access it again by running:
  brew tap homebrew/cask
And then you can install it by running:
  brew install --cask gimp
```

brew tap homebrew/cask

```
homebrew/cask
homebrew/core
```




## アンインストール

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/uninstall.sh)"
〜
==> /usr/bin/sudo /usr/bin/find /home/ichiro/.linuxbrew/bin /home/ichiro/.linuxbrew/etc /home/ichiro/.linuxbrew/include /home/ichiro/.linuxbrew/lib /home/ichiro/.linuxbrew/opt /home/ichiro/.linuxbrew/sbin /home/ichiro/.linuxbrew/share /home/ichiro/.linuxbrew/var /home/ichiro/.linuxbrew/Frameworks -depth -type d -empty -exec rmdir {} ;
==> /usr/bin/sudo rmdir /home/ichiro/.linuxbrew
rmdir: '/home/ichiro/.linuxbrew' を削除できません: ディレクトリは空ではありません
Warning: Failed during: /usr/bin/sudo rmdir /home/ichiro/.linuxbrew
Warning: Homebrew partially uninstalled (but there were steps that failed)!
To finish uninstalling rerun this script with `sudo`.
The following possible Homebrew files were not deleted:
/home/ichiro/.linuxbrew/bin/
/home/ichiro/.linuxbrew/etc/
/home/ichiro/.linuxbrew/include/
/home/ichiro/.linuxbrew/lib/
/home/ichiro/.linuxbrew/opt/
/home/ichiro/.linuxbrew/sbin/
/home/ichiro/.linuxbrew/share/
You may wish to remove them yourself.


rm -rf .linuxbrew





