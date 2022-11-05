# CUI で Markdown が 見れるように glow を入れる

## dpkg に glow はなかった

```
sudo apt list glow
  [sudo] ichiro のパスワード: 
  一覧表示... 完了

  sudo apt search glow
  ソート中... 完了
  全文検索... 完了  
  gimp-plugin-registry/impish 9.20200927 amd64
    repository of optional extensions for GIMP

  glowing-bear/impish,impish 0.9.0+ds-2 all
    Web frontend for the WeeChat IRC client

  pinta/impish,impish 1.6-2 all
    Simple drawing/painting program

  plymouth-themes/impish 0.9.5git20210406-0ubuntu2 amd64
    boot animation, logger and I/O multiplexer - themes

  primrose/impish 6+dfsg1-4build1 amd64
    compelling tile-placement puzzle game
```

## brew に glow があった！！

```
brew search glow
  ==> Formulae
  glow                                  glog                                  glfw                                  glew

  ==> Casks
  homebrew/cask-fonts/font-glow-sans-j-compressed   homebrew/cask-fonts/font-glow-sans-sc-compressed  homebrew/cask-fonts/font-glow-sans-tc-compressed
  homebrew/cask-fonts/font-glow-sans-j-condensed    homebrew/cask-fonts/font-glow-sans-sc-condensed   homebrew/cask-fonts/font-glow-sans-tc-condensed
  homebrew/cask-fonts/font-glow-sans-j-extended     homebrew/cask-fonts/font-glow-sans-sc-extended    homebrew/cask-fonts/font-glow-sans-tc-extended
  homebrew/cask-fonts/font-glow-sans-j-normal       homebrew/cask-fonts/font-glow-sans-sc-normal      homebrew/cask-fonts/font-glow-sans-tc-normal
  homebrew/cask-fonts/font-glow-sans-j-wide         homebrew/cask-fonts/font-glow-sans-sc-wide        homebrew/cask-fonts/font-glow-sans-tc-wide
```

## brew より glow インストール！！

```
brew install glow
  Running `brew update --auto-update`...
  ==> Auto-updated Homebrew!
  Updated 1 tap (homebrew/cask).

  You have 1 outdated formula installed.
  You can upgrade it with brew upgrade
  or list it with brew outdated.

  ==> Downloading https://ghcr.io/v2/homebrew/core/glow/manifests/1.4.1
  ######################################################################## 100.0%
  ==> Downloading https://ghcr.io/v2/homebrew/core/glow/blobs/sha256:a57317e524f7ca1af42f21c91b1e387faa9a0c7e33efae5193443be86dd38a83
  ==> Downloading from https://pkg-containers.githubusercontent.com/ghcr1/blobs/sha256:a57317e524f7ca1af42f21c91b1e387faa9a0c7e33efae5193443be86dd38a83?se=2022-07-
  ######################################################################## 100.0%
  ==> Pouring glow--1.4.1.x86_64_linux.bottle.tar.gz
  🍺  /home/linuxbrew/.linuxbrew/Cellar/glow/1.4.1: 5 files, 18.2MB
  ==> Running `brew cleanup glow`...
  Disable this behaviour by setting HOMEBREW_NO_INSTALL_CLEANUP.
  Hide these hints with HOMEBREW_NO_ENV_HINTS (see `man brew`).
```
