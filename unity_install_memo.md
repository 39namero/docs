# Unity install

https://docs.unity3d.com/hub/manual/InstallHub.html#install-hub-linux

## ダウンロードサイト

https://docs.unity3d.com/hub/manual/InstallHub.html#install-hub-linux

## UnityHubリポジトリを追加

sudo sh -c 'echo "deb https://hub.unity3d.com/linux/repos/deb stable main" > /etc/apt/sources.list.d/unityhub.list'

## 公開署名キーを追加

wget -qO - https://hub.unity3d.com/linux/keys/public | sudo apt-key add -

## インストール

sudo apt update

sudo apt-get install unityhub

## アンインストール

sudo apt-get remove unityhub

