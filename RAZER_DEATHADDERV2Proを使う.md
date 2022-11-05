# RAZER DEATHADDER V2 Pro を使う

## apt パッケージを最新化

sudo apt update
sudo apt upgrade

## ドライバーインストール

### linux-header がインストールされていることを確認する

sudo dpkg -l | grep linux-header

### PPA インストール

sudo apt install software-properties-gtk

sudo add-apt-repository ppa:openrazer/stable

### パッケージをインストール

sudo apt update
sudo apt install openrazer-meta

### 再起動

sudo systemctl reboot

これで何ができて、何がインストールされるのか？
やってみないとわからない




Razer in Linux
https://www.youtube.com/watch?v=dlC5I6BTunQ

Control Razer device from Linux!
https://www.youtube.com/watch?v=A0D0L-F1V7E


LinuxでのRazerRGBのセットアップ-ManjaroLinux-Linuxでのゲーム
https://www.youtube.com/watch?v=muOTZUJChMI

OpenRazer
https://openrazer.github.io/

##  piper

linux で使用するデバイス制御アプリ

sudo apt install piper
sudo apt install ratbagd

## razergenie

https://software.opensuse.org//download.html?project=hardware%3Arazer&package=razergenie

echo 'deb http://download.opensuse.org/repositories/hardware:/razer/xUbuntu_21.10/ /' | sudo tee /etc/apt/sources.list.d/hardware:razer.list
curl -fsSL https://download.opensuse.org/repositories/hardware:razer/xUbuntu_21.10/Release.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/hardware_razer.gpg > /dev/null
sudo apt update
sudo apt install razergenie

```
    パッケージリストを読み込んでいます... 完了
    依存関係ツリーを作成しています... 完了        
    状態情報を読み取っています... 完了        
    以下のパッケージが新たにインストールされます:
    razergenie
    アップグレード: 0 個、新規インストール: 1 個、削除: 0 個、保留: 2 個。
    143 kB のアーカイブを取得する必要があります。
    この操作後に追加で 569 kB のディスク容量が消費されます。
    取得:1 http://download.opensuse.org/repositories/hardware:/razer/xUbuntu_21.10  razergenie 0.9.0-0 [143 kB]
    143 kB を 5秒 で取得しました (30.7 kB/s)
    以前に未選択のパッケージ razergenie を選択しています。
    (データベースを読み込んでいます ... 現在 272782 個のファイルとディレクトリがインストールされています。)
    .../razergenie_0.9.0-0_amd64.deb を展開する準備をしています ...
    razergenie (0.9.0-0) を展開しています...
    razergenie (0.9.0-0) を設定しています ...
    desktop-file-utils (0.26-1ubuntu2) のトリガを処理しています ...
    hicolor-icon-theme (0.17-2) のトリガを処理しています ...
    gnome-menus (3.36.0-1ubuntu1) のトリガを処理しています ...
    libc-bin (2.34-0ubuntu3.2) のトリガを処理しています ...
    mailcap (3.69ubuntu1) のトリガを処理しています ...
```